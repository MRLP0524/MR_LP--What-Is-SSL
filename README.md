##0.前言

今日闲着无聊，上网正好看到一个标题党，*《洒泪告别 神秘代码终被谷歌逼上绝路》*。

因为好奇，所以点开看了一下，结果发现是一篇逗逼文章，说白了就是说一下，SSL 到底是什么？ 正巧之前也看过一些国外的文章，今天就一起来和大家分享一下，什么是 SSL。

##1.SSL 的由来

我们知道，**HTTP协议传输的数据都是未加密的，也就是明文的，因此使用HTTP协议传输隐私信息非常不安全。**为了保证这些隐私数据能加密传输，网景公司设计了SSL（Secure Sockets Layer）协议用于对HTTP协议传输的数据进行加密，从而就诞生了HTTPS。

这里面涉及了两个概念，分别是 SSL 和 HTTPS 。

那么我们接下来就一起来看看，这两个东西都分别是什么？

##2. 什么是 SSL ？

>SSL
>Secure Sockets Layer [安全套接层](http://baike.baidu.com/view/525499.htm),及其继任者[传输层安全](http://baike.baidu.com/view/831898.htm)（Transport Layer Security，TLS）是为[网络通信](http://baike.baidu.com/view/538641.htm)提供安全及[数据完整性](http://baike.baidu.com/view/702953.htm)的一种安全协议。TLS与SSL在[传输层](http://baike.baidu.com/view/239605.htm)对网络连接进行加密。

>----- [百度百科](http://baike.baidu.com/link?url=ETZAyshF68GM2XTX7MfrQOIYzeONBOdYIExZPjGWOylnAXRBs2e8YXDKmUNtji9GTi_40uDWc2UIX6jUWjmwf_)

说白了，安全套接字层（SSL）是一种计算机网络协议认证客户端身份验证和加密的通信之间，一般用于服务器和客户。

SSL允许的敏感信息，如信用卡号码，社会安全号码和登录凭据安全地传输。通常情况下，浏览器和Web服务器之间发送的数据是纯文本，让你容易受到窃听发送。如果攻击者可以拦截所有的数据在浏览器和Web服务器之间发送的，他们可以看到和使用这些信息。

那有一个问题呀，**什么时候进行的 SSL 加密的呢？**

这里我们可以参考一张图。

![](http://upload-images.jianshu.io/upload_images/693359-55c742bc3e8b3897.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

首先明确一点，我们的 HTTP 是属于 应用层的协议。

之后当我们去请求数据的时候，我们的计算机网络协议，实际上是从应用层开始向下利用下层协议的原理，在每层增加相应的头部信息。

![](http://upload-images.jianshu.io/upload_images/693359-d1cde3cfa0aff82d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这样我们就能获取到对应的请求数据的包了。

![](http://upload-images.jianshu.io/upload_images/693359-5dbbb2920eef79bb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可是细心的小伙伴一定发现了，刚才看第一张图，不是说在 TCP 和 IP 之上还存在一个 SSL 或 TLS 么？

这两个东西哪里去了？

实际上，如果我们直接去进行传输，那我们的数据就好像是脱了衣服的美女一样，没有一点点防备。

那我们平时肯定不能够就这么上街呀，所以我们在出去之前，先要去穿一层“衣服”。

也就是进行一次加密。

例如下面的代码：

```
POST / HTTP/1.1
Host: www.baidu.com
User-Agent: ...
Content-Length:27
Cookie: session=fsdaf;aaa=dfasf;......

name=user&password=password
```

*Content-length的长度是下面数据的长度。*

当不使用加密时，这段数据直接在网上传播，可以被监听并破解。而当我们把这些信息扔到一个黑盒子（SSL层进行包装）里，我们继续让这个黑盒子在网上传播，可以被监听，但你必须要有对应的密钥才能解开。

这样的话，我们传输的内容安全系数也就高的多了，这个也就是我们俗称的 HTTPS 加密。

在这里再简单提一下 TLS，了解即可。

>SSL跟TLS不是一回事，但他们很相似，TLS是SSL的继任者。
>SSL是个二进制协议，HTTP是个字符型协议。如果地址以HTTPS开头的话，客户端会先用HTTP协议连接目标服务器的80端口，（这个过程是不加密的）。
>这个过程交换双方协议的版本号，选择双方都了解的密码，对双方身份进行验证，生成临时的会话密匙。
>接着，客户端利用相应的参数跟服务器进行通信，从这里开始就开始加密了。

如果我们设置了 HTTPS ，我们就可以在网址的开始位置，看到一个小锁头。


![](http://upload-images.jianshu.io/upload_images/693359-e95472993e08f570.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


##3. 附录 - SSL的历史

SSL协议是由[网景公司](http://translate.baiducontent.com/transpage?cb=translateCallback&ie=utf8&source=url&query=http%3A%2F%2Fsearchsoa.techtarget.com%2Fdefinition%2FNetscape&from=en&to=zh&token=&monLang=zh)在上世纪90年代。公司希望传输中的数据进行加密，其主打的Netscape Navigator浏览器和Web服务器之间的网络上以确保敏感数据，如信用卡号码，进行保护。
1版从未公开发布，2版，二月发布的1995，包含了一些安全缺陷。
3版包括一个完整的重新设计，在1996发布。
尽管它从未正式规范——SSL 3 1996稿发表的[IETF](http://translate.baiducontent.com/transpage?cb=translateCallback&ie=utf8&source=url&query=http%3A%2F%2Fsearchsoa.techtarget.com%2Fdefinition%2FIETF&from=en&to=zh&token=&monLang=zh)RFC 6101中的历史文件，它成为在互联网上提供安全通信的事实标准。

在IETF正式接管了SSL协议规范，它通过一个开放的过程，3.1版的SSL传输层安全性1、介绍安全改进减轻弱点已经在早期版本中找到释放。
（改名是为了避免和Netscape。任何法律问题）对SSL的攻击都集中在实现上的问题，但[贵宾犬](http://translate.baiducontent.com/transpage?cb=translateCallback&ie=utf8&source=url&query=http%3A%2F%2Fsearchsecurity.techtarget.com%2Fdefinition%2FPOODLE-Padding-Oracle-On-Downgraded-Legacy-Encryption&from=en&to=zh&token=&monLang=zh)漏洞是在SSL 3协议本身已知的缺陷，开发的方式，它忽略了填充字节时运行[密码块链接（CBC）](http://translate.baiducontent.com/transpage?cb=translateCallback&ie=utf8&source=url&query=http%3A%2F%2Fsearchsecurity.techtarget.com%2Fdefinition%2Fcipher-block-chaining&from=en&to=zh&token=&monLang=zh)模式。
该漏洞可能允许攻击者解密敏感信息，如身份认证[Cookies](http://translate.baiducontent.com/transpage?cb=translateCallback&ie=utf8&source=url&query=http%3A%2F%2Fsearchsoftwarequality.techtarget.com%2Fdefinition%2Fcookie&from=en&to=zh&token=&monLang=zh)。
TLS 1是不容易受到这种攻击，因为它指定所有填充字节必须有相同的价值和被验证。

其他关键的差异，使SSL和TLS TLS更安全高效的协议进行消息认证，密钥材料生成和支持的密码套件与TLS支持新的和更安全的算法。
TLS和SSL可互操作的，尽管TLS提供向后兼容性为了与遗留系统的工作。
TLS协议的最新版本是1.2。

参考资料：

>1. [百度百科](http://baike.baidu.com/link?url=ETZAyshF68GM2XTX7MfrQOIYzeONBOdYIExZPjGWOylnAXRBs2e8YXDKmUNtji9GTi_40uDWc2UIX6jUWjmwf_)

>2. [WHAT IS SSL](https://www.digicert.com/ssl.htm)

>3. [Secure Sockets Layer (SSL)](http://searchsecurity.techtarget.com/definition/Secure-Sockets-Layer-SSL)

>4.  [知乎](http://blog.csdn.net/mr_lp?viewmode=contents)
