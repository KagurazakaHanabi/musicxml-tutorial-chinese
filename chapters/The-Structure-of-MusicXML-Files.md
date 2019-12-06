# MusicXML 文件的结构

## 根据层级调整乐谱

假设我们有一段需要两个或者更多的人弹奏的音乐。每个演奏者有一个声部和多个小节。XML 代表层次结构中的数据，但是乐谱更像是格子。我们该如何协调？声部的水平组织是主要的，还是小节的垂直组织？

答案是每个音乐软件都各不相同。音乐认知专家、Humdrum 的发明者 David Huron 建议我们确保能够以两种方式表现音乐，并且能够轻松地转换。

这就是为什么 MusicXML 有两种不同的顶层 DTD，每个都有它自己的根元素。
如果你使用 partwise DTD，根元素是 `<score-partwise>`。乐章是主体，小节包含在乐章中。如果你使用 timewise DTD，根元素是 `<score-timewise>`。小节是主体，乐章包含在小节中。MusicXML XSD 在单个 XSD 中包含两个根元素。

如果没有自动的方法在两种结构之间切换，那么它们将无法正常工作。MusicXML 提供了两个 XSLT 样式表，可以在两种文档类型之间转换。parttime.xsl 样式表从 `<score-partwise>` 转换到 `<scoretimewise>`，timepart.xsl 样式表从 `<score-timewise>` 转换到 `<scorepartwise>`。

读取 MusicXML 的应用程序可以选择主要格式，然后检查该文档类型。如果是正确的根元素，继续即可。如果不是，检查是不是另外一种 MusicXML 根元素。如果是，使用适当的 XSLT 样式表以首选格式创建新的 MusicXML 文档，然后继续。如果都不是，那么这不是一个正确的 MusicXML 乐谱，可以返回适当的错误信息。

当你的应用在编写 MusicXML 文档时，根据你自己的需要写入任何一种格式均可。如果需要，让读取 MusicXML 的程序转换它即可。如果在你的项目中使用两种维度的组织形式，以至于确实都很容易编写，考虑使用 `score-partwise` 格式。如今大多数的 MusicXML 软件都使用这种格式，如果其他所有条件都相同，那么转换次数更少比其他重要。

## 顶层文档元素

score.mod 文件定义了 MusicXML 的基本结构。主要的文档定义都包含在这几行中：

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

`%partwise;` 和 `%timewise;` 是在顶级 DTD partwise.dtd 和 timewise.dtd 中定义的。`<![` 表示条件语句，类似于 C 中的 `#ifdef`。所以如果正在使用 partwise.dtd，`<score-partwise>` 元素就被定义，如果正在使用 timewise.dtd，`<score-timewise>` 元素就被定义。

这两种格式唯一的不同是是 `part` 和 `measure` 元素的排列顺序。score-partwise 文档包含一个或多个 `part` 元素，每个 `part` 包含一个或多个 `measure` 元素。score-timewise 文档则相反。

在任何一种情况下，较低级别的元素都填充有音乐数据实体。包含乐谱中的实际音乐，定义如下：

```ampl
<!ENTITY % music-data
        "(note | backup | forward | direction | attributes |
          harmony | figured-bass | print | sound | barline |
          grouping | link | bookmark)*">
```

此外，每个 MusicXML 文件都包含一个 `%score-header`，定义如下：

```ampl
<!ENTITY % score-header
        "(work?, movement-number?, movement-title?,
          identification?, defaults?, credit*, part-list)">
```

我们将详细看下 `score-header`。如果前面的「Hello World」示例提供了足够的信息，你可能希望跳到下个开始描述 `music-data` 的章节。

## 乐谱的基础元数据

乐谱的头部包含关于此乐谱的基本元数据，例如标题和作曲。它还包含 `part-list`，列出了乐谱中所有的声部和乐器。

以「Mut」的 MusicXML 为例，这是 Franz Schubert 的 _Winterreise_ 中的第 22 首歌。示例如下：

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

可以看到 `score-header` 包括所有五种元素：`work`，`movement-number`, `movement-title`，`identification` 和 `part-list`。只有 `part-list` 是必需的，其它所有元素是可选的。

逐行看下每个部分：

