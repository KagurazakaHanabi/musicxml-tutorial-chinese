# Notation Basics in MusicXML

MIDI represents musical performance information, but leaves out a great deal of information about music notation. MusicXML represents this information, making it much more useful than MIDI for interchange between notation programs. In this section we describe the main elements used to represent music notation that go far beyond what is represented in MIDI files.

## How Music Looks vs. How Music Sounds

Let us look again at the example we used in the previous section - the first four bars of "Après un rêve" by Gabriel Fauré:

![How Music Looks vs. How Music Sounds](../assets/04.jpg)

Clearly our discussion of the MIDI-compatible portion of MusicXML left out many thingsrepresented in this music. Where are the tempo and dynamic markings: the Andantino, pp, dolce,crescendo and diminuendo wedges? Where are stem directions stored? The downstem on theinitial G in the voice part is not what many programs would default to. How is the beamingrepresented, so that all the eighth notes are beamed together in the piano part, but separated intotriplets in the voice part? How are the piano chords split between staves? How are accidentalsindicated, including courtesy accidentals like the A-flat in the fourth bar?

A fundamental part of MusicXML is the distinction between elements that primarily represent thesound of the music versus those that represent its appearance. We discussed the sound elements inthe previous section, and they are of great use to applications dealing with MIDI or other soundfiles. Now we discuss the elements for musical appearance, which are of great use to musicnotation applications.

Here is what the beginning of the voice part looks like for "Après un rêve," up to the end of the first measure:
