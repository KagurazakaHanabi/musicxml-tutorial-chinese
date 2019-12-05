# MusicXML FAQ

## 为什么我们需要一个新的格式

世界上有很多好用的音乐软件，不幸的是，在它们之间共享音乐是困难的。这才是真正的问题，因为没有一个程序可以将所有事情都做得很好。必须为每个软件重新输入音乐数据，这给使用多个音乐软件的人带来很大的不便。

在 MusicXML 之前，唯一受支持的音乐符号交换格式是 MIDI。MIDI 对于诸如音序器之类的演奏应用来说是一种绝佳的格式，但对于诸如音乐符号之类的其他应用而言却并非如此。 MIDI 无法区分 ♯F 和 ♭G；它不能表示符干方向，符尾，重复，连音线，小节和其他方面的标记。

多年以来，人们已经认识到需要一种新的交换格式，但是没有成功的尝试来创建新的标准格式。 NIFF 可能是迄今为止最成功的尝试，但是它的使用非常有限，并且格式没有得到维护。 SMDL 是最雄心勃勃的尝试，但实际上没有软件使用它。

Internet 友好的标准格式对于 Internet 音乐出版市场的增长是必需的。在 MusicXML 之前，就像在发明 HTML 之前使用 Internet 或在发明 MIDI 之前使用合成器一样。

## 为什么不使用现有的格式，例如 NIFF 和 SMDL

NIFF 和 SMDL 为解决相同类型的问题做出了出色的努力。 那么为什么不使用它们而是发明新的东西呢？

NIFF 使用图形格式表示音乐。 NIFF 中没有「C」 的概念：相反，您可以通过将其放置在谱杆上来确定音高。 这种类型的图形音乐表示形式具有悠久的历史。 它非常适合 NIFF 工作的扫描程序。 但是，它在许多其他类型的应用程序（例如音序器和音乐数据库）中效果不佳。 对于这两种应用，MIDI 的性能都比 NIFF 好得多。 但是，NIFF 比 MIDI 更完整。 MusicXML 旨在满足所有这些类型的应用程序的共享需求。

像 NIFF 这样的图形格式确实不能很好地用于一般互换，这是 NIFF 未被更多程序采用的主要原因之一。 另一个主要障碍是 NIFF 是二进制格式，而不是 XML 之类的文本格式。与读写二进制格式的程序相比，编写和调试程序要容易得多。

SMDL 遭受了 试图成为代表过去，现在和未来所有可能音乐的通用解决方案 的问题。 此外，该项目并非以实际经验为基础。 结果太复杂，几乎没人能理解。复杂性极大地限制了 SMDL 的采用 - 当然也限制了我们！ - 并且没有商业软件支持它。

## MusicXML 的设计从何而起

MusicXML 主要基于两种学术音乐格式：

- The MuseData format, developed by Walter Hewlett at the Center for Computer Assisted Research in the Humanities (CCARH), located at Stanford University
- The Humdrum format, developed by David Huron, based at Ohio State University

来自 CCARH 的 Eleanor Selfridge-Field 编辑了一本名叫 **Beyond MIDI: A Handbook of Musical Codes** 的书。通过研究此书，我们可以清楚地了解到，正如我们所建议的那样，MuseData 和 Humdrum 是我们要构建的语言类型最全面的起点。

MusicXML 的第一个 beta 版本基本上是对 MuseData 的 XML 更新，并增加了 Humdrum 的一些关键概念。由于两种格式主要用于古典音乐和民间音乐，因此 MusicXML 已扩展到这些范围之外，以更好地支持当代流行音乐。在最新发行的版本中，MusicXML 的功能已大大扩展，因此它既可以用作数字乐谱的分发格式，又可以用作交换格式。添加的许多功能使 MusicXML 在打印页面上格式化乐谱时几乎无损。

## 为什么使用 XML

