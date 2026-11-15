---
marp: true
math: true  # Use default Marp engin for math rendering
headingDivider: 3
paginate: true
# https://github.com/orgs/marp-team/discussions/192#discussioncomment-1517399
style: |
  .columns {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }
title: "Confidence as hyperparameter tuning for sequential decision-making"
date: 2024-10-16T10:13:06+01:00
draft: false
showToc: true
tags:
- decision-making
- confidence
---

<!-- Put each of the following lines into an HTML comment to display the title slide -->

<!-- Apply header and footer to first slide only
_header: "[![IMN logo](../../../static/images/imn_logo.png)](https://ensc.bordeaux-inp.fr) [![INRIA logo](../../../static/images/inria_logo.jpg)](https://www.inria.fr) [![ENSC logo](../../../static/images/ENSC_2022.jpg)](https://ensc.bordeaux-inp.fr)" 
_footer: "[Baptiste Pesquet](https://www.bpesquet.fr)" 
headingDivider: 3 

<style scoped>
  img {
    padding-right: 40px
  }
</style>

# Confidence as hyperparameter tuning for sequential decision-making

Show pagination, starting with second slide 
paginate: true  -->

## Metacognition

[![Metacognition diagram](../confidence/images/metacognition_diagram.png)](../confidence/#metacognition)

## Sequential decision-making

- Speed/Accuracy Tradeoff.
- Canonical model: integration of noisy information until a threshold is reached.
- Many refinements: multi-alternative choice, impact of learning, change of mind, etc.

[![](../decision-making/images/eam_rdk.png)](../decision-making/#sequential-sampling)

## Confidence for decision-making

- Quantifies the degree of certainty associated with a decision.
- Canonical model: post-decisional computation based on accumulated info.
- Can be used to alter the subsequent decisions.

<div class="columns">
<div>

![Balance of Evidence example](../confidence/images/BoE.png)

</div>
<div>

![2DSD](../confidence/images/2DSD.png)

</div>
</div>

## Proposed architecture: confidence as hyperparameter tuning for sequential decision-making

![Architecture of a confidence-regulated AI](images/metacognitive_agent.png)

## Current & next steps

- Article for [ESANN 2025](https://www.esann.org/).
- Detailed review of confidence for decision-making (future PhD chapter).
- First experiment on very basic task.

## Questions?
