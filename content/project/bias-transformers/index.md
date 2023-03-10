---
title: Biases and Stereotypes in StableDiffusion
summary: Automatically create pictures with StableDiffusion from a given point and analyze them with DeepFace. What stereotypes and biases are embedded in StableDiffusion? How far do they reach and what could be done to elimate existing biases?  Example Gender Bias:: What gender will the people in the scene have with the following description "a nurse talks to a doctor"?" 

tags:
  - Machine Learning
  - Natural Language Processing
date: '2023-02-28T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: ''

image:
  caption: Photo by rawpixel on Unsplash
  focal_point: Smart

---
Resources:
- S. Pengpeng, C. Shengli, F. Peihua , SEIR Transmission dynamics model of 2019 nCoV coronavirus with considering the weak infectious ability and changes in latency duration, Preprint, medRxiv, 2020. 

- C. Graf, Ausbreitung von Epidemien, Maturitätsarbeit, Winterthur, 2017


A SEIR model is a approach that is used to describe the spread of infectious diseases. In this project I am programming a simple simulation of such model.

In its most basic form the model looks like this:

```mermaid
graph LR;
  S-->E;
  E-->I;
  I-->R;
```
The different state are Suspectible, Exposed, Infected and Recovered. Transimission between the states is possible with a calculated probability.
