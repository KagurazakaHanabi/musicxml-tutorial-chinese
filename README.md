# MusicXML 3.1 Tutorial

MusicXML 是数字乐谱的交换和分发格式。目标是为西方常用音乐符号创建通用格式，类似 MP3 格式用于录制音频的作用。设计这种音乐信息主要用于记谱软件，音序器，其他表演节目，音乐教育项目和音乐数据库。

本教程的目的是向对阅读或编写 MusicXML 文件感兴趣的软件开发人员介绍 MusicXML。MusicXML 具有支持专业级音乐软件所需的许多功能。但是您无需使用或理解所有这些元素即可上手。

## 目录

- [MusicXML FAQ](chapters/MusicXML-FAQ.md)
  - 为什么我们需要一个新的格式？
  - 为什么不使用现有的格式，例如 NIFF 和 SMDL？
  - MusicXML 的设计从何而起？
  - 为什么使用 XML？
  - MusicXML 是否免费？
  - MakeMusic 的软件是否开源？
  - 谁在使用 MusicXML？
  - 有哪些可用的工具？
  - 为什么要发布用于 MusicXML 2.0 的 XSD？
  - 为什么要使用元素而不是属性？
  - 为什么 MusicXML 这么冗长？那不是效率低下吗？
  - 在浏览器中查看 MusicXML 文件时，为什么看到的是文本而不是音乐？
- [MusicXML 中的「Hello World」](chapters/Hello-World-in-MusicXML.md)
- [MusicXML 文件的结构](chapters/The-Structure-of-MusicXML-Files.md)
  - 根据层级调整乐谱
  - 顶层文档元素
  - 乐谱的基础元数据
- [MusicXML 中 MIDI 兼容的部分](chapters/The-MIDI-Compatible-Part-of-MusicXML.md)
  - 属性
    - Divisions
    - 调号
    - 拍号
    - 移调
  - 音高
  - 时值
  - 连结音
  - 和弦
  - 歌词
  - 多声部
  - 重复
  - Sound Suggestions
- [MusicXML 中的符号基础](chapters/Notation-Basics-in-MusicXML.md)
  - How Music Looks vs. How Music Sounds
  - 属性
    - 五线谱
    - 谱号
    - 拍号
  - Musical Directions
  - Note Appearance
    - Symbolic Note Types
    - 连音
    - 符杆
    - 符尾
    - 临时记号
    - Notations
  - 多声部
- [和弦符号和 和弦图](chapters/Chord-Symbols-and-Diagrams.md)
  - 和弦符号
  - 和弦图
- [弦乐器](chapters\Tablature-in-MusicXML.md)
  - 品和弦
  - 调弦
  - 击弦和勾弦
- [打击乐器](chapters/Percussion-in-MusicXML.md)
  - Unpitched Notes
  - 谱线
  - Multiple Instruments Per Part
  - Notehead Shapes
  - Measure Styles
- [压缩的 .MXL 文件](chapters/Compressed-MXL-Files.md)
  - 压缩文件格式
  - 文件名后缀和媒体类型
  - Zip 存档结构

### MusicXML FAQ

为什么我们需要一个新的格式？

What's behind some of the ways that MusicXML looks and feels?

我可以使用什么工具软件？

MusicXML 免费吗？

### MusicXML 中的 "Hello World"

最简单的 MusicXML 文件：一个声部，一个小节，一个音符。

### MusicXML 文件的结构

有两种构造 MusicXML 文件的方法：声部中包含小节，小节中包含声部。本节介绍如何以任何一种方式进行操作，以及如何在它们之间转换，还介绍了 MusicXML 文件开始处的描述性数据。

### MusicXML 的 MIDI 兼容

需要 MusicXML 的哪些部分来表示 MIDI 文件？此处介绍了 MusicXML 中和 MIDI 等价的部分。

### MusicXML 中的符号基础

这部分我们讨论了 MIDI 之外的基本符号功能，包括符杆，符尾，临时记号，演奏技巧和指示。

### 和弦符号和 和弦图

MusicXML 为和声提供了丰富的表示形式，用于和声分析和 和弦符号。这部分我们讨论如何创建许多现代乐谱中的和弦符号和 和弦图，包括主唱，钢琴 / 人声 / 吉他和乐队总谱。

### 弦乐器

这部分我们描述了 TAB 谱的基本知识：指定弦，品格，调弦和吉他特有的表示法（例如击弦和勾弦）。

### 打击乐器

这部分我们讨论代表打击乐部分（例如鼓组）所需的步骤。其中一些技术适用于其他类型的音乐，例如使用多种乐器，备用符头和不同小节风格。

### 压缩的 .MXL 文件

MusicXML 2.0 添加了一种基于 zip 的压缩格式，大大减小了 MusicXML 文件的大小。
这部分我们讨论压缩的 .mxl 格式的结构。
