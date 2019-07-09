*2019-07*

Recently, I've been writing microtonal music for synthesizers, using a limited sonic palette. 

## The Well Tuned Piano

I use a single tuning, a just intonation devised by La Monte Young for his magnum opus. Thanks to Kyle Gann, the tuning used in The Well Tuned Piano has been reverse-engineered, confirmed by LMY himself, and documented on [Kyle Gann's site](https://www.kylegann.com/wtp.html).

I'm documenting the tuning here for posterity, "in frequency ratios to the tonic E-flat":

| Notes | Eb   | E       | F    | F#      | G     | G#        | A        | Bb  | B     | C   | C#      | D |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| Ratios | 1/1 | 567/512 | 9/8	| 147/128 | 21/16 | 1323/1024 | 189/128	 | 3/2 | 49/32 | 7/4 | 441/256 | 63/32 |


Using Kyle Gann's notes, I entered the tuning into [Huygens-Fokker Scala](http://www.huygens-fokker.org/scala/). Scala is hard to use – it's arcane software for a niche user base. It's hard to iterate on tunings, since there isn't an easy way to preview them. I highly recommend using a software synthesizer to test your `.scl` files (more on microtonal soft synths below).

I ended up transposing the tuning slightly from the original, so that A4 is set to [A440](https://en.wikipedia.org/wiki/A440_(pitch_standard)). This was a useful modification: since the tuning's pitches now roughly match the layout of 12TET on a keyboard, improvising is more intuitive for me, and it's possible combine the tuning with 12TET instruments.

- [Kyle Gann's article on WTP in Perspectives of New Music](https://www.dropbox.com/s/b0d59oa6h0h3e7e/PNM-WellTunedPiano.pdf?dl=0)
- [Original liner notes for WTP](https://www.dropbox.com/s/j2ukmqiax99vdzd/LinerNotes-WellTunedPiano.pdf?dl=0)
- [Transposed WTP Tuning (scala file)](https://www.dropbox.com/s/j559yak0b5n7019/WTP-A440.scl?dl=0)

## Tuning the Prophet 12

Loading a custom tuning onto the [Prophet 12](https://www.sequential.com/product/prophet-12-keyboard), my hardware synth, was non-trivial. I've put together some documentation here for my future self and the internet. Your mileage may vary: this is based on my vague memories of using niche software 2 years ago, and the [DSI forum post](https://forum.sequential.com/index.php?topic=2187.0) that I originally used as a reference.

### 1. Generate a sysex file

DSI uses the MIDI tuning standard (MTS). 

From the Scala program's "show synth" menu:
```
Use MIDI Tuning Standard bulk dump (107) for:
Dave Smith Instruments: Prophet 6, Prophet 12, Pro 2;
```

First, generate a `.scl` file that includes the a "bulk dump" command. In Scala:

```
1 load the scale
2 in the command space write: set synth 107
3 save normally
```

Next, convert the file to sysex, a hex file format. You can use this online [scl-to-mts converter tool](http://www.microtonalsoftware.com/scl-scala-to-mts-converter.html).

### 2. Edit the sysex file's destination slot

To avoid overwriting tuning slots, we'll need to set a destination slot (the Prophet has 17 tuning slots).

You can use a hex editor, like [Hex Fiend](http://ridiculousfish.com/hexfiend/).

```
1 load the .syx file 
2 change the second number of the second file from 00 to other hexadecimal number between 01 to 16 in hexadecimal
3 save 
```

### 3. Send sysex to the Prophet

Finally, you'll need to send the sysex file to the Prophet.

I think this was pretty straightforward, using [SysEx Librarian](https://www.snoize.com/SysExLibrarian/).


## Microtonal Soft Synths
