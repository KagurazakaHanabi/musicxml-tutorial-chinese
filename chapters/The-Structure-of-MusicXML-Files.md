# MusicXML 文件的结构

## 根据层级调整乐谱

Say we have a piece of music for two or more people to play. It has multiple parts, one per player, and multiple measures. XML represents data in a hierarchy, but musical scores are more like a lattice. How do we reconcile this? Should the horizontal organization of musical parts be primary, or should the vertical organization of musical measures?

The answer is different for every music application. David Huron, a music cognition specialist and the inventor of Humdrum, advised us to make sure we could represent music both ways, and be able to switch between them easily.

This is why MusicXML has two different top-level DTDs, each with its own root element. If you use the partwise DTD, the root element is `<score-partwise>`. The musical part is primary, and measures are contained within each part. If you use the timewise DTD, the root element is `<score-timewise>`. The measure is primary, and musical parts are contained within each measure. The MusicXML XSD includes both of the top-level document elements in a single XSD file.

Having two different structures does not work well if there is no automatic way to switch between them. MusicXML provides two XSLT stylesheets to convert back and forth between the two document types. The parttime.xsl stylesheet converts from `<score-partwise>` to `<scoretimewise>`, while the timepart.xsl stylesheet converts from `<score-timewise>` to `<scorepartwise>`.

An application reading MusicXML can choose which format is primary, and check for that document type. If it is your root element, just proceed. If not, check to see if it is the other MusicXML root element. If so, apply the appropriate XSLT stylesheet to create a new MusicXML document in your preferred format, and then proceed. If it is neither of the two toplevel document types, you do not have a MusicXML score, and can return an appropriate error message.

When your application writes to MusicXML, simply write to whichever format best meets your needs. Let the program reading the MusicXML convert it if necessary. If you have a twodimensional organization in your program so that either format is truly equally easy to write, consider using the score-partwise format. Most of today's MusicXML software uses this format, so if all else is equal, conversion times should be lower overall.

## Top-Level Document Elements

The score.mod file defines the basic structure of a MusicXML file. The primary definition of the file is contained in these lines:

```ampl
<![ %partwise; [
<!ELEMENT score-partwise (%score-header;, part+)>
<!ELEMENT part (measure+)>
<!ELEMENT measure (%music-data;)>
]]>
<![ %timewise; [
<!ELEMENT score-timewise (%score-header;, measure+)>
<!ELEMENT measure (part+)>
<!ELEMENT part (%music-data;)>
]]>
```

The `%partwise;` and `%timewise;` entities are set in the top-level DTDs partwise.dtd and timewise.dtd. The `<![` lines indicate a conditional clause like the `#ifdef` statement in C. So if partwise.dtd is used, the `<score-partwise>` element is defined, while if timewise.dtd is used, the `<score-timewise>` element is defined.

You can see that the only difference between the two formats is the way that the `part` and `measure` elements are arranged. A score-partwise document contains one or more `part` elements, and each `part` element contains one or more `measure` elements. The score-timewise document reverses this ordering.

In either case, the lower-level elements are filled with a music-data entity. This contains the actual music in the score, and is defined as:

```ampl
<!ENTITY % music-data
        "(note | backup | forward | direction | attributes |
          harmony | figured-bass | print | sound | barline |
          grouping | link | bookmark)*">
```

In addition, each MusicXML file contains a %score-header; entity, defined as:

```ampl
<!ENTITY % score-header
        "(work?, movement-number?, movement-title?,
          identification?, defaults?, credit*, part-list)">
```

We will now look at the score-header entity in more detail. If the example in the preceding "Hello World" section gave you enough information, you may want to skip ahead to the next section that starts describing music-data.

## The Score Header Entity

The score header contains some basic metadata about a musical score, such as the title and composer. It also contains the part-list, which lists all the parts or instruments in a musical score.

As an example, take our MusicXML encoding of "Mut," the 22nd song from Franz Schubert's song cycle Winterreise. Here is a sample score header for that work:

```xml
<work>
  <work-number>D. 911</work-number>
  <work-title>Winterreise</work-title>
</work>
<movement-number>22</movement-number>
<movement-title>Mut</movement-title>
<identification>
  <creator type="composer">Franz Schubert</creator>
  <creator type="poet">Wilhelm Müller</creator>
  <rights>Copyright © 2001 Recordare LLC</rights>
  <encoding>
    <encoding-date>2002-02-16</encoding-date>
    <encoder>Michael Good</encoder>
    <software>Finale 2002 for Windows</software>
    <encoding-description>MusicXML 1.0 example</encoding-description>
  </encoding>
  <source>Based on Breitkopf &amp; Härtel edition of 1895</source>
</identification>
<part-list>
  <score-part id="P1">
    <part-name>Singstimme.</part-name>
  </score-part>
  <score-part id="P2">
    <part-name>Pianoforte.</part-name>
  </score-part>
</part-list>
```

