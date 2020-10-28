---
title: "Let's build an autodiff engine! - Part 1: motivation and inspirations"
date: 2020-10-28T16:10:03+01:00
draft: true
---

## Existing autodiff engines

### micrograd

When he's not working at Tesla, [Andrej Karpathy](https://karpathy.github.io/) seems to enjoy publishing minimalist implementations of complex topics. [micrograd](https://github.com/karpathy/micrograd) is his attempt at creating the tiniest possible autodiff engine.

In about 100 LOC, this little gem implements reverse-mode autodiff for scalar values. On top of it, a PyTorch-like API lets you define and train neural networks.

Here's a glimpse of what **micrograd** can do.

```python
from micrograd.engine import Value

# Create a managed scalar value
x = Value(-4.0)
z = 2 * x + 2 + x  # z = -10
q = z.relu() + z * x  # q = 40
h = (z * z).relu()  # h = 100
y = h + q + q * x  # y = -20
# Compute gradients w.r.t. input values
y.backward()
print(x.grad)  # dy/dx = 46
```

Technically speaking, **micrograd** defines several attributes for each autodiff-managed value:

- `.data` is the wrapped scalar.
- `.grad` (also a scalar) is the computed value of its gradient.
- `._backward` is the function implementing the chain rule to compute the gradients for the operation that created the current value.
- `._prev` is the set of values involved in the computation of the current one.

```python
class Value:
    """ stores a single scalar value and its gradient """
    def __init__(self, data, _children=(), _op=''):
        self.data = data
        self.grad = 0
        # internal variables used for autograd graph construction
        self._backward = lambda: None
        self._prev = set(_children)
```

Each operation on a managed value creates a new value. The `_backward` function is defined as a nested function to gain access to its input and output values.

For example, here's how the multiplication operation is implemented in **micrograd**.

```python
def __mul__(self, other):
    other = other if isinstance(other, Value) else Value(other)
    out = Value(self.data * other.data, (self, other), '*')
    def _backward():
        self.grad += other.data * out.grad
        other.grad += self.data * out.grad
    out._backward = _backward
    return out
```

When it's time to backpropagate, a topogical list of all involved values is recursively built. For each of them (in reverse order), the `_backward` function is called to apply the chain rule and compute all gradients.

```python
def backward(self):
    # topological order all of the children in the graph
    topo = []
    visited = set()
    def build_topo(v):
        if v not in visited:
            visited.add(v)
            for child in v._prev:
                build_topo(child)
            topo.append(v)
    build_topo(self)

    # go one variable at a time and apply the chain rule to get its gradient
    self.grad = 1
    for v in reversed(topo):
        v._backward()
```

All in all, **micrograd** is a brilliant take on the autodiff subject, albeit limited (by design) to scalar values and first-order gradients.

### joelgrad

[Joel Grus](https://joelgrus.com/) also likes to create pedagogical resources on Machine Learning-related subjects (you may know him for [other](https://joelgrus.com/2016/05/23/fizz-buzz-in-tensorflow/) [reasons](https://docs.google.com/presentation/d/1n2RlMdmv1p25Xy5thJUhkKGvjtV-dkAIsUXP-AL4ffI/edit#slide=id.g362da58057_0_1) 😃). After coding a [Keras-like library](https://github.com/joelgrus/joelnet), he published a simple [autodiff engine](https://github.com/joelgrus/autograd) and a series of livecoding videos.

{{< youtube RxmBukb-Om4 >}}

At the heart of this library is a `Tensor` class wrapping a [NumPy](https://numpy.org/) array into its `.data` attribute. Other notable attributes are:

- `.requires_grad` which indicates if gradient should be computed for this tensor.
- `.depends_on` which is the list of dependencies towards other tensors. Each dependency is a `(tensor, function)` tuple.
- `.grad` which stores the computed gradient for this tensor.

```python
class Dependency(NamedTuple):
    tensor: 'Tensor'
    grad_fn: Callable[[np.ndarray], np.ndarray]

class Tensor:
    def __init__(self,
                 data: Arrayable,
                 requires_grad: bool = False,
                 depends_on: List[Dependency] = None) -> None:
        self._data = ensure_array(data)
        self.requires_grad = requires_grad
        self.depends_on = depends_on or []
        self.shape = self._data.shape
        self.grad: Optional['Tensor'] = None
```

> Note the use of [type annotations](https://docs.python.org/3/library/typing.html) for clarifying parameter types.

Tensor operations create an output tensor with dependencies. For each input tensor, a specific function computes and returns the gradient of the operation w.r.t. it.

For example, here's the implementation of the multiplication operation.

```python
def _mul(t1: Tensor, t2: Tensor) -> Tensor:
    data = t1.data * t2.data
    requires_grad = t1.requires_grad or t2.requires_grad
    depends_on: List[Dependency] = []

    if t1.requires_grad:
        def grad_fn1(grad: np.ndarray) -> np.ndarray:
            grad = grad * t2.data
            # ... (handle broadcasting)
            return grad
        depends_on.append(Dependency(t1, grad_fn1))

    if t2.requires_grad:
        def grad_fn2(grad: np.ndarray) -> np.ndarray:
            grad = grad * t1.data
            # ... (handle broadcasting)
            return grad
        depends_on.append(Dependency(t2, grad_fn2))

    return Tensor(data,
                  requires_grad,
                  depends_on)
```

Backpropagation is implemented in the `backward` method of the `Tensor` class. The received gradient is accumulated into the `.grad` attribute. For each dependency, the gradient is computed through the `grad_fn` function and passed to the subsequent `backward` call on the associated tensor. The computational graph is thus traversed in reverse order.

```python
def backward(self, grad: 'Tensor' = None) -> None:
    assert self.requires_grad, "called backward on non-requires-grad tensor"
    if grad is None:
        if self.shape == ():
            grad = Tensor(1.0)
        else:
            raise RuntimeError("grad must be specified for non-0-tensor")
    self.grad.data = self.grad.data + grad.data  # type: ignore
    for dependency in self.depends_on:
        backward_grad = dependency.grad_fn(grad.data)
        dependency.tensor.backward(Tensor(backward_grad))
```

This library is another inspirational example of what can be done to create an autodiff engine.

### autodidact

Through this [blog post](https://towardsdatascience.com/pytorch-autograd-understanding-the-heart-of-pytorchs-magic-2686cd94ec95), I discovered [autodidact](https://github.com/mattjj/autodidact).

### PyTorch

{{< youtube MswxJw-8PvE >}}

<https://jimmy-shen.medium.com/how-to-understand-pytorch-source-code-1fdbdbbf007e>

<https://pytorch.org/docs/stable/autograd.html#>
<https://github.com/pytorch/pytorch/tree/v0.1.1/torch/autograd>
<https://github.com/pytorch/pytorch/tree/v0.4.0/torch/autograd>

<https://www.cs.toronto.edu/~rgrosse/courses/csc321_2018/slides/lec10.pdf>
