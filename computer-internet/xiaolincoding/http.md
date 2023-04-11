# What's HTTP
## HyperText Transfer Protocol

+ 协议
+ 传输
+ 超文本

## Status Code
+ 1xx，中间状态，不常用
+ 2xx，success，报文正确收到并处理。
  + 200，success，如果是非HEAD请求，Body会返回数据。
  + 204，No Content，Body无数据。
  + 206，Partial Content，返回的是资源的一部分，不是全部。
+ 3xx，redirect
  + 301，Moved Permanently
  + 302，Found，请求的资源还在，需要用其他URL访问。
  + 304，Not Modified
>301和301
>
>返回时在响应字段Location设置正确的URL
+ 4xx，报文有误，服务器无法处理。
  + 400，bad request，客户端请求的报文有误。
  + 403，Forbidden，服务器禁止访问资源，不是客户端的请求出错。
  + 404，Not Found，服务器上无资源。
+ 5xx，客户端请求正确，服务器处理时内部发生了错误，服务器端的错误码。
  + 500，internal server error，错误码，服务器发生了什么错误，并不知道。
  + 501，not implemented，客户端请求的功能还不支持。
  + 502，bad gateway，服务器作为网关或者代理发生了错误。
  + 503，server unavailable，服务器很忙。

## Http Attribute
+ HOST
  + www.A.com
  + 访问的URL的域名

+ Content-Length
  + Body的长度
  + HTTP通过回车符、换行符作为Header的边界

+ Connection:Keep-Alive
  + 当客户端发送另外一个请求时，会使用相同的连接。
  + 不断开连接就一直保持。

+ Content-Type
  + 用于服务器返回
  + 标注本次响应的数据是什么格式
> Content-Type : text/html;
>Charset = utf-8
+ Accept
  + 客户端发送时填入的字段。
  + 表示客户端接收返回什么类型的数据。

> Accept = */*;
> 接收任何类型的数据

+ Content-Encoding 返回数据的压缩类型 && Accept-Encoding 接受什么样的压缩数据

## GET && POST
### GET
+ 从服务器获取指定的资源。
+ 超文本，静态的文本、页面、图面、视频。
+ GET请求的参数只能使用ASCII码类型。
+ HTTP对URL的长度无要求，浏览器对URL的长度有要求。
### POST
+ 根据请求报文对相应资源做出处理。
### 安全和幂等
+ 安全和幂等的概念
  + 安全，指请求不会破坏服务器上的资源。
  + 幂等，无论进行多次相同的操作，结果都是相同的。

+ GET方法安全且幂等，浏览器会对返回的数据进行缓存。
+ POST方法不安全也不幂等，浏览器不会缓存。

## HTTP缓存技术
### 强制缓存
### 协商缓存


## HTTP 特性
### advantage
+ 简单
  + 报文格式是 header + body
  + header是Key-value
  + 易于理解

+ 灵活且易于扩展
  + HTTP中的每个字段都可被自定义
  + HTTP位于应用层，底层协议都可以被自定义

+ 应用广泛且跨平台

### disadvantage
+ 无状态
  + 好处，不需要额外空间记忆HTTP的状态
  + 坏处，服务器无记忆能力，关联操作麻烦
  + cookie技术

+ 明文传输
  + wireshark抓包可以肉眼查看body中的内容

+ 不安全
  + 内容可能被窃听
  + 不会验证通信双方的身份
  + 无法证明报文的完整性

# HTTP/1.1
+ 基于TCP/IP、请求-应答方式
+ 长连接
  + 只要任意一端不断开连接，则一直保持连接状态
  + 减少了TCP连接的重复建立和断开所造成的额外开销，减少了服务器端的负载
  + 长世界没有交互会自动断开连接
+ 管道网络传输，流水线，可以同时发出多个HTTP请求
+ 队头阻塞

# HTTP与HTTPS
## HTTPS的特性
+ HTTP是超文本传输，信息是明文传输，存在安全风险的问题。HTTPS解决HTTP不安全的缺点，在传输层与应用层之间加上了SSL/TLS安全协议，使得报文能够加密传输。
+ HTTPS三次握手之后，还需要进行SSL/TLS的握手加密过程。
+ HTTP Port 80，HTTPS Port 443
+ HTTPS需要申请数字证书，来证明服务器的身份是可信的。

## HTTPS解决了HTTP的哪些问题
+ 窃听风险，HTTP传输过程中可能会被窃取内容。HTTPS会对信息进行加密，交互信息无法被窃取。
+ 篡改风险，HTTP协议传输过程中可能会被篡改传输的内容，强行植入垃圾广告。HTTPS增加了校验机制，无法篡改通信内容，篡改了也无法显示。
+ 冒充风险，冒充淘宝网站。身份证书，证明自己是淘宝网。

## HTTPS如何解决以上三个风险
+ 混合加密实现信息的机密性，解决了窃听的风险
+ 摘要算法校验信息的完整性，为数据生成独一无二的指纹，指纹用于校验数据的完整性，解决了篡改的风险
+ 将服务器公钥放入数字证书中，解决了冒充的风险。