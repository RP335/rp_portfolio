---
layout: single
title: "A Fun TouchDesigner experiment with Open Sound Control"
toc: false
date: 2021-05-7 13:00:00 +0000
categories:  MusicTheory CreativeCoding
---

## Discovering TouchDesigner

I've constantly been yearning to do my own visuals for my music. In the past, I dabbled with Blender to create animations. However, I did find it a task to make them react to MIDI. 

Fast forward to now, I discovered this node-based software called TouchDesigner. I was intimidated by the learning curve. I watched, learned through small tutorials, and read the documentation until I got somewhere. The idea of drawing with sound fascinated me, and I could do that through TD.

---

## What's the plan?

Well, I didn't have any concrete idea at first as to how I'd go about this, as the date for a live show by our band was nearing, and we wanted to make something interactive speedy. We could play around with something on stage using our hands or a stick. Finally, we decided to:

- Make a projected paintable wall with a LIDAR sensor.
- Paint random strokes that would result in some incredible visuals.
- Use those visuals to drive sound.

---

## How did we go about it?

After a bunch of scavenging-for-tutorials sessions on YouTube (I'm a beginner in TD), I came across this tutorial, which made kaleidoscopic visuals using strokes across a screen. I spent a good chunk of time watching this until I got a basic setup and then decided to brainstorm how I'd send the drawing data as MIDI.

### Challenges and Solutions:

- **Understanding MIDIOut Chop**: It seemed hard to understand, so I opted to use OSC (Open Sound Control) instead.
- **OSC Benefits**:
  - Send data to my friend's laptop connected to the same network.
  - Leverage his better collection of VSTs and synths compared to my stock Ableton setup.

The node network looked something like this:
![Node Network Overview](/rp_portfolio/assets/images/node_network_overview.jpg)

The RGB values were manipulated to drive sound, as shown here:
![RGB Values](/rp_portfolio/assets/images/rgb_values.jpg)

I used the OSCOut DAT to send messages:
![OSCOut DAT](/rp_portfolio/assets/images/osc_out_dat.jpg)

---

Eventually, the rest of my work involved writing some Python code that would take these values and create some cool sounds. The only thing that came to my mind at the time was:

- The scale was stacked fifths up until a Major 13th Chord.
- The scale kept changing through an offset, which was also triggered through an LFO in TouchDesigner.

I'm gonna attach the code at the very end. Meanwhile, enjoy these chords!

<iframe width="560" height="315" src="https://www.youtube.com/embed/_jFhIcUEjkA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

---

## What happened eventually?

As I write this, I'm getting too excited to perform this next week at my home (The LIDAR sensor hasn't come yet). If I'm successfully able to pull this off:

- I'll create an interactive installation for the next live show.
- I'll collaborate with some cool cats from Bangalore and put together a fun trio.

Let's hope for the best, fingers crossed!



### cOdE


```python
from pythonosc import dispatcher, osc_server
import mido
import time
import random

midi_out = mido.open_output('IAC Driver Bus 1')

base_midi_notes = [40, 47, 54, 61, 68, 75, 82]
current_offset = 0  # Initialize offset

def osc_key_switch_handler(address, *args):
    global current_offset
    print(f"Received OSC key switch at address - {address} with args: {args}")

    if len(args) == 1 and isinstance(args[0], int):
        current_offset = args[0]
        print(f"Updated offset: {current_offset}")
    else:
        print(f"Format invalid (keyswitch): {args}")


def osc_to_midi_handler(address, *args):
    global current_offset
    print(f"Received OSC message at {address} with arguments: {args}")

    if len(args) == 1 and isinstance(args[0], (int, float)):
        value = int(args[0])
        # print(value)
    else:
        print(f"Unhandled OSC data format: {args}")
        return

    if value < 40:
        print(f"OSC value {value} is below 40, no note will be played.")
        return

    midi_notes = [(note + current_offset) for note in base_midi_notes]
    print(f"Midi notes after offset adjustment: {midi_notes}")

    midi_note = midi_notes[value % len(midi_notes)]
    print(f"Mapped OSC value {value} to MIDI note {midi_note}")

    note_on = mido.Message('note_on', note=midi_note, velocity=64, channel=0)
    midi_out.send(note_on)
    print(f"Sent MIDI Note On: {note_on}")

    # time.sleep(1.4)
    time.sleep(0.4)

    note_off = mido.Message('note_off', note=midi_note, velocity=64, channel=0)
    # note_off = mido.Message('note_onn', note=midi_note, velocity=127, channel=1)
    midi_out.send(note_off)
    print(f"Sent MIDI Note Off: {note_off}")

dispatcher = dispatcher.Dispatcher()
dispatcher.map("/from_TD", osc_to_midi_handler)
dispatcher.map("/from_TD_Key_switch", osc_key_switch_handler)

ip = "127.0.0.1"
port = 10000

server = osc_server.ThreadingOSCUDPServer((ip, port), dispatcher)
print(f"OSC server running on {ip}:{port}")

try:
    server.serve_forever()
except KeyboardInterrupt:
    print("Closing OSC server.")
    server.shutdown()
    midi_out.close()

```



