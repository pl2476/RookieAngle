# 关于Node.js的字符编码
###### 文章在我的博客上的地址： [点击跳转](http://www.ershing.cn/nodejsencoding/ "点击我")

        关于字符编码，其实是非常基础的东西，不过，对于很多人来说，也没有弄清楚它是怎样来的一个东西，就只知道有很多不同的字符编码，常用的是utf-8，所以这里还是要说一下字符编码。

        对于计算机来说，它可以处理这么多不同数据（视频、图片、程序等等），是怎样做到的呢？其实对硬件来说，它能感受到的就是高低电平，低电平表示0，高电平表示1，那么它就能处理0和1这两种数据（实际远不止这么简单），所以可以说，它实质处理的是由1和0组合的二进制数据。

        由于我们对计算机的输入远远不止1和0两个数字，所以必须利用它们的组合来表示其他的数字或字符，我们都知道，一个字节（byte） 有8个比特（bit），就是一个8位的二进制数，所以一个字节可以用0-255这么多个整数来表示其他东西。

        大家都知道，美国人发明计算机时候，肯定按照自己想法来搞，所以按照它们的字符来对应整数的话，只有0-127个字符被编码到计算机里，包括大小写字母、数字和其他一些符号等等，这个编码表就是著名的ASCII编码。

        那么问题就来了，你美国自己那么少字符，我们中国这么复杂的文字怎么表示呢？1个字节肯定不够用来表示了，所以我们会用两个字节来表示，制定了我们的GB2312编码。当然了，其他国家也会这样了，所以有很多不同的编码。

        那么问题又来了，如果的数据里面又有我们这个国家的东西，又有你们国家的东西，那么无论用哪个字符编码，都肯定会出现乱码的情况啊，所以，就出现了大一统的Unicode编码。

        而这个Unicode编码呢，又是两个字节的，为什么呢？因为能够表示的东西足够多啊，那如果我全部数据都是英文的话，你要我一个字母用两个字节表示，就要前面补0，相当于浪费了一倍的存储空间了，所以，就出现了可伸缩长度的UTF-8编码，又叫做万国码，现在已经标准化为RFC 3629，可以用1到6个字节编码Unicode字符，表示英文字母用一个字节，表示中文用三个字节，所以如果用的多英文的时候又可以节省空间了。

        好了，可以回过头来说一下Node.js的字符编码了。

        Node.js目前支持的字符编码有这几种（用字符串表示）：

        'ascii'、'utf8'、'utf16le'、'ucs2'、'base64'、'latin1'、'binary'、'hex'

        前面两个都说了，而‘utf16le’是用2个 或 4 个字节的 Unicode 字符编码，相当于又是一个变种的Unicode，而‘ucs2’就是‘utf16le’的别名，一样的。

        至于‘base64’，相信大家都很熟悉了，它是网络上最常见的用于传输8Bit字节代码的编码方式之一，有时候我们见到的类似“%XX”形式的就是通过‘base64’加密的（转换），它的转换过程大概如此：先将字符转换为ascii编码，然后用二进制表示，以三个字节（每个字节有8位）为一组，然后分成4份，每份6位，当然了，每一份要补全字节，都要在前面加两个0，就变成了四个字节了（实际浪费了三分一的空间），这么有规律的转换，所以是有Base64编码表查到每一个编码对应的真实字符的。

        而'latin1'就是一字节编码，类似‘ascii’，实际上虽然‘ascii’也是一字节字符编码，但是它实际只利用了7位，最高位为0，因为它只表示0-127，而‘latin1’就表示0-255，所以它向下兼容‘ascii’的，而‘binary’就是'latin1'的别名。

        最后，'hex'就是将每个字节编码为两个十六进制字符，2的8次方和16的平方相等啦，所以它们可以转换过来的啦。

        其实字符编码，就是用一个整数来表示某一个字符的一种方式，而且不会重复，至于你选择用一个字节（二进制），两个字节（二进制），还是不同进制（十进制、十六进制）来表示，就是不同的字符编码了。

<div align=center><img src="http://img3.imgtn.bdimg.com/it/u=1855107654,1762545927&fm=26&gp=0.jpg"/></div>