# 压缩的 .MXL 文件

常规的纯文本 MusicXML 文件可能非常大 - 比原始的 Finale 和 Sibelius 文件或相应的 MIDI 文件大得多。使用 MusicXML 作为交换格式不是什么大问题，但它限制了 MusicXML 作为乐谱发行格式使用。

MusicXML 2.0 引入了一种新的压缩格式，可将 MusicXML 文件的大小减小到与相应的 MIDI 文件大致相同的大小。该格式使用 zip 压缩以及特殊的.mxl 文件后缀和 Internet 媒体类型，以将文件标识为 MusicXML 文件还是常规 XML 文件。本节介绍压缩格式的工作方式。

## 压缩文件格式

MusicXML 使用基于 zip 的 XML 格式，类似于 Open Office 和许多其他 XML 格式。MusicXML 3.1 zip 文件格式与 java.util.zip 包和 Java JAR 文件使用的 zip 格式兼容。它基于在以下位置描述的 Info-ZIP 格式：

[http://www.info-zip.org/doc/appnote-19970311-iz.zip](http://www.info-zip.org/doc/appnote-19970311-iz.zip)

JAR 文件格式在以下位置指定：

[http://docs.oracle.com/javase/8/docs/technotes/guides/jar/jar.html](http://docs.oracle.com/javase/8/docs/technotes/guides/jar/jar.html)

请注意，与 JAR 文件兼容，文件名应以 UTF-8 格式编码。带有 zip 容器的文件被压缩为 DEFLATE 算法。DEFLATE 压缩数据格式（RFC 1951）在以下位置指定：

[http://www.ietf.org/rfc/rfc1951.txt](http://www.ietf.org/rfc/rfc1951.txt)

通过做出这些选择，软件通常可以使用可用于 Java 和大多数其他编程语言的 zip 库来创建压缩的 zip 文件。

## 文件名后缀和媒体类型

对于 MusicXML 文件，建议的文件后缀是.mxl（压缩）和.musicxml（未压缩）。通过使用唯一的文件后缀，程序可以将 MusicXML 文件与常规 XML 文件区分开，而对于未压缩的文件则不能使用.xml 后缀。

现在，许多 XML 编辑工具（例如 XMLSpy 和 Oxygen）都支持 zip 压缩 XML 文件的编辑。所需要做的就是让编辑器应用程序知道 .mxl 文件是基于 zip 的格式。然后，编辑器将使您可以编辑 .mxl 文件的结构以及 zip 存档中包含的 .musicxml 文件。

对于 Internet 使用，MusicXML 3.1 已注册了可用于压缩.mxl 和未压缩.musicxml 文件的媒体类型。压缩的 MusicXML 文件的推荐媒体类型为：

```text
application/vnd.recordare.musicxml
```

对于未压缩的 MusicXML 文件，建议的媒体类型为：

```text
application/vnd.recordare.musicxml+xml
```

## Zip 存档结构

遵循许多基于 zip 的 XML 格式的示例，MusicXML 具有严格定义的方式来确定根 MusicXML 文件在档案中的位置。每个 MusicXML zip 存档都有一个位于 META-INF/container.xml 的文件。此容器描述了 MusicXML 文件的版本和入口点，以及乐谱的 PDF 和音频版本等替代格式。

container.xml 文件由 container.dtd 文件定义。考虑到格式的简单性，目前没有相应的.xsd 文件。

例如，让我们看一下 Make Music 网站上可用的 Dichterliebe01.xml 文件。这是它的 META-INF/container.xml 文件：

```xml
<?xml version="1.0" encoding="UTF-8">
<container>
    <rootfiles>
        <rootfile full-path="Dichterliebe01.xml"
                  media-type="application/vnd.recordare.musicxml+xml" />
    </rootfiles>
</container>
```

container 元素是此文件的文档元素。它包含一个 rootfiles 元素。rootfiles 元素又包含一个或多个 rootfile 元素。必须在第一个 rootfile 元素中描述 MusicXML 根。full-path 属性提供相对于 zip 文件根文件夹的路径。用作根文件的 MusicXML 文件的文档元素可以是 score-partwise，score-timewise 或 opus。

其他 rootfile 元素可以描述备用版本，例如 PDF 和音频文件。可以通过具有不同媒体类型属性值的每个 rootfile 来区分多个 rootfile 元素。例如，如果 Dichterliebe01.mxl 文件包含 PDF 格式的副本以及 MusicXML 文件，则 container.xml 文件将如下所示：

```xml
<?xml version="1.0" encoding="UTF-8">
<container>
    <rootfiles>
        <rootfile full-path="Dichterliebe01.xml"
                  media-type="application/vnd.recordare.musicxml+xml" />
        <rootfile full-path="Dichterliebe01.pdf"
                  media-type="application/pdf" />
    </rootfiles>
</container>
```

如果没有媒体类型值，则假定为 MusicXML 文件。但是，如果存在多个 rootfile，则可能会澄清所有 rootfile 元素都包含 media-type 属性的情况。

zip 归档文件还可包含使用 MusicXML image 和 credit-image 元素引用的图像，或使用 MusicXML 链接元素引用的其他媒体。MusicXML 3.1 并未指定这些文件在 zip 文件中的位置，但是如果将图像或其他类似类型的文件在 zip 档案内的子文件夹中分组在一起，则可能会造成最少的混乱。

zip 中的第一个文件应该是名为 mimetype 的文件。该文件的内容应为 MIME 媒体类型字符串

```text
application/vnd.recordare.musicxml
```

mimetype 文件应使用 US-ASCII 编码，并且不得压缩或加密，并且其 zip 标头中不得包含多余的字段，内容不得包含任何填充空白或空格，并且不得以字节顺序标记开头。

mimetype 文件可以帮助应用程序识别压缩的 MusicXML 文件。出于相同的原因，EPUB 和其他基于 zip 的格式也使用了 mimetype 文件。3.1 版之前的 MusicXML 的较早版本未指定此 mimetype 文件，因此应用程序可能仍会看到没有该文件的容器。
