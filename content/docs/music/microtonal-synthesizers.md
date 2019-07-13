# Microtonal Synthesizers
*2019*

Recently, I've started writing microtonal music for synthesizers, using a limited sonic palette. 

By immersing myself in a single alternate tuning and limiting myself to a few tools, I aspire to write microtonal music that sounds alien and accessible; strange, but constrained to an consistent internal language.


## The Well Tuned Piano

I use a just intonation devised by La Monte Young for his magnum opus, The Well Tuned Piano. Thanks to Kyle Gann, the tuning used in The Well Tuned Piano has been reverse-engineered, confirmed by LMY himself, and documented on [Kyle Gann's site](https://www.kylegann.com/wtp.html).

I'm documenting the tuning here for posterity, "in frequency ratios to the tonic E-flat":

| Notes | Eb   | E       | F    | F#      | G     | G#        | A        | Bb  | B     | C   | C#      | D |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | 
| Ratios | 1/1 | 567/512 | 9/8	| 147/128 | 21/16 | 1323/1024 | 189/128	 | 3/2 | 49/32 | 7/4 | 441/256 | 63/32 |


Using Kyle Gann's notes, I entered the tuning into [Huygens-Fokker Scala](http://www.huygens-fokker.org/scala/). Scala is hard to use – it's arcane software for a niche user base. It's difficult to iterate on tunings, since there isn't an easy way to preview them. 

I wish I'd used a software synthesizer to test my Scala tuning files, and make tune at least one soft synth to match the hardware. Syncing microtuning in a software synth with a hardware synth is surprisingly tricky, and still warps my brain. I think this has something to do with the resolution of different standards.

- [Kyle Gann's article on WTP in Perspectives of New Music](https://www.dropbox.com/s/b0d59oa6h0h3e7e/PNM-WellTunedPiano.pdf?dl=0)
- [Original liner notes for WTP](https://www.dropbox.com/s/j2ukmqiax99vdzd/LinerNotes-WellTunedPiano.pdf?dl=0)
- [Transposed WTP Tuning (`.scl` file)](https://www.dropbox.com/s/j559yak0b5n7019/WTP-A440.scl?dl=0)

## Tuning the Prophet 12

Many hardware synthesizers support custom tunings. I use the [Prophet 12](https://www.sequential.com/product/prophet-12-keyboard).

Loading a custom tuning onto the Prophet was non-trivial. Your mileage may vary: this doc is based on my vague memories of using niche software 2 years ago, along with the [DSI forum post](https://forum.sequential.com/index.php?topic=2187.0) that I originally used as a reference.

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

There are many software synths that support custom tunings. 

In my search, I was specifically looking for a modeling-based synth (no samples) for piano and plucked string sounds. [Pianoteq](https://www.pianoteq.com/) fits the bill, and supports Scala files.

I also wanted an oscillator-dense synth, capable of producing a convincing trance supersaw. [ZynAddSubFx](http://zynaddsubfx.sourceforge.net/) seems like a good option, and older versions are free.

- [KVR forum thread, instruments with microtonal support](https://www.kvraudio.com/forum/viewtopic.php?t=497777&start=45)
- [Xen Wiki, list of microtonal plugins](https://en.xen.wiki/w/List_of_Microtonal_Software_Plugins)
- [VSTs for microtonal music](https://sevish.com/2014/vsts-for-playing-and-composing-microtonal-music/)
