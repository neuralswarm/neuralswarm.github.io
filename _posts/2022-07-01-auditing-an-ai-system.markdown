---
layout: post
category: Learn
title: Auditing an AI System
description: A new framework for auditing an AI System.
image: assets/posts/auditing-an-ai-system/splash.jpg
author: tlyleung
---

<!-- Sell companies on benefits of an AI Audit -->

Machine learning systems are more complex than software systems. Auditing a machine learning system requires a significant shift in thinking. While software engineering principles have predominantly matured, the rapid evolution of machine learning means that machine learning systems can look very different from one company to the next. Earlier systems may be missing some of the more recent but essential developments in machine learning, such as model monitoring, continual training and responsible AI. A Machine Learning system that is deployed and put in production, needs to be reliable, scalable, maintainable and adaptable[^huyen22].

## Why Do An AI Audit?

Audits are independent examinations used to satisfy regulatory requirements. Beyond that, an audit can have other uses too. For example, audits can be used to identify and mitigate risks either internally within the company or externally by an acquirer performing due diligence on a target. Another overlooked benefit of an audit is to propagate industry-accepted best practices.

## Machine Learning System Risks

<!-- New ML risks you didn't know about -->

A machine learning system carries its own specific set of risks in addition to all the risks of a software system. Common software audit frameworks, such as COBIT 2019 (a general framework for IT management and governance) and ISO 27001 (a framework emphasising information security), are insufficient.

In typical software systems, code is separate from data. This means that, regardless of input data, the software system itself doesn't change. Machine Learning systems, however, are a function of code *and* data *and* the parameters used to combine them. Changing any of these will result in different model weights and, consequently, a different model. It is impossible to decouple them. For that reason, risk mitigating techniques easily implementable in software systems become vastly more complicated in machine learning systems.

