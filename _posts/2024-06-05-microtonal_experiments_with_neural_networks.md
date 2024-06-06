---
layout: single
title: "The Microtonal Experiment"
toc: false
date: 2024-06-5 13:00:00 +0000
categories: DeepLearning MusicTheory AudioProcessing
---


## Inspiration

Shower thoughts: I recently heard this [piece](https://youtu.be/FO9ihziyL5c?feature=shared) but it felt much better than the original and that's what a lot of others I know personally said. Maybe 31 EDO is something which humans naturally gravitate to? 
While most certainly a computer can't feel the same emotions as us while hearing perfectly locked-in intervals, I think it could identify them. If I did years of ear training maybe, I'd be able to tell apart 31 EDO from 19 EDO and so on, but what I want to see is if a computer could figure that out real quick.

## EDO and its Definition

EDO (what is it ?): An EDO, or Equal Division of the Octave, is a tuning system that divides the octave into a specific number of equally spaced steps. Traditional Western music uses 12-EDO, but microtonal music explores other divisions such as 19-EDO, 31-EDO, and beyond. These alternative tunings offer unique intervals and harmonies not found in standard tuning. Refer to the [Xenharmonic Wiki](https://en.xen.wiki/w/EDO).

## Approach

If you'd like to see the full history of how my code developed into this, do refer [Github](https://github.com/RP335/microtonal_experiments).
<br>
To summarize, I started by reading up about methods to classify stuff and came across a big explanation of neural networks and went down the rabbit hole of exploring these things.
<br>

I looked at [this](https://arxiv.org/abs/2405.16000) for reference to gain some insights as to how I could analyze pitched audio. 
Seems like a decent start for implementing something of this sort and I felt that this method would prove to be more accurate than a regular RandomForestClassifier or the same thing tweaked and fine tuned. So I went with Leveraging Convolutional Neural Networks (CNNs) combined with Time-Distributed Networks (TDNs) and Long Short-Term Memory (LSTM) networks. This approach aims to capture both the spatial and temporal hierarchies in the audio data. I trained this model for up to 200 epochs to ensure it had ample opportunity to learn the patterns in the data.
<br>

I then tried a RandomForestClassifier, a more traditional machine learning method, to benchmark its performance against the deep learning model.

<br>
To improve the performance of the Random Forest, I fine-tuned its hyperparameters using grid search, optimizing settings like the number of trees, maximum depth, and minimum samples split.


<br>
So I began, and the first thing I did was generate the dataset as I couldn't find a dataset which had the following
- triads in various edos
- each triad can be in random pitches (not just 12 tet keys for the root notes)

To do this task, I adopted [Xenharmlib](https://xenharmlib.readthedocs.io/en/latest/), a music theory library in python for exploration of microtonality. Thank god for the existence ot this, otherwise I'd have to break my head trying to generate the dataset itself. Enough ranting, let's continue.
<br>
Since it was triads, I needed to generate edos >= 5 and I chose 11, 15, 19, 31, 53 and 24 as the options. Cycling through them I got a full dataset of chords. Here's the code for that.



### Code Snippet for Generating Microtonal Files

```python
import os
from xenharmlib import EDOTuning, export, UpDownNotation, play
import numpy as np

output_dir = 'microtonal_audio_files'
os.makedirs(output_dir, exist_ok=True)

def generate_and_export_chords(edo,  duration=2.0, sample_rate=22050):
    edoTuning = EDOTuning(edo)
    root = edoTuning.pitch(0)
    third = edoTuning.pitch(int(4*edo/12))
    fifth = edoTuning.pitch(int(7*edo/12))
    for i in range(40):
        triad = edoTuning.pitch_scale([root, third, fifth]).transpose((np.random.randint(45,65))*edo/12)
        filename = os.path.join(output_dir, f'microtonal_chord_{edo}edo_{i+1}.wav')
        export.audio.export_wav(filename, triad, duration=duration, play_as_chord=True, sample_rate=sample_rate)
```

### Conclusion
Given my exploration of this topic, I think that CNNs with TDNs gave the best accuracy (70.83%), which is quite decent for such a complex task. While this isn't perfect, it's a significant improvement over random guessing. There's still much to explore, and I believe that better feature extraction methods and further tuning could push these results even higher.

This experiment has shown me that AI can indeed aid me in my microtonal explorations. Let me see what I can do next with microtones and AI.
For further details on the implementation and code, you can refer to my Colab Notebook in the Github link above.

And with that, I'm off to bed. Until next time, happy experimenting with microtonal music!

