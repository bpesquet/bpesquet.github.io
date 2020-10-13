---
title: "Deconstructing AI"
date: 2019-12-09T10:47:12+01:00
draft: false
weight: 1
---

## Summary

- What Is AI, Actually?
- How Do Machines Learn?
- Should We Be Scared Of AI?

---

## What Is AI, Actually?

---

## The original ambition of AI

> "AI is the science and engineering of making intelligent machines." ([John McCarthy](https://en.wikipedia.org/wiki/John_McCarthy_(computer_scientist)))

> "Every aspect of learning or any other feature of intelligence can in principle be so precisely described that a machine can be made to simulate it." ([Dartmouth Workshop](https://en.wikipedia.org/wiki/Dartmouth_workshop), 1956)

> "AI is the science of making machines do things that would require intelligence if done by men." ([Marvin Minsky](https://en.wikipedia.org/wiki/Marvin_Minsky))

---

## A technical definition of AI

> "AI refers to systems that **display** intelligent behavior by analysing their **environment** and taking **actions** - with some degree of **autonomy** - to achieve specific **goals**." ([EC, 2018](https://ec.europa.eu/newsroom/dae/document.cfm?doc_id=51625))

AI systems can be either:

- Purely **software**-based (e.g. voice assistants, search engines, face recognition systems).
- Embedded in **hardware** devices (e.g. robots, autonomous cars, drones).

---

## Main areas of research

- **Problem solving** (e.g. search algorithms, constraint solving).
- **Reasoning** and **decision making** (e.g. logic, knowledge representation).
- **Machine Learning**.
- **Real-world interactions** (e.g. computer vision, natural language understanding, robotics).

---

## AI is a moving target

As soon as AI successfully solves a problem, the problem is no longer considered a part of AI.

> "[AI is whatever hasn't been done yet](https://en.wikipedia.org/wiki/AI_effect)."

---

## The tumultuous history of AI

[![The AI timeline](images/ai_timeline.png)](https://www.slideshare.net/dlavenda/ai-and-productivity)

---

## AI is a highly interdisciplinary field

![AI fields](images/ai_fields.png)

---

## AI is a social science

AI has many social and societal implications:

- Job market transformation.
- Human/machine interactions.
- Trust and acceptability.
- Legal aspects and regulation.
- Fairness.
- Ethical use.
- Personal data.
- ...

---

## AI comes in different flavours

- **Substitutive intelligence**: replacement of men by machines.
- **Augmented intelligence**: human-centered AI for performance augmentation & autonomy enhancement.
- **Hybrid intelligence**: human-machine collaboration on complex tasks.

---

## A broader definition of AI

> "AI is an **interdisciplinary** field aiming at **understanding** and **imitating** the mechanisms of **cognition** and **reasoning**, in order to **assist** or **substitute** humans in their activities." ([Commission d'enrichissement de la langue française](https://fr.wikipedia.org/wiki/Commission_d%27enrichissement_de_la_langue_fran%C3%A7aise), 2018)

---

## How Do Machines Learn?

---

## Machine Learning in a nutshell

Set of techniques for giving machines the ability to find **patterns** and extract **rules** from data, in order to:

- **Identify** or **classify** elements.
- Detect **tendencies**.
- Make **predictions**.

As more data is fed into the system, results get better: performance improves with experience.

a.k.a. **Statistical Learning**.

---

![AI/ML/DL Venn diagram](images/ai_ml_dl.png)

---

![ML category tree](images/machine_learning_tree.png)

---

## A new paradigm

![Programming paradigm](images/programming_paradigm.png)

![Training paradigm](images/training_paradigm.png)

---

## The Machine Learning workflow

1. **Frame** the problem.
1. Collect, analyze and prepare **data**.
1. Select and train several **models** on data.
1. **Tune** the most promising model.
1. **Deploy** the model to production.

---

## ML is not a silver bullet!

- Some use cases are a better fit for ML than others:
  - Difficulty to express the actions as rules.
  - Data too complex for traditional analytical methods.
  - Performance > interpretability.
- Data quality is paramount.

---

## Algorithm #1: K-Nearest Neighbors

Prediction is based on the `k` nearest neighbors of a data sample.

[![K-NN](images/knn.png)](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm)

---

## Algorithm #2: Decision Trees

Build a tree-like structure based on a series of discovered questions on the data.

![Decision Tree for Iris dataset](images/dt_iris.png)

---

## Algorithm #3: Neural Networks

- Layers of loosely neuron-inpired computation units.
- Can approximate any continuous function.

![Neuron output](images/neuron_output.png)

---

![Dog or Cat?](images/neural_net.gif)

---

## Training a network

![Training and inference](images/training_inference1.png)

---

## The Deep Learning tsunami

- Multilayered neural networks trained on (generally) vast amounts of data.

[![AlexNet'12 (simplified)](images/alexnet.png)](https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf)

- Since 2010, outperformed previous state-of-the-art techniques in many fields (language translation, image and scene recognition...).

---

![Big data universe](images/big_data_universe.png)

---

![Computer power sheet](images/infographic2-intel-past-present.gif)

---

## From labs to everyday life

[![LeCun - LeNet](images/lecun_lenet.gif)](http://yann.lecun.com/exdb/lenet/)

[![Facial recognition in Chinese elementary school](images/china_school_facial_reco.gif)](https://twitter.com/mbrennanchina/status/1203687857849716736)

---

## Should We Be Scared Of AI?

---

## AI is altering the job market...

- Machines outperform humans in a growing list of cognitive tasks.
- Repetitive tasks are most exposed (even complex ones, like medical diagnosis or financial analysis).
- Entire industries are on the verge of disruption (example: truck-based transportation, first employer in the U.S.).

---

## ... For better or worse

- Net impact of AI on job quantity is unknown.
- Most jobs will be **transformed**, not replaced by AI.
  - Boring and repetitive stuff will be automated.
  - AI will add new insight to help human decision.
- Human/machine interactions will multiply.
- Their quality will be a key factor of performance for organizations.

---

## Real or fake?

[![GAN progress from 2014 to 2018](images/gan_2014_2018.jpg)](https://twitter.com/goodfellow_ian/status/1084973596236144640)

---

## AGI is very far away

- Current AI systems are **weak**: highly tuned to perform well in one task.
- **Artificial General Intelligence** a.k.a. **strong AI**, the ability to perform any task as well as a human, is out of reach.

[![Y. LeCun tweet on AGI, Déc. 2019](images/ylecun_tweet_agi.png)](https://twitter.com/ylecun/status/1204013978210320384)

---

## The intelligence debate

- Despite their complexity, ML and DL algorithms can be viewed as merely [curve fitting](https://diginomica.com/ai-curve-fitting-not-intelligence).
- On the contrary, some AI researchers envision DL as a new form of **algorithmic reasoning**, somehow mimicking the human brain.

---

## The human brain is a masterpiece

- Approx. 86 billions neurons in 1.4 kg.
- Typical energy consumption: 20 W (!)
- So much of it is still unknown.

![The human brain](images/human_brain.jpg)

---

## Babies are outstanding learners

[![Conceptuals acquisitions by babies](images/conceptual_acquisition_infants.png)](http://www.lscp.net/persons/dupoux/)

---

## Any questions?

![The cutest baby ever](images/cutest_baby_ever.png)