Take version control, for example. In a software system, only source code and package dependencies have to be placed under version control. In Machine Learning systems, each component needs to be placed under version control systems that are often separate. Source code will use Git; data will use [DVC](https://dvc.org/);  experiment parameters and trained models will use [Weights & Biases](https://wandb.ai/).


## Stale Data Produces Stale Models

Data, being an integral part of the trained model, also comes with unique challenges. While issues surrounding data quality (such as availability, completeness, consistency, and correctness) are a concern of any software system, low-quality data only affects the immediate output of such a system. In a Machine Learning system, however, bad or untimely data can poison all future outputs of the system.

Bad data often means data that is corrupt or missing. In Machine Learning systems, however, even input data that is different from the data used to train the model is considered bad. This problem is called data drift, which can be divided further into feature drift and label drift. Model monitoring is an essential part of the deployment process required to combat data drifts.

The timeliness dependency means that even good data is rendered useless after some time. This expiry date on the data (and, by extension, the model trained on that data) means that system needs continual retraining on fresh data.

## Machine Learning Industry Best Practices

<!-- Best practices you didn't know about -->

There are several ways to disseminate best practices in the software industry. Industry experts can move around companies taking best practices with them, FAANG companies can spread them through engineering blog posts and tech talks, or they can be gleaned from reading open source and vendor documentation. Performing an AI Audit can be an excellent alternative to these. Spreading best practices is particularly important in Machine Learning because only recently have best practices become codified and consolidated.

Here are a few examples of more recent best practices:

- Model monitoring and continual learning
- Generating fair, compact, robust and explainable models
- Testing models in a robust and reproducible manner, instead of only relying on the loss function
- Tracking data lineage
- Using the same data pipeline for train/test and batch/streaming data

## Neural Swarm AI Audit Framework

<!-- Present new framework -->

Neural Swarm has created a new audit framework for AI Systems (see Table 1). It is intended to supplement the controls and processes in a software audit.

<style>table .description { display: none; } table .controls { text-align: right; }</style>
<table>
  <thead>
    <tr>
      <th class="shortcode">Shortcode</th>
      <th class="category">Category</th>
      <th class="name">Objective</th>
      <th class="description">Description</th>
      <th class="controls">Controls</th>
    </tr>
  </thead>
  <tbody>
    <tr class="hr">
      <th class="shortcode">AI-VAL-1</th>
      <td class="category">Value</td>
      <td class="name">System Feasibility</td>
      <td class="description">Ensure that the AI system is feasible</td>
      <td class="controls">3</td>
    </tr>
    <tr>
      <th class="shortcode">AI-VAL-2</th>
      <td class="category">Value</td>
      <td class="name">System Requirements</td>
      <td class="description">Determine constraints of the AI system</td>
      <td class="controls">7</td>
    </tr>
    <tr class="hr">
      <th class="shortcode">AI-DAT-1</th>
      <td class="category">Data</td>
      <td class="name">Data Collection</td>
      <td class="description">Ensure collected data is suitable for model development</td>
      <td class="controls">7</td>
    </tr>
    <tr>
      <th class="shortcode">AI-DAT-2</th>
      <td class="category">Data</td>
      <td class="name">Data Preparation</td>
      <td class="description">Prepare collected data for preprocessing</td>
      <td class="controls">5</td>
    </tr>
    <tr>
      <th class="shortcode">AI-DAT-3</th>
      <td class="category">Data</td>
      <td class="name">Data Splitting</td>
      <td class="description">Ensure data is split correctly</td>
      <td class="controls">3</td>
    </tr>
    <tr>
      <th class="shortcode">AI-DAT-4</th>
      <td class="category">Data</td>
      <td class="name">Data Preprocessing</td>
      <td class="description">Enforce data preprocessing best practices</td>
      <td class="controls">6</td>
    </tr>
    <tr>
      <th class="shortcode">AI-DAT-5</th>
      <td class="category">Data</td>
      <td class="name">Data Pipeline Testing</td>
      <td class="description">Ensure that data pipeline conforms to its design</td>
      <td class="controls">2</td>
    </tr>
    <tr class="hr">
      <th class="shortcode">AI-MOD-1</th>
      <td class="category">Model</td>
      <td class="name">Model Development</td>
      <td class="description">Use suitable features and models</td>
      <td class="controls">3</td>
    </tr>
    <tr>
      <th class="shortcode">AI-MOD-2</th>
      <td class="category">Model</td>
      <td class="name">Model Training</td>
      <td class="description">Increase training speed and stability</td>
      <td class="controls">4</td>
    </tr>
    <tr>
      <th class="shortcode">AI-MOD-3</th>
      <td class="category">Model</td>
      <td class="name">Model Evaluation</td>
      <td class="description">Evaluate model performance</td>
      <td class="controls">5</td>
    </tr>
    <tr>
      <th class="shortcode">AI-MOD-4</th>
      <td class="category">Model</td>
      <td class="name">Model Testing</td>
      <td class="description">Ensure that model conforms to its design</td>
      <td class="controls">5</td>
    </tr>
    <tr class="hr">
      <th class="shortcode">AI-DEP-1</th>
      <td class="category">Deployment</td>
      <td class="name">Operations</td>
      <td class="description">Enforce MLOps best practices</td>
      <td class="controls">6</td>
    </tr>
    <tr>
      <th class="shortcode">AI-DEP-2</th>
      <td class="category">Deployment</td>
      <td class="name">Monitoring and Continual Learning</td>
      <td class="description">Monitor and correct models for skews, shifts and drifts </td>
      <td class="controls">6</td>
    </tr>
    <tr class="hr">
      <th class="shortcode">AI-RES-1</th>
      <td class="category">Responsible AI</td>
      <td class="name">Model Fairness</td>
      <td class="description">Produce fair models</td>
      <td class="controls">2</td>
    </tr>
    <tr>
      <th class="shortcode">AI-RES-2</th>
      <td class="category">Responsible AI</td>
      <td class="name">Model Explainability</td>
      <td class="description">Produce explainable models</td>
      <td class="controls">4</td>
    </tr>
    <tr>
      <th class="shortcode">AI-RES-3</th>
      <td class="category">Responsible AI</td>
      <td class="name">Model Compactness</td>
      <td class="description">Produce compact model</td>
      <td class="controls">1</td>
    </tr>
    <tr>
      <th class="shortcode">AI-RES-4</th>
      <td class="category">Responsible AI</td>
      <td class="name">Model Robustness</td>
      <td class="description">Produce robust models</td>
      <td class="controls">1</td>
    </tr>
    <tr class="hr">
      <th class="shortcode">AI-ENG-1</th>
      <td class="category">Software Engineering</td>
      <td class="name">Source Code</td>
      <td class="description">Produce good quality source code</td>
      <td class="controls">6</td>
    </tr>
    <tr>
      <th class="shortcode">AI-ENG-2</th>
      <td class="category">Software Engineering</td>
      <td class="name">Documentation</td>
      <td class="description">Facilitate knowledge sharing and transfer</td>
      <td class="controls">2</td>
    </tr>
    <tr>
      <th class="shortcode">AI-ENG-3</th>
      <td class="category">Software Engineering</td>
      <td class="name">Version Control</td>
      <td class="description">Ensure that modifications are tracked and reproducible</td>
      <td class="controls">5</td>
    </tr>
    <tr>
      <th class="shortcode">AI-ENG-4</th>
      <td class="category">Software Engineering</td>
      <td class="name">Testing</td>
      <td class="description">Ensure that software conforms to its design</td>
      <td class="controls">2</td>
    </tr>
  </tbody>
  <caption>Table 1: Neural Swarm AI Audit Framework</caption>
</table>

The Neural Swarm Audit Framework consists of 87 controls spanning six categories and 21 groups. The six categories comprise of four phases from the Neural Swarm project workflow (Data, Value, Model and Deployment) as well as two supplementary categories (Responsible AI and Software Engineering).

Here is a brief description of the six categories:

- **Value:** Determine that AI adds business value and that the AI system is feasible with clear requirements.

- **Data:** Ensure that data is suitably collected and that the data pipeline is created and tested correctly.

- **Model:** Check that suitable features and models are used, that training is optimised and that the model is correctly evaluated and tested.

- **Deployment:** Enforce MLOps best practices, including model monitoring and continual training.

- **Responsible AI:** Verify that the model is fair, explainable, compact and robust.

- **Software Engineering:** Certify that the system follows software engineering best practices around source code, documentation, version control and testing.

## What does an AI Audit look like?

<!-- Methodology -->

Auditors look for conformity by collecting evidence. In a Machine Learning audit, the evidence comes primarily from reading documentation such as design documents and interviewing key stakeholders. In some cases, auditors can review source code and run certain tests to evaluate model fairness and robustness.

Different stakeholders are interviewed for the six categories:

- **Value:** Interview with the *Machine Learning Product Manager* to discuss developing the product roadmap, and mapping user needs to product features.

- **Data:** Interview with the *Data Engineer* to discuss building data pipelines for data collection and transformation.

- **Model:** Interview with the *Machine Learning Engineer* to discuss designing, building and tuning the models.

- **Deployment:** Interview with the *MLOps Engineer* to discuss deploying the system and monitoring concept and data drifts.

- **Responsible AI:** Interview with the *Machine Learning Product Manager* to discuss how the model addresses Responsible AI concepts.

- **Software Engineering:** Interview with the *MLOps Engineer* to discuss software engineering best practices around source code, documentation, version control and testing.

The audit result is usually written up in a 15–20 page report. The majority of the report is the *Recommendations* section. For each group with minor or major non-conformities, a series of recommendations will be made along with a description of the controls and observations. Depending on the complexity and number of models, the whole process can take around two weeks.


[^breck17]: Breck, E., Cai, S., Nielsen, E., Salib, M., & Sculley, D. (2017). The ML Test Score: A Rubric for ML Production Readiness and Technical Debt Reduction. *Proceedings of IEEE Big Data.*

[^huyen22]: Huyen, C. (2022). *Lecture 1: Understanding ML Production [Presentation slides].* Unpublished manuscript, CS329S: Machine Learning Systems Design, Stanford University.
