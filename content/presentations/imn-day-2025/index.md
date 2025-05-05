---
marp: true
math: true  # Use default Marp engin for math rendering
title: "Towards metacognitive agents: integrating confidence in sequential decision-making"
date: 2025-05-05T10:04:27+02:00
draft: false
tags:
- decision-making
- confidence
style: |
  .columns {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
---

<!-- Apply header and footer to first slide only -->
<!-- _header: "[![INRIA logo](../inria_logo.jpg)](https://www.inria.fr)" -->
<!-- _footer: "[Baptiste Pesquet](https://www.bpesquet.fr)" -->
<!-- headingDivider: 5 -->

# Towards metacognitive agents: integrating confidence in sequential decision-making

<!-- Show pagination, starting with second slide -->
<!-- paginate: true -->

## Confidence in natural cognition

### Decision-making as a sequential process

- Decision-makers need **time** to collect and process informative cues.
- Decinion-making is often modeled as an **accumulation-to-threshold** process [[Gold and Shadlen, 2007](https://www.annualreviews.org/doi/10.1146/annurev.neuro.29.051605.113038)].
- The balance between response time and accuracy (when available) is called the **Speed/Accuracy Trade-off** [[Heitz, 2014](https://www.frontiersin.org/journals/neuroscience/articles/10.3389/fnins.2014.00150/full)].

### Models of sequential decision-making

<div class="columns">
<div>

For binary choices, a popular model is the **Diffision Decision Model** [[Ratcliff and McKoon, 2008](https://direct.mit.edu/neco/article/20/4/873-922/7299)].

![Illustration of the DDM model](images/forstmannSequentialSamplingModels2016_1.png)

*Image credits: [[Forstmann et al., 2016](https://doi.org/10.1146/annurev-psych-122414-033645)]*

</div>
<div>

Multi-alternative decisions are often modeled as a **race** between accumulators for each possible choice.

![Illustration of a race model](images/mamassianVisualConfidence2016_1.png)

*Image credits: [[Mamassian, 2016](https://www.annualreviews.org/doi/10.1146/annurev-vision-111815-114630)]*

</div>
</div>

### Confidence in decision-making

- **Uncertainty** is inherent to all stages of neural computation [[Fleming, 2024](https://doi.org/10.1146/annurev-psych-022423-032425)].
  - It refers to probabilistic representations of information in the brain.
- **Confidence** quantifies the degree of **certainty** associated with a decision.
  - It refers to scalar values derived from those distributions [[Meyniel et al., 2015](https://linkinghub.elsevier.com/retrieve/pii/S0896627315008284)].
- More formally, confidence can be defined as the **probability** that a choice is correct given the evidence [[Pouget et al., 2016](https://www.nature.com/articles/nn.4240)].

### Computing confidence in sequential decision-making models

<div class="columns">
<div>

In **decisional focus models**, confidence is directly indexed by the state of evidence at the time of choice.

![Race model with BoE](images/kepecsNeuralCorrelatesComputation2008_1.png)

*Image credits: [Kepecs et al., 2008](https://www.nature.com/articles/nature07200)*

</div>
<div>

**Post-decisional focus models** posit that evidence accumulation goes on after decision time to account for confidence.

![2DSD model](images/pleskacTwostageDynamicSignal2010_1.png)

*Image credits: [Pleskac and Busemeyer, 2008](https://doi.apa.org/doi/10.1037/a0019737)*

</div>
</div>

### Confidence as a doorway to metacognition

- **Metacognition** is the ability to **monitor** and **regulate** one's cognitive processes [[Flavell, 1979](https://www.semanticscholar.org/paper/Metacognition-and-Cognitive-Monitoring%3A-A-New-Area-Flavell/ee652f0f63ed5b0cfe0af4cb4ea76b2ecf790c8d)].
  - Example: should I study more (or differently) for this exam?
- As part of metacognitive monitoring, confidence judgments may inform the processes of **cognitive control** [[Fleming and Lau, 2014](http://journal.frontiersin.org/article/10.3389/fnhum.2014.00443/abstract)].

### An emerging field: the neuroscience of confidence

- Activity in the **parietal cortex** seems related to evidence accumulation during decision-making.
- **Separate** and perhaps **multiple** brain areas are involved in confidence monitoring and reporting [[Grimaldi et al., 2015](https://linkinghub.elsevier.com/retrieve/pii/S0149763415001025)]:

  - Importance of the prefrontal cortex, more precisely the **ventromedial prefrontal cortex** (vmPFC), in the formation of confidence.
  - Firing rates of many single neurons in the **orbitofrontal cortex** (OFC) of rats match confidence models [[Kepecs et al., 2008](https://www.nature.com/articles/nature07200)].

## Proposed approach

### Agent architecture

<div class="columns">
<div>

Model combining:

- a **decision module** based on an evidence accumulation model;
- a **metacognitive module** in which confidence is used to tune the decision hyperparameters.

Assessed on a classic **perceptual task**: Random Dot Motion discrimination.

</div>
<div>

![Confident agent model](images/pesquetAlexandre2025_1.png)

</div>
</div>

### Preliminary results

- As expected, confidence and decision time are oppositely correlated with dot motion coherence.
- Model is able to implement the SAT.

![First model results](images/pesquetAlexandre2025_2.png)

### Future works

- Refine the hyperparameters tuning process.
- Add different metacognitive strategies.
- Implement model on a human/robot collaborative task.
- ...

## Thanks for your attention!

Any questions?
