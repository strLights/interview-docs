<template><h1 id="https工作原理" tabindex="-1"><a class="header-anchor" href="#https工作原理" aria-hidden="true">#</a> HTTPS工作原理</h1>
<blockquote>
<p>一、首先HTTP请求服务端生成证书，客户端对证书的有效期、合法性、域名是否与请求的域名一致、证书的公钥（RSA加密）等进行校验；<br>
二、客户端如果校验通过后，就根据证书的公钥的有效， 生成随机数，随机数使用公钥进行加密（RSA加密）；<br>
三、消息体产生的后，对它的摘要进行MD5（或者SHA1）算法加密，此时就得到了RSA签名；<br>
四、发送给服务端，此时只有服务端（RSA私钥）能解密。<br>
五、解密得到的随机数，再用AES加密，作为密钥（此时的密钥只有客户端和服务端知道）<br></p>
</blockquote>
<h2 id="拓展-关于加密方面" tabindex="-1"><a class="header-anchor" href="#拓展-关于加密方面" aria-hidden="true">#</a> 拓展(关于加密方面)</h2>
<blockquote>
<p>加密方式</p>
<blockquote>
<p>加密算法一般分为对称加密与非对称加密。</p>
</blockquote>
</blockquote>
<blockquote>
<p>对称加密</p>
<blockquote>
<p>客户端与服务器使用相同的密钥对消息进行加密</p>
</blockquote>
</blockquote>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>优点：

加密强度高，很难被破解
计算量小，仅为非对称加密计算量的 0.1%
缺点：

无法安全的生成和管理密钥
服务器管理大量客户端密钥复杂

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br><span class="line-number">7</span><br><span class="line-number">8</span><br><span class="line-number">9</span><br></div></div><blockquote>
<p>非对称加密</p>
<blockquote>
<p>非对称指加密与解密的密钥为两种密钥。服务器提供公钥，客户端通过公钥对消息进行加密，并由服务器端的私钥对密文进行解密。</p>
</blockquote>
</blockquote>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>优点：安全

缺点

性能低下，CPU 计算资源消耗巨大，一次完全的 TLS 握手，密钥交换时的非对称加密解密占了整个握手过程的 90% 以上。而对称加密的计算量只相当于非对称加密的 0.1%，因此如果对应用层使用非对称加密，性能开销过大，无法承受。
非对称加密对加密内容长度有限制，不能超过公钥的长度。比如现在常用的公钥长度是 2048 位，意味着被加密消息内容不能超过 256 字节。
HTTPS 下的加密
HTTPS一般使用的加密与HASH算法如下：

非对称加密算法：RSA，DSA/DSS
对称加密算法：AES，RC4，3DES
HASH算法：MD5，SHA1，SHA256
其中非对称加密算法用于在握手过程中加密生成的密码，对称加密算法用于对真正传输的数据进行加密，而HASH算法用于验证数据的完整性。由于浏览器生成的密码是整个数据加密的关键，因此在传输的时候使用了非对称加密算法对其加密。非对称加密算法会生成公钥和私钥，公钥只能用于加密数据，因此可以随意传输，而网站的私钥用于对数据进行解密，所以网站都会非常小心的保管自己的私钥，防止泄漏。
TLS握手过程中如果有任何错误，都会使加密连接断开，从而阻止了隐私信息的传输。正是由于HTTPS非常的安全，攻击者无法从中找到下手的地方，于是更多的是采用了假证书的手法来欺骗客户端，从而获取明文的信息，但是这些手段都可以被识别出来

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br><span class="line-number">7</span><br><span class="line-number">8</span><br><span class="line-number">9</span><br><span class="line-number">10</span><br><span class="line-number">11</span><br><span class="line-number">12</span><br><span class="line-number">13</span><br><span class="line-number">14</span><br><span class="line-number">15</span><br></div></div></template>
