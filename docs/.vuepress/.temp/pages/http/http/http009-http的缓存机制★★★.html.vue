<template><h1 id="http009-http的缓存机制★★★" tabindex="-1"><a class="header-anchor" href="#http009-http的缓存机制★★★" aria-hidden="true">#</a> http009-http的缓存机制★★★</h1>
<blockquote>
<p>根据是否需要重新向服务器发起请求来分类，可以将其分为两大类(强制缓存，对比缓存)，强制缓存如果生效，不需要再和服务器发生交互，而对比缓存不管是否生效，都需要与服务端发生交互。</p>
</blockquote>
<blockquote>
<p>两类缓存规则可以同时存在，强制缓存优先级高于对比缓存，也就是说，当执行强制缓存的规则时，如果缓存生效，直接使用缓存，不再执行对比缓存规则。</p>
</blockquote>
<h3 id="强制缓存" tabindex="-1"><a class="header-anchor" href="#强制缓存" aria-hidden="true">#</a> 强制缓存</h3>
<p>对于强制缓存来说，header中会有两个字段来标明失效规则（Expires/Cache-Control）</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>Expires
    Expires的值为服务端返回的到期时间，即下一次请求时，请求时间小于服务端返回的到期时间，直接使用缓存数据。
    不过Expires 是HTTP 1.0的东西，现在默认浏览器均默认使用HTTP 1.1，所以它的作用基本忽略。
    另一个问题是，到期时间是由服务端生成的，但是客户端时间可能跟服务端时间有误差，这就会导致缓存命中的误差。
    所以HTTP 1.1 的版本，使用Cache-Control替代。


Cache-Control
    用于定义所有的缓存机制都必须遵循的缓存指示，这些指示是一些特定的指令，包括public、private、no-cache、no-store、max-age、s-maxage以及must-revalidate等；Cache-Control中设定的时间会覆盖Expires中指定的时间；

    private:             客户端可以缓存
    public:              客户端和代理服务器都可缓存
    max-age=xxx:   缓存的内容将在 xxx 秒后失效
    no-cache:          需要使用对比缓存来验证缓存数据 (表示可以存储，但在重新验正其有效性之前不能用于响应客户端请求)
    no-store:           所有内容都不会缓存，强制缓存，对比缓存都不会触发（基本不用）
no-cache 不用本地的强制缓存，服务端可以缓存，no-store 本地强制缓存和服务端的协商缓存都不用。基本用不到

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br><span class="line-number">7</span><br><span class="line-number">8</span><br><span class="line-number">9</span><br><span class="line-number">10</span><br><span class="line-number">11</span><br><span class="line-number">12</span><br><span class="line-number">13</span><br><span class="line-number">14</span><br><span class="line-number">15</span><br><span class="line-number">16</span><br><span class="line-number">17</span><br></div></div><p>图中Cache-Control仅指定了max-age，所以默认为private，缓存时间为31536000秒（365天）
也就是说，在365天内再次请求这条数据，都会直接获取缓存数据库中的数据，直接使用。</p>
<h3 id="对比缓存" tabindex="-1"><a class="header-anchor" href="#对比缓存" aria-hidden="true">#</a> 对比缓存</h3>
<blockquote>
<p>对比缓存，顾名思义，需要进行比较判断是否可以使用缓存。
浏览器第一次请求数据时，服务器会将缓存标识与数据一起返回给客户端，客户端将二者备份至缓存数据库中。
再次请求数据时，客户端将备份的缓存标识发送给服务器，服务器根据缓存标识进行判断，判断成功后，返回304状态码，通知客户端比较成功，可以使用缓存数据。</p>
</blockquote>
<h4 id="etag-if-none-match-优先级高于last-modified-if-modified-since" tabindex="-1"><a class="header-anchor" href="#etag-if-none-match-优先级高于last-modified-if-modified-since" aria-hidden="true">#</a> Etag  /  If-None-Match（优先级高于Last-Modified  /  If-Modified-Since）</h4>
<p>Etag：</p>
<p>服务器响应请求时，告诉浏览器当前资源在服务器的唯一标识（生成规则由服务器决定）。</p>
<p>If-None-Match：</p>
<p>再次请求服务器时，通过此字段通知服务器客户段缓存数据的唯一标识。
服务器收到请求后发现有头If-None-Match 则与被请求资源的唯一标识进行比对，
不同，说明资源又被改动过，则响应整片资源内容，返回状态码200；
相同，说明资源无新修改，则响应HTTP 304，告知浏览器继续使用所保存的cache。</p>
<h2 id="总结" tabindex="-1"><a class="header-anchor" href="#总结" aria-hidden="true">#</a> 总结</h2>
<p>我们可以看到两类缓存规则的不同，强制缓存如果生效，不需要再和服务器发生交互，而对比缓存不管是否生效，都需要与服务端发生交互。
两类缓存规则可以同时存在，强制缓存优先级高于对比缓存，也就是说，当执行强制缓存的规则时，如果缓存生效，直接使用缓存，不再执行对比缓存规则。</p>
<p><b>对于强制缓存，服务器通知浏览器一个缓存时间，在缓存时间内，下次请求，直接用缓存，不在时间内，执行比较缓存策略。
对于比较缓存，将缓存信息中的Etag和Last-Modified通过请求发送给服务器，由服务器校验，返回304状态码时，浏览器直接使用缓存。</b></p>
<h1 id="几种刷新与缓存的关系" tabindex="-1"><a class="header-anchor" href="#几种刷新与缓存的关系" aria-hidden="true">#</a> 几种刷新与缓存的关系</h1>
<blockquote>
<p>1.正常操作 强制缓存有效，协商缓存有效
2.手动刷新 强制缓存失效，协商缓存有效
3.强制刷新 强制缓存失效，协商缓存失效</p>
</blockquote>
</template>