```xml
<work>
  <work-number>D. 911</work-number>
  <work-title>Winterreise</work-title>
</work>
```

在 MusicXML中，独立的乐章通常用单个文件表示。`work` 元素用于标识这是长作品中的哪个章节。Schubert's works are more commonly referred to via D. numbers than opus numbers, so that is what we use in the `work-number` element；`work-title` 是作品名。

If you have all the movements in a work represented, you can use the `opus` element to link to the MusicXML opus file that in turn contains links to all the movements in the work.

```xml
<movement-number>22</movement-number>
```

使用 `movement-number` 标识「Mut」是 _Winterreise_ 中的第 22 首歌，它不限于用于交响乐中的乐章。

```xml
<movement-title>Mut</movement-title>
```

类似的，我们将 `movement-title` 元素用于单曲的标题。如果一首单曲没有很多部分组成，通常会将歌曲的标题放在 `movement-title` 元素中，并且不使用 `work` 和 `movement-number` 元素。

```xml
<identification>
  <creator type="composer">Franz Schubert</creator>
  <creator type="poet">Wilhelm Müller</creator>
```

`identification` 元素的定义位于 identity.mod 文件中。它包含基于 Dublin Core 的基本元数据元素。在这首歌中有两个创作者，是作曲 (composer) 和作词 (poet)。所以使用了两个 `creator` 元素，并使用 `type` 属性区分它们。如果作品的创作者只有作曲，那么就没有必要使用 `type` 属性。

```xml
  <rights>Copyright © 2001 Recordare LLC</rights>
```

`rights` 元素包含版权信息。如果包含多个版权声明（例如词和曲），需要使用多个 `rights` 元素。和 `creator` 元素一样可以使用 `type` 属性说明版权的类型。在此示例中，Mut 的文字和音乐均属于公共领域，但我们对作品的电子版拥有版权。

```xml
  <encoding>
    <encoding-date>2002-02-16</encoding-date>
    <encoder>Michael Good</encoder>
    <software>Finale 2002 for Windows</software>
    <encoding-description>MusicXML 1.0 example</encoding-description>
  </encoding>
```

The `encoding` element contains information about how the MusicXML file was created. Here we are using all four of the available sub-elements to describe the encoding. You can have multiple instances of these elements, and they can appear in any order.

```xml
  <source>Based on Breitkopf &amp; Härtel edition of 1895</source>
</identification>
```

`source` 元素对于从纸质乐谱或手稿进行编码的音乐很有用。不同版本的音乐将包含不同的音乐信息。在我们的案例中，我们以 _Winterreise_ 的 Breitkopf＆Härtel 版本的 Dover 重印为起点，更正了该已发布乐谱中的一些错误。

`identification` 元素还可以包含 `miscellaneous` 元素。 依次包含 `miscellaneous` 元素，每个元素都有一个 `name` 属性。如果您的软件包含一些在 MusicXML DTD 中不存在的标识信息，则在保存和读取 MusicXML 时要保留这些信息可能会有所帮助。

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

`part-list` 是所有 MusicXML 乐谱中所需的一部分。它由一系列 `sore-part` 元素组成，每个元素都具有必需的 `id` 属性和 `part-name` 元素。By convention, our software simply numbers the parts as "P1", "P2", etc. to create the `id` attributes. You may use whatever technique you like as long as it produces unique names for each `score-part`.

In addition to the `part-name`, there are many optional elements that can be included in a `score-part`:

- An `identification` element, helpful if individual parts come from different sources.
- A `part-abbreviation` element. Often, you will use the `part-name` for the name used at the start of the score, and the `part-abbreviation` for the abbreviated name used in succeeding systems.
- A `group` element, used when different parts can be used for different purposes. In MuseData, for instance, there will often be different parts used for a printed score, a printed part, a MIDI sound file, or for data analysis.
- One or more `score-instrument` elements, used to describe instrument sounds and virtual instrument settings, as well as to define multiple instruments within a `score-part`. This element serves as a reference point for MIDI instrument changes.
- One or more `midi-device` elements for identifying the MIDI devices or ports that are being used in a multi-port configuration. Multiple devices let you get beyond MIDI's 16-channel barrier.
- One or more `midi-instrument` elements, specifying the initial MIDI setup for each `score-instrument` within a part.
