---
layout:  
title: "Generative MIDI"  
toc: false  
date: 2024-06-07 13:00:00 +0000  
categories: MusicTech
---

## Motivation

During the rise of AI music tools such as [Suno](https://suno.ai/) and [Udio](https://www.udio.io/), I became fascinated with their compelling music generations. However, I felt there was something off about the results. While undeniably creative, the audio artifacts were more noticeable, which is a common limitation in AI-generated music that heavily focuses on audio synthesis. After discussing with peers, we agreed that the focus should shift towards MIDI, which offers a more detailed representation of musical ideas.

This led me to explore MIDI generation with large language models (LLMs). Fortunately, I discovered [MidiTok](https://miditok.readthedocs.io/en/latest/), a MIDI tokenizer that aligned perfectly with my goal. With the essential pieces in place, all that remained was to integrate them into my own project.

## Process

After spending some time learning how tokenization works, and delving into concepts like transformers, sequence-to-sequence (seq2seq) models, and more, I decided to implement a solution. I trained the model using a collection of my own compositions (I produce and compose video game music) along with datasets like [VGMMidi](https://github.com/lucasnfe/vgmidi) and [JazzNet](https://github.com/tosiron/jazznet).

I experimented with various models, tokenization approaches, and training configurations, ultimately settling on the Mistral transformer model, as provided in the default example. I combined the three MIDI datasets (my dataset being smaller, but adding a personal touch) and wrote this code: [8 Bar Loop Generator](https://github.com/RP335/8_bar_loop_generator). 

For training, I used AWS EC2, as I preferred not to invest in Google Colab for this short-term task. After some experimentation, I achieved satisfactory results, which can be found in the linked demo.

## Conclusion

MIDI generation is still far from perfect. The output often feels overly quantized and lacks the human touch. I haven't yet found a better way to tokenize the MIDI data to produce more natural results, but there may be configurations I'm missing. Despite these limitations, I'm pleased with the experiment and excited to explore further tweaking, including combining more datasets. The future of generative music holds great potential.

