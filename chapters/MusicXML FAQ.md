# MusicXML FAQ

## 为什么我们需要一个新的格式

世界上有很多好用的音乐软件，不幸的是，在它们之间共享音乐是困难的。这才是真正的问题，因为没有一个程序可以将所有事情都做得很好。必须为每个软件重新输入音乐数据，这给使用多个音乐软件的人带来很大的不便。
在 MusicXML 之前，唯一受支持的音乐符号交换格式是 MIDI。
MIDI 对于诸如音序器之类的演奏应用来说是一种绝佳的格式，但对于诸如音乐符号之类的其他应用而言却并非如此。 MIDI 无法区分 ♯F 和 ♭G；它不能表示符干方向，符尾，重复，连音线，小节和其他方面的标记。
多年以来，人们已经认识到需要一种新的交换格式，但是没有成功的尝试来创建新的标准格式。 NIFF 可能是迄今为止最成功的尝试，但是它的使用非常有限，并且格式没有得到维护。 SMDL 是最雄心勃勃的尝试，但实际上没有软件使用它。
Internet 友好的标准格式对于 Internet 音乐出版市场的增长是必需的。在 MusicXML 之前，就像在发明 HTML 之前使用 Internet 或在发明 MIDI 之前使用合成器一样。

## 为什么不使用现有的格式，例如 NIFF 和 SMDL

NIFF and SMDL were noble efforts to solve the same type of interchange problem that MusicXML addresses. So why don't we use them rather than inventing something new?
NIFF represents music using a graphical format. There is no concept of a "C" in NIFF: instead, you determine pitch by its placement on a staff. This type of graphical music representation has a long and distinguished history. It works well for the scanning programs that were the focus of
NIFF's work. But it works poorly for many other types of applications, such as sequencing and musical databases. For both of these applications, MIDI works much better than NIFF; for notation, though, NIFF is more complete than MIDI. MusicXML is designed to meet the interchange needs for all these types of applications.
A graphical format like NIFF really does not work well for general interchange, which is one of the main reasons NIFF has not been adopted by more programs. Another major impediment is that NIFF is a binary format, rather than a text format like XML. It is much easier to write and debug programs that read and write to a text format vs. a binary format.
SMDL suffered from the problem of trying to be a general-purpose solution to the problem of representing all possible musics of the past, present, and future. In addition, the project was not grounded in practical implementation experience. The result was something so complicated that practically nobody can understand it. The overwhelming complexity greatly inhibited SMDL's adoption - it certainly inhibited us! - and no commercial software supports it.

## MusicXML 的设计来自哪里

MusicXML was based primarily on two academic music formats:

- The MuseData format, developed by Walter Hewlett at the Center for Computer Assisted Research in the Humanities (CCARH), located at Stanford University
- The Humdrum format, developed by David Huron, based at Ohio State University

Eleanor Selfridge-Field from CCARH edited a magnificent book called **Beyond MIDI: A Handbook of Musical Codes.** Studying this volume made it clear that, as we had been advised, MuseData and Humdrum were the most comprehensive starting points for the type of language we wanted to build.

The first beta version of MusicXML was basically an XML updating of MuseData, with the addition of some key concepts from Humdrum. Since both formats have been used primarily for work in classical and folk music, MusicXML was extended beyond those boundaries to better support contemporary popular music. In recent releases, MusicXML’s capabilities have been greatly expanded so it can serve as a distribution format for digital sheet music as well as an interchange format. Many features have been added in order to make MusicXML near-lossless when it comes to capturing how music is formatted on the printed page.

## 为什么使用 XML