You see that this score-header has all five of the possible top-level elements in the score-header entity: the work, movement-number, movement-title, identification, and part-list. Only the partlist is required, all other elements are optional.

Let's look at each part in turn:

```xml
<work>
  <work-number>D. 911</work-number>
  <work-title>Winterreise</work-title>
</work>
```

In MusicXML, individual movements are usually represented as separate files. The work element is used to identify the larger work of which this movement is a part. Schubert's works are more commonly referred to via D. numbers than opus numbers, so that is what we use in the worknumber element; the work-title is the name of the larger work.

If you have all the movements in a work represented, you can use the opus element to link to the MusicXML opus file that in turn contains links to all the movements in the work.

```xml
<movement-number>22</movement-number>
```

_Winterreise_ is a cycle of 24 songs. We use the movement-number to identify that "Mut" is the 22nd song in the cycle - it is not restricted to use for movements in a symphony.

```xml
<movement-title>Mut</movement-title>
```

Similarly, we use the movement-title element for the title of the individual song. If you have a single song that is not part of a collection, you will usually put the title of the song in the movement-title element, and not use either the work or movement-number elements.

```xml
<identification>
  <creator type="composer">Franz Schubert</creator>
  <creator type="poet">Wilhelm Müller</creator>
```

The identification element is defined in the identity.mod file. It contains basic metadata elements based on the Dublin Core. In this song, as many others, there are two creators: in this case, the composer and the poet. Therefore, we use two creator elements, and distinguish their roles with the type attribute. For an instrumental work with just one composer, there is no need to use the type attribute.

```xml
  <rights>Copyright © 2001 Recordare LLC</rights>
```

The rights element contains the copyright notice. You may have multiple rights elements if multiple copyrights are involved, say for the words and the music. As with the creator element, these can have type attributes to indicate what type of copyright is involved. In this example, both the words and music to Mut are in the public domain, but we are copyrighting our electronic edition of the work.

```xml
  <encoding>
    <encoding-date>2002-02-16</encoding-date>
    <encoder>Michael Good</encoder>
    <software>Finale 2002 for Windows</software>
    <encoding-description>MusicXML 1.0 example</encoding-description>
  </encoding>
```

The encoding element contains information about how the MusicXML file was created. Here we are using all four of the available sub-elements to describe the encoding. You can have multiple instances of these elements, and they can appear in any order.

```xml
  <source>Based on Breitkopf &amp; Härtel edition of 1895</source>
</identification>
```

The source element is useful for music that is encoded from a paper published score or manuscript. Different editions of music will contain different musical information. In our case, we used the Dover reprint of the Breitkopf & Härtel edition of Winterreise as our starting point, correcting some errors in that published score.

The identification element also may contain a miscellaneous element. This in turn contains miscellaneous-field elements, each with a name attribute. This can be helpful if your software contains some identification information not present in the MusicXML DTD that you want to preserve when saving and reading from MusicXML.

```xml
<part-list>
  <score-part id="P1">
    <part-name>Singstimme.</part-name>
  </score-part>
  <score-part id="P2">
    <part-name>Pianoforte.</part-name>
  </score-part>
</part-list>
```

The part-list is the one part of the score header that is required in all MusicXML scores. It is made up of a series of score-part elements, each with a required id attribute and part-name element. By convention, our software simply numbers the parts as "P1", "P2", etc. to create the id attributes. You may use whatever technique you like as long as it produces unique names for each score-part.

In addition to the part-name, there are many optional elements that can be included in a score-part:

- An identification element, helpful if individual parts come from different sources.
- A part-abbreviation element. Often, you will use the part-name for the name used at the start of the score, and the part-abbreviation for the abbreviated name used in succeeding systems.
- A group element, used when different parts can be used for different purposes. In MuseData, for instance, there will often be different parts used for a printed score, a printed part, a MIDI sound file, or for data analysis.
- One or more score-instrument elements, used to describe instrument sounds and virtual instrument settings, as well as to define multiple instruments within a score-part. This element serves as a reference point for MIDI instrument changes.
- One or more midi-device elements for identifying the MIDI devices or ports that are being used in a multi-port configuration. Multiple devices let you get beyond MIDI's 16-channel barrier.
- One or more midi-instrument elements, specifying the initial MIDI setup for each score-instrument within a part.
