---
title: "DECsing"
date: 2023-09-04T16:44:35-04:00
draft: false
archived: true
personal: true
header_image: /images/projects/decsing/dectalk.jpg
description: "Translates MIDI into pitch, phoneme, and tone information for DECtalk."
tags: ["java", "hackathon/gamejam", "sound"]
source: "https://github.com/SPIGS/HackIO-2018"
---

## About

DECsing is a Java program that reads the track information from [MIDI](https://en.wikipedia.org/wiki/MIDI) music files and translates it into pitch, phoneme, and tone information so it can be sung by the [DECtalk](https://en.wikipedia.org/wiki/DECtalk) text-to-speech program.

This project was made in the Fall of 2018 as part of my first hackathon, [HackOHI/O](https://hack.osu.edu/), at university with a friend. HackOHI/O, is a 24 hour hackathon and it is encouraged to participate in one of the corporate-sponsored challenges, but being new students and it being our first time participating in a hackathon, we decided to come up with our own project during the competition. We wanted to do something unique and humorous. Our idea for DECsing was inspired by Moonbase Alpha text-to-speech [music videos](https://www.youtube.com/watch?v=CNPKXfb3rws). We figured there should be a way to automate the inputs for Moonbase Alpha to more efficiently sing songs while working on the moon. 

In the 24 hours of the competition, we managed to get DECsing half-working. It was able to handle some simple MIDI files (only one or two tracks so think a solo pianist), and correctly converted pitch. However, it ran into issues with more complex tracks (multiple tracks so think a whole band), and would produce tracks that were too high of tempo. In addition, DECtalk has a hard limit on the length of an input string which we didn't account for. This resulted in some outputs devolve into the text-to-speech utter each individual "bracket", "brace", and number used in the formatting of the input string.

Below is an example of a "successful" output of a snippet of *Fur Elise*:

{{< audio src="/audio/projects/decsing/input.mp3" caption="Input MIDI file">}}

{{< audio src="/audio/projects/decsing/generated.mp3" caption="Output from DECsing. Notice that the tempo has increased.">}}

## Postmortem

> This postmortem was written in August of 2023.

Looking back on this project, after experience working in several other hackathons, taking several project classes, and working in industry, I can say my friend and I could probably produce something more complete in the same amount of time. Though, I am proud of what did manage to accomplish in such a short amount of time with essentially zero planning.  

## Acknowledgements and Further Reading

- [MIDI Spec](https://www.midi.org/specifications): the MIDI specification
  - [A more condensed verison](https://www.cs.cmu.edu/~music/cmsip/readings/davids-midi-spec.htm)
- [Phonemes](https://dectalk.github.io/dectalk/idh_ref_3_phonemic_symbols.htm): DECtalk phonemes for various languages
- [Cover photo](https://en.wikipedia.org/wiki/DECtalk#/media/File:DECtalk_DCT01_and_Tink.jpg): from the Wikipedia article on DECtalk (I do not own a cat)