<template><h1 id="http工作原理-同一次完整的http事务是怎样一个过程" tabindex="-1"><a class="header-anchor" href="#http工作原理-同一次完整的http事务是怎样一个过程" aria-hidden="true">#</a> HTTP工作原理(同一次完整的HTTP事务是怎样一个过程？)</h1>
<p>这个问题跟输入url后，到页面呈现经历了那些过程类似！</p>
<h2 id="简单说" tabindex="-1"><a class="header-anchor" href="#简单说" aria-hidden="true">#</a> 简单说:</h2>
<blockquote>
<p>1）域名解析</p>
</blockquote>
<blockquote>
<p>2） 发起TCP的3次握手</p>
</blockquote>
<blockquote>
<p>3） 建立TCP连接后发起http请求</p>
</blockquote>
<blockquote>
<p>4） 服务器响应http请求，浏览器得到html代码</p>
</blockquote>
<blockquote>
<p>5） 浏览器解析html代码，并请求html代码中的资源（如js、css、图片等）</p>
</blockquote>
<blockquote>
<p>6） 浏览器对页面进行渲染呈现给用户</p>
</blockquote>
<h2 id="详细解析" tabindex="-1"><a class="header-anchor" href="#详细解析" aria-hidden="true">#</a> 详细解析：</h2>
<blockquote>
<p>HTTP协议定义Web客户端如何从Web服务器请求Web页面，以及服务器如何把Web页面传送给客户端。HTTP协议采用了请求/响应模型。客户端向服务器发送一个请求报文，请求报文包含请求的方法、URL、协议版本、请求头部和请求数据。服务器以一个状态行作为响应，响应的内容包括协议的版本、成功或者错误代码、服务器信息、响应头部和响应数据。</p>
</blockquote>
<blockquote>
<p>以下是 HTTP 请求/响应的步骤：</p>
</blockquote>
<blockquote>
<p>1、客户端连接到Web服务器<br></p>
<blockquote>
<p>一个HTTP客户端，通常是浏览器，与Web服务器的HTTP端口（默认为80）建立一个TCP套接字连接。例如，http://www.baidu.com。<br></p>
</blockquote>
</blockquote>
<blockquote>
<p>2、发送HTTP请求<br></p>
<blockquote>
<p>通过TCP套接字，客户端向Web服务器发送一个文本的请求报文，一个请求报文由请求行、请求头部、空行和请求数据4部分组成。<br></p>
</blockquote>
</blockquote>
<blockquote>
<p>3、服务器接受请求并返回HTTP响应<br></p>
<blockquote>
<p>Web服务器解析请求，定位请求资源。服务器将资源复本写到TCP套接字，由客户端读取。一个响应由状态行、响应头部、空行和响应数据4部分组成。<br></p>
</blockquote>
</blockquote>
<blockquote>
<p>4、释放连接TCP连接<br></p>
<blockquote>
<p>若connection 模式为close，则服务器主动关闭TCP连接，客户端被动关闭连接，释放TCP连接;若connection 模式为keepalive，则该连接会保持一段时间，在该时间内可以继续接收请求;<br></p>
</blockquote>
</blockquote>
<blockquote>
<p>5、客户端浏览器解析HTML内容<br></p>
<blockquote>
<p>客户端浏览器首先解析状态行，查看表明请求是否成功的状态代码。然后解析每一个响应头，响应头告知以下为若干字节的HTML文档和文档的字符集。<br>
客户端浏览器读取响应数据HTML，根据HTML的语法对其进行格式化，并在浏览器窗口中显示。<br></p>
</blockquote>
</blockquote>
</template>
