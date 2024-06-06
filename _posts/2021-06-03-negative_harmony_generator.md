---
layout: single
title: "Exploring Negative Harmony with MuseScore"
toc: false
date: 2021-05-7 13:00:00 +0000
categories:  MusicTheory MuseScore QML
---

## Introduction

Back in the day I'd see a lot of videos about negative harmony especially afater it got too much hype during the rise in popularity of Jacob Coller and being a music nerd myself, I found it fascinating. But I didn't quite understand how I'd use this concept in my own compositions or do this real quick without having to draw the cirlce of fifths and flip notes. So insticntively, the next thing I planned on doing was automating this whole process.
In this post, I'll dive into my explorations of negative harmony in music theory and how I developed a method to transform scores using this concept. This journey began in May 2021 and led me to the create a plugin for MuseScore, enabling composers to use negative harmony as a compositional tool.

## Understanding Negative Harmony

Negative harmony is a theoretical concept where musical notes are mirrored around a central axis, creating a harmonically inverse piece. This exploration involved deep dives into music theory, understanding the principles of negative harmony, and applying these principles to real-world compositions.

## Developing the Negative Harmony Generator Plugin

To bring this concept to life, I created a plugin for MuseScore using QML and the MuseScore Plugin API. The plugin allows users to generate the negative harmony of a selected or entire score with a few clicks.

### Tech Stack

- **MuseScore Plugin API:** For integrating the plugin with MuseScore.
- **QML:** For developing the user interface and handling the logic of the plugin.
- **JavaScript:** For scripting the transformation algorithms.

### Key Features

- **Scale Selection:** Users can select the scale for generating negative harmony.
- **Transformation:** The plugin transforms the selected notes or the entire score into their negative harmony equivalents.

Here is the link to the [GitHub repository](https://github.com/RP335/NegativeHarmonyGenerator/blob/main/negativeharmonygenerator.qml) for the plugin.

<!-- ![Score Before Transformation](/assets/images/before_transformation_image.png) -->
<img src="{{site.baseurl | prepend: site.url}}/assets/before_transformation_image.png" alt="before_score" />
*Score before transformation*

<!-- ![Score After Transformation](/assets/images/after_transformation_image.png) -->
<img src="{{site.baseurl | prepend: site.url}}/assets/after_transformation_image.png" alt="after_score" />
*Score after transformation*

## Using the Plugin

To use this plugin, refer to the [MuseScore Plugin Documentation](https://musescore.github.io/MuseScore_PluginAPI_Docs/plugins/html/). This guide will help you install and utilize the plugin effectively.

## Further Explorations

While the current plugin provides a basic transformation, the concept of algorithmic negative harmony generation still has room for improvement. One area worth exploring is leveraging large language models (LLMs) to train on musical data for more human-like compositional translations. This approach could address the challenges of creating organic-sounding melodies that follow the leading melody's pattern.

### Future Plans

- **Enhancing the Algorithm:** Improving the algorithm to produce more organic-sounding results.
- **UI for MIDI File Uploading:** Developing a user interface for uploading MIDI files and translating them using the plugin.
- **Exploring QML and MuseScore:** This project has been a great opportunity to delve into QML and MuseScore, exploring their potential for composition, transcription, and more.

## Conclusion

The negative harmony generator plugin is just the beginning of exploring the fascinating world of music theory and its applications in modern software tools. This project has opened up many avenues for further exploration and development, making it a worthy undertaking for anyone interested in music and technology.

Stay tuned for more updates and explorations in music and software engineering!

---

This post is part of my broader explorations in music, tech, and software engineering. Stay tuned for more insights and projects!
