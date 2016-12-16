# ASCII模式一丁点补充

最近在处理一个问题时，从ORACLE(AL32UTF8)到文本文件时，发现使用ASCII模式，数据竟然不正确。在查询源和目标的16进制编码时，在目标文件中，发生了变化，实在是诡异。

这个问题在倒腾了一会之后，发现罪魁祸首就是字符串长度问题。将字符串长度增加2倍之后，整个数据都正确了。 同时也感谢台湾的David。

仔细想了一下，根本原因就在于

- ASCII模式的工作原理，它是处理单字节的，所以它的长度也是按单字节来计算的。
- 而对于UTF-8编码是变长的，所以对于中文字符串长度至少是原来的2倍。
- 根据CJK编码，现在只用到Plane2，所以，对于中日韩，字符长度设置成原来的3倍就可以了。


