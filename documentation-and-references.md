---
website: https://comp.anu.edu.au/courses/comp4350/assessments/lens-performance/
name: Shiv Suresh
uid: u7493339
title: Fragments, in E Minor
---

# LENS Performance Documentation


## Technical Description
### Ambient baseline (Pure Data)

My performance begins with 6 harmonised base notes, playing at random via a patch I made in PureData. The patch is made of 6 of the following subpatches, for each of the 6 harmonised notes:

![Alt text](/src/note.png)

Each note generator (such as note1, note2, etc.) operates on a timed system controlled by a metro 10000, which activates every 10 seconds but only when enabled by a master toggle and a randomisation mechanism. The sound is produced using a phasor~ oscillator whose pitch is modulated by a low-frequency oscillator (LFO), creating dynamic variation. Timing is further randomized through two mechanisms: one generates a scheduling interval between 10,000 and 40,000 milliseconds using random 30000 + 10000, while the other sets a trigger delay of approximately 2 seconds with ±700 milliseconds of variability. To ensure smooth amplitude transitions, the envelope of each note is shaped by line objects, applying a fade-in and fade-out over 3 milliseconds

The patch is controlled by the following:

![Alt text](/src/control.png)

-	The master toggle (labeled "Master Toggle for Ambeint Base") is a button (tgl) that sends a bang to s toggle. This bang is received by each note section’s r toggle, enabling or disabling the corresponding metro.

-	The randomise button sends a bang to s random, which all note sections listen to via r random. This triggers new random timing values, refreshing metro intervals and delays.

Pitches are assigned using:

![Alt text](/src/pitch.png)

Each note generator receives one of these values via r noteX, ensuring that each oscillator has a unique pitch, spread across a range suitable for a bassline. These notes harmonise together using the e minor pentatonic scale.

In summary, each note subpatch plays a filtered, slowly modulated sine wave tone at a randomly scheduled interval, triggered by the master toggle. The randomise control refreshes all time parameters, making each run unique. The system combines randomness and pitch modulation to create the first component of my performance 

### Rhythmic baseline (Strudel.cc)
Using studel.cc, my rhythmic bassline is made by sequencing two alternating note patterns: one ascending ([0, 2, 4, 7, 9, 7, 4, 2]) and one descending ([0, 3, 5, 8, 7, 5, 3, 0]). These sequences are mapped onto the E minor pentatonic scale as well, providing a musically consonant and tonally rich foundation. The .segment(8) function ensures that the full sequence spans eight rhythmic subdivisions, creating a repeating, metrically grounded phrase. With .slow(1), each note is played at a steady pace, forming a consistent pulse. The use of the sine waveform adds a smooth, round tone ideal for a bassline, while .gain(0.7) and .legato(0.9) help ensure each note flows seamlessly into the next without sharp breaks.

To enhance the rhythmic feel and sonic texture, the patch introduces subtle modulation through Perlin noise functions. The low-pass filter (.lpf) and high-pass filter (.hpf) evolve gradually, shaping the frequency spectrum over time and giving the bassline a dynamic, breathing quality. The panning effect (.pan) moves the sound slowly across the stereo field, creating a spatial rhythm in addition to the temporal one. A touch of delay (.delay(0.15)) and reverb (.room(1.0)) further reinforce the rhythmic flow by layering slight echoes behind each note. Lastly, .degradeBy(0.1) adds mild bit reduction, lending the bassline a slightly gritty, lo-fi character that contributes to its rhythmic identity.

### Rhythmic baseline 2 (Strudel.cc)

The next stage of my performance is another rhythmic backing made in strudel.cc. The patch generates a complex and evolving rhythmic texture by layering four distinct musical voices. The first voice alternates between e1 and e2 using frequency modulation synthesis (.fm("7")) for a harmonically rich tone. Its low-pass filter, modulated by Perlin noise, gradually changes the timbre over time, while .fast(2) speeds up its rhythmic articulation. Reverb (.room(0.5)), a short attack envelope (.lpenv(-3)), and .lpa(.2) smooth out the dynamic transitions, contributing to a percussive yet fluid rhythmic feel. The second voice, built from a random selection of pitches within the E minor pentatonic scale, runs at a slower rate (.slow(4)) with bit degradation (.degradeBy(0.4)) and a soft piano timbre, adding syncopated melodic motion beneath the primary rhythm.