XML 旨在准确解决我们当今在音乐软件中面临的问题。假设您有 100 个音乐应用，每个应用都有自己的格式。为了使它们之间能够彼此通信，需要编写 10,000 个独立的程序！使用通用的语言，每个应用仅编写一个程序，因此仅需要 100 个单独的程序。消费者以相对较低的成本为软件开发人员获得了巨大的价值。

XML 建立在其前身 SGML 数十年的经验以及 HTML 和 Web 爆炸式增长的经验基础上。正如过去的 HTML 和 MIDI 一样，XML 达到了简单性和强大功能之间神奇的「最佳结合点」。它旨在表示复杂的结构化数据，并且乐谱符合该描述。

使用 XML 使我们不必担心语言的基本语法，而让我们担心语义 - 表示什么以及如何表示。同样，也不需要编写低级解析器来读取该语言：XML 解析器随处可见。基于 XML 的音乐交换语言使音乐软件（一个相对较小的社区）可以利用对大型市场（例如电子商务）生产的工具的投资。

## MusicXML 是否免费

Yes. MusicXML 3.1 is developed by the W3C Music Notation Community Group and licensed under the W3C Community Final Specification Agreement.

## MakeMusic 的软件是否开源

不开源。MusicXML 格式本身的免费和开源很重要。MakeMusic 将对 MusicXML 格式的责任移交给了 W3C Music Notation Community Group 以帮助确保其在音乐界的持续成功。

MakeMusic 没有看到开源我们自己的 Finale MusicXML 软件能带来的优势。我们的 Sibelius 插件不是开源的，但是我们可能会决定在将来进行更改。 许多开源应用程序也包含 MusicXML 支持。

## 谁在使用 MusicXML

Many companies, music software developers, and scholars are using MusicXML in their products and research. People use MusicXML with many different types of notation software, such as:

- Desktop notation editing programs including Finale, Sibelius, Dorico, MuseScore, capella, Encore, and Overture.
- Web-based notation programs for editing, playback, and education, including Noteflight, SmartMusic, Soundslice, Flat, Gustaf, and Scorio.
- Digital audio workstation programs including Cubase, Digital Performer, Logic, Reaper, and Sonar.
- Music scanning programs, including SmartScore, PhotoScore, SharpEye Music Reader, capella-scan, ScoreMaker, PlayScore, and Audiveris.
- Tablature editors, including Guitar Pro, Progression, Fandango, TablEdit, TaBazar, and TuxGuitar.
- iOS notation programs for iPhone and iPad, including Komp, Notion, Symphony Pro, and SeeScore.
- Android notation programs, including Ensemble Composer, Notate, and NotateMe.
- Electronic music stands, including Newzik, Blackbinder, and OrganMuse.
- Musicology applications and toolkits, including music21 and MelodicMatch.

See our MusicXML software page at www.musicxml.com/software/ for a more complete list, including links to each application.

## 有哪些可用的工具

One of the great things about basing our work on XML is that there are tools available for practically every computer platform.

At Recordare, we used Microsoft tools for our first generation of Dolet software. The original Dolet for Finale plug-in was written in a mix of Visual Basic 6.0 and Visual C++ 6.0, using Microsoft's MSXML parser. The Microsoft parser was designed to be easy to use within Visual Basic and succeeded admirably. We had great success with it.

We then rewrote the Dolet for Finale plug-in in Java and C++ so that our software could run on macOS as well as Windows. Many other projects are using Java for multiple platforms, including Linux. We used the Xerces parser from the Apache group, as are most of the other Java-based MusicXML projects that we know. We have also heard good reports about the Xerces C++ parser. Other projects use the built-in XML support provided by Python, JavaScript, and other programming languages.

If all you want to do is write MusicXML files, not read them, you really don't need a parser, though you may find it useful. A scanner like SharpEye Music Reader, for instance, does not have any great need to read MusicXML files. Its MusicXML support is written in C, like the rest of the program, without using any special XML tools. The pae2xml translator is written in Perl. The Dolet 6 for Sibelius plug-in is written in ManuScript. You can also use XSLT to read and transform MusicXML files.

