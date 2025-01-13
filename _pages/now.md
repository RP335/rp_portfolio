---
title: Now
layout: archive
collection: now
permalink: /now/
author_profile: false
---

> To replace the social media updates I keep this page inspired by [Derek Sivers](http://sivers.org/) and the [/now page movement](https://nownownow.com/about).

## Update from June 5th, 2024

### 💻 Work/Study

- Currently working as a **Software Engineer**.
- Focusing on **signal processing research** and **music technology research**.
- Developing **pendulum wave polyrhythm generators** as side projects.
- Actively **transcribing** Herbie Hancock's works and jamming on the piano.

### 🎵 Listening

- Into **jazz**, **UK garage**, and **R&B**.
- Frequently listening to Herbie Hancock and other jazz legends.


### 🕹️ Playing

- I'm currently playing Tears of the Kingdom way too much (an unhealthy amount hehe cause it's just a phenomenal game, I have no words to describe)
- Others include MarioKart, SmashBros, KatamariDamacy, MetriodPrime... the list goes on 

### 🔭 Looking forward to...

- Building a keen interest in **signal processing research** and **music technology research**.
- Exploring different methods and research areas to make composition transcription easier.

<hr>
# Old updates

{% assign now_pages = site.now |sort:'date' | reverse %}
{%- for post in now_pages -%}
{% include archive-single.html %}
{%- endfor -%}