A steady beat is grounded by the third layer: a driving kick pattern [bd:11]*4, filtered and given room ambience for subtle punch. This layer anchors the patch with rhythmic regularity. The final layer is a sawtooth-driven melodic figure ([e1 e3 e2 e1]*2) that loops and is gated by a rhythmic mask (.mask("[1 1 1 1]*4")), ensuring tight control over when notes are played. Random modulation of its filter cutoff and gain (rand.range(...)) makes it shimmer with slight variation each cycle. Together, these layers form a dynamic, syncopated, and rhythmically rich soundscape, tightly bound to a tempo of 130 BPM divided into four parts per beat (setcps(130/60/4)), giving it both groove and fluid complexity.

### Percussion (Strudel.cc)

The percussion in my performance is controlled by a simple strudel.cc patch. This drum section builds progressively from a simple kick-hat-ride combo to a complex, layered rhythm. It begins subtly, with a kick drum paired with hi-hats and ride cymbals, set at a low gain and slight room reverb for spatial depth. As the sequence evolves, it introduces additional textures: mid and low toms accompany snappy snares and claps, each layered with distinct effects such as bitcrushing, panning, and low-pass filtering. The groove becomes more dynamic with glitchy noise bursts and percussive hits enriched by high-pass filtering and wide stereo movement via a Perlin-driven panning effect. Finally, a distorted tom groove rounds out the rhythm with a gritty, compressed texture, blending kick, snare, clap, and toms under a tight low-pass filter. Each layer retains a consistent kick backbone ("bd4"), creating cohesion while allowing individual timbres to cut through with character and rhythmic variation. Each drum function can by dynamically turned on and off during the performance

### Melody (Strudel.cc)

Finally, the melody. 
The melody patch builds a richly layered electric guitar composition using a variety of melodic fragments, harmonic textures, and rhythmic riffs across different octaves and voices. By defining several reusable components (e.g. _lead1 to _lead6, _dug1/2, _sweep1/2, etc.), the patch cycles through both melodic leads and chordal backings in a structured arrangement (arrange). It maintains consistency by anchoring all melodic and harmonic parts in the E minor scale, using instruments like gm_electric_guitar_jazz and embellishing with .attack, .release, .room, and .gain to create smooth transitions, ambient reverb, and dynamic phrasing. The struct patterns introduce off-beat accents and syncopation, which contribute to a rhythmic groove that feels natural and expressive.

Layered over the two previous patches, this melodic guitar arrangement works as a compelling lead texture. The earlier bassline and generative synthesis layers provide atmospheric harmonic support and rhythmic drive, while this guitar patch introduces melodic storytelling and tonal clarity. The slow-moving background filters, FM textures, and ambient effects from the first two patches allow space in the mix for these clean, deliberate guitar lines to sit prominently. Because this patch is rhythmically complex and harmonically constant, it complements the evolving percussive textures and randomised motifs in the other patches—adding narrative phrasing without overwhelming the overall soundscape. The result is a cohesive, cinematic, and texturally rich performance.


## Visuals
The visuals of my performance were done by a program called Synesthesia. It uses the microphone input to manipulate various visual effects. For my performance, I chose a visual effect which clearly shows the beat and rhythm of my patches.

In addition to the visual element on display, I also arranged for each group member to wear matching hats during our performance. 

## Design decsision
Throughout this course, I have always attributed PureData to creating sound and Studel to creating rhythm. That is why I made the decision to have all of my rhythmic components in Studel and the ambient baseline in PD.

## Performance
Thank you to my group members, Daoyan and Yudong for helping perform my performance. 

The perfromance began with Daoyan starting my ambient base patch. I then sequentially layered my rhythmic baseline patches, dynamically adjusting their master volume, then added my melody on top. Yudong controlled the percussion, adding '_' before functions in the patch to dynamically add and remove various percussive elements. 

## References
QCGInteractiveMusic. (n.d.). YouTube. https://www.youtube.com/channel/UCtQVQIgKdxGTpM1ynAPIwyg

YouTube. (n.d.). DZO DIGITAL. [online] Available at: https://www.youtube.com/channel/UCY3y6kGLgimmxATfT25y4Gg [Accessed 6 Jun. 2025].

Namtao (2024). Siberspace (Strudel.cc Algorave). [online] YouTube. Available at: https://www.youtube.com/watch?v=xtH0PlES0NQ [Accessed 6 Jun. 2025].
