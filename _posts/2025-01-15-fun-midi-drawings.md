---
layout: single
title: "Bezier Curve MIDI tool (a music hackathon thing)"
toc: false
date: 2025-01-17 13:00:00 +0000
categories:  MusicTheory CreativeCoding
---

## MIDI transform
Ableton live 12 came with a bunch of amazing features and one of them was MIDI transform tools. [This one](https://www.ableton.com/en/live-manual/12/midi-tools/). I found some curve based transforms in those pretty cool so I decided to do this as a fun project for the [Music Hack Day India](https://musichackdayindia.github.io/) which was a part of ADC2025. 

## What ended up happening?
Ethan, Azan and I were brainstorming for a while to come up with something like this Max4Live device I'd made a while back (something which makes midi out of bezier curves) - [Max4live scurvee](https://maxforlive.com/library/device/11990/scurveee). We eventually decided to make it a web based tool as our goal for this hackathon submission was to make the creative process of making music accessible to anyone. After a bunch of tinkering we came up with this which we ended up demoing.
![PIC of the thing](/rp_portfolio/assets/images/scurvee_view_browser.jpg)

We had a few prototypes and things evolved a lot (all code be lurking in this [repo](https://github.com/azan-n/scurvee/tree/rp/knobs))
I was pretty satisfied with this design as it was a huge upgrade from the max4live device, given that there were more scale options and I could customise the UI as much as I wanted. The only limitation was that it was a pain to get realtime playback and updation in a web based environment and that's where I knew I'm limited by the immense programming wall that I needed to cross to get to DAW architecture level on the web lol. So we stuck to generating midi and importing it in to a DAW/midi player. I wish I could show you how these curves sounded but I guess you could try it out yourself once I finish making a better version of this and host it (I hope work gets less hectic :( and I could do more fun stuff)).


## Examples
Look at this curve
![curve raw](/rp_portfolio/assets/images/curve_1.jpg)
this is the curve before I generated it's midi.

![curve midi](/rp_portfolio/assets/images/midi_curve_1.jpg)

The midi sound really interesting given I chose this scale haha

![scale options](/rp_portfolio/assets/images/super_scale.jpg)

## The outcome?
We ended up getting a special mention ;) and although this was all we could do within less than 7 hours, I am convinced that this could become a really fun tool for musicians to play around with. I'm gonna make more M4L midi devices like this. Shoutout to my teammates who helped get this across. 
[Ethan's socials (he works at this music tech company called pitchinnovations btw)](https://www.instagram.com/ethan.dj0seph/) and [Azan](https://www.instagram.com/azan.n0/) is one of the founding members of [Cryptlex](https://cryptlex.com/). Amazing people fo sho.