There are many XML sites that can guide you to XML tools beyond what we list here. If you are using an XML parser, in most cases you will probably be using the XML DOM (Document Object Model) to handle MusicXML files. Good DOM support is likely to be more important than SAX support for MusicXML programs.

Many tools today will automatically generate classes from an XSD schema definition. MusicXML’s schema has some complexity that can require manual edits of the automated output, but many developers find these tools to save a lot of time in their MusicXML development.

## 为什么要发布用于 MusicXML 2.0 的 XSD

When we started developing MusicXML, a DTD (Document Type Definition) was the only official W3C recommendation for defining an XML document. Since that time, XSD (XML Schema Definition) has become an official W3C recommendation, and alternative standards like RELAX NG have also become available.

When XSDs were first released, neither the supporting XSD software nor the state of MusicXML application usage was sufficiently advanced to take advantage of this technology. XSDs are more complex than DTDs, so it was clear there would be a cost to creating a MusicXML XSD schema. At the time, it was also not clear how support would evolve for XSD, RELAX NG, and other schema alternatives. It thus made sense to stay with DTDs for the releases of MusicXML 1.0 and 1.1.

XSD and MusicXML technology have both matured significantly in the past few years. Developer tool support for XSDs is now as pervasive as for DTDs. New XML tools such as XQuery and XML data binding tools can work much better with XSDs than DTDs. While RELAX NG has some advantages over XSDs, its software support is not yet as pervasive as for XSDs.

In addition, MusicXML’s move from an interchange to a distribution format makes it increasingly important to provide the most powerful tools possible for automated quality assurance. Validating against an XSD can catch many more errors in XML document creation than validating against a DTD.

These combined customer needs and opportunities regarding XSDs led us to develop a MusicXML 2.0 XSD that was released in September 2008. The XSD puts much more of MusicXML’s semantics into the language definition itself, rather than just in the documentation. Thus there are many documents that validate against the DTD that do not validate against the XSD, but these reflect MusicXML file errors that you do want to catch as early and automatically as possible.

DTDs remain more readable than XSDs for many people. To learn MusicXML, you may find it easiest to read the DTDs, the XSDs, or both in combination. This will depend on your experience and comfort level with the different technologies. The XSDs will generally offer more precise definitions than the DTDs since the format is now much more strongly typed.

## 为什么要使用元素而不是属性

这主要是一个风格决定。 一些 XML 书建议尽可能在元素中而不是属性中表示语义。 这样做的优点之一是元素具有结构，而属性没有结构。 如果发现所表示的内容确实包含多个部分，则可以使用元素创建层次结构。 使用属性，您将被限制为无序列表。 对于信息检索应用程序，直接搜索元素而不是属性 / 元素组合也可能更容易。

In MusicXML, attributes are generally limited to a few uses:

- To indicate if this is where an element starts or stops, such as for slurs and tuplets.
- To identify elements, as in measure numbers or beam levels.
- To suggest how an element would best be printed.
- To suggest how an element would best be converted into MIDI or other sound formats.

In both MusicXML 1.1 and 2.0, the third category - suggesting how an element would best be printed - grew enormously. So you will find that MusicXML 3.1 files make much more use of attributes than do MusicXML 1.0 files. The principles determining when to use elements and when to use attributes have remained the same.

In summary, we follow common recommended practice by using elements for data and attributes for metadata. We find this works well. Certainly there are DTDs and XSDs in other domains that use attributes much more extensively, and they work well too. Either way can do the job as long as it is applied consistently.

While there are a lot of MusicXML elements, we have tried to limit them to elements that directly represent musical concepts. We have tried to avoid using elements that would introduce concepts not found in musical scores. For example, there is no "timeslice" element as found in formats like NIFF. We have generally found that we can represent what applications need without having to introduce artificial elements.
