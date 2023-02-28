---
title: Simple SEIR model 
summary: A simple seir model written in python
tags:
  - Simulation
date: '2023-02-28T00:00:00Z'

# Optional external URL for project (replaces project detail page).
external_link: ''

image:
  caption: Photo by rawpixel on Unsplash
  focal_point: Smart

links:
  - icon: twitter
    icon_pack: fab
    name: Follow
    url: https://twitter.com/georgecushen
url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: example
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
