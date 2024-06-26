<template><h2 id="jwt-json-web-token" tabindex="-1"><a class="header-anchor" href="#jwt-json-web-token" aria-hidden="true">#</a> JWT（JSON Web Token）</h2>
<p>本质就是一个字符串书写规范，如下图，作用是用来在用户和服务器之间传递安全可靠的信息</p>
<p>使用token鉴权机制用于身份验证是最常见的方案流程如下：</p>
<p>服务器当验证用户账号和密码正确的时候，给用户颁发一个令牌，这个令牌作为后续用户访问一些接口的凭证
后续访问会根据这个令牌判断用户时候有权限进行访问</p>
<p>Token，分成了三部分，头部（Header）、载荷（Payload）、签名（Signature），并以.进行拼接。其中头部和载荷都是以JSON格式存放数据，只是进行了编码</p>
<h2 id="header" tabindex="-1"><a class="header-anchor" href="#header" aria-hidden="true">#</a> #header</h2>
<p>每个JWT都会带有头部信息，这里主要声明使用的算法。声明算法的字段名为alg，同时还有一个typ的字段，默认JWT即可。以下示例中算法为HS256</p>
<p>{  &quot;alg&quot;: &quot;HS256&quot;,  &quot;typ&quot;: &quot;JWT&quot; }
因为JWT是字符串，所以我们还需要对以上内容进行Base64编码，编码后字符串如下：</p>
<p>eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9</p>
<h3 id="payload" tabindex="-1"><a class="header-anchor" href="#payload" aria-hidden="true">#</a> #payload</h3>
<p>载荷即消息体，这里会存放实际的内容，也就是Token的数据声明，例如用户的id和name，默认情况下也会携带令牌的签发时间iat，通过还可以设置过期时间，如下：</p>
<p>{
&quot;sub&quot;: &quot;1234567890&quot;,
&quot;name&quot;: &quot;John Doe&quot;,
&quot;iat&quot;: 1516239022
}
同样进行Base64编码后，字符串如下：</p>
<p>eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ</p>
<h2 id="signature" tabindex="-1"><a class="header-anchor" href="#signature" aria-hidden="true">#</a> #Signature</h2>
<p>签名是对头部和载荷内容进行签名，一般情况，设置一个secretKey，对前两个的结果进行HMACSHA25算法，公式如下：</p>
<p>Signature = HMACSHA256(base64Url(header)+.+base64Url(payload),secretKey)
一旦前面两部分数据被篡改，只要服务器加密用的密钥没有泄露，得到的签名肯定和之前的签名不一致</p>
<p>#二、如何实现
Token的使用分成了两部分：</p>
<p>生成token：登录成功的时候，颁发token
验证token：访问某些资源或者接口时，验证token
#生成 token
借助第三方库jsonwebtoken，通过jsonwebtoken 的 sign 方法生成一个 token：</p>
<p>第一个参数指的是 Payload</p>
<p>第二个是秘钥，服务端特有</p>
<p>第三个参数是 option，可以定义 token 过期时间</p>
<p>const crypto = require(&quot;crypto&quot;),
jwt = require(&quot;jsonwebtoken&quot;);
// TODO:使用数据库
// 这里应该是用数据库存储，这里只是演示用</p>
<div class="language-javascript ext-js line-numbers-mode"><pre v-pre class="language-javascript"><code><span class="token keyword">let</span> userList <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span>

<span class="token keyword">class</span> <span class="token class-name">UserController</span> <span class="token punctuation">{</span>
  <span class="token comment">// 用户登录</span>
  <span class="token keyword">static</span> <span class="token keyword">async</span> <span class="token function">login</span><span class="token punctuation">(</span><span class="token parameter">ctx</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">const</span> data <span class="token operator">=</span> ctx<span class="token punctuation">.</span>request<span class="token punctuation">.</span>body<span class="token punctuation">;</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span>data<span class="token punctuation">.</span>name <span class="token operator">||</span> <span class="token operator">!</span>data<span class="token punctuation">.</span>password<span class="token punctuation">)</span> <span class="token punctuation">{</span>
      <span class="token keyword">return</span> ctx<span class="token punctuation">.</span>body <span class="token operator">=</span> <span class="token punctuation">{</span>
        <span class="token literal-property property">code</span><span class="token operator">:</span> <span class="token string">"000002"</span><span class="token punctuation">,</span> 
        <span class="token literal-property property">message</span><span class="token operator">:</span> <span class="token string">"参数不合法"</span>
      <span class="token punctuation">}</span>
    <span class="token punctuation">}</span>
    <span class="token keyword">const</span> result <span class="token operator">=</span> userList<span class="token punctuation">.</span><span class="token function">find</span><span class="token punctuation">(</span><span class="token parameter">item</span> <span class="token operator">=></span> item<span class="token punctuation">.</span>name <span class="token operator">===</span> data<span class="token punctuation">.</span>name <span class="token operator">&amp;&amp;</span> item<span class="token punctuation">.</span>password <span class="token operator">===</span> crypto<span class="token punctuation">.</span><span class="token function">createHash</span><span class="token punctuation">(</span><span class="token string">'md5'</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">update</span><span class="token punctuation">(</span>data<span class="token punctuation">.</span>password<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">digest</span><span class="token punctuation">(</span><span class="token string">'hex'</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span>result<span class="token punctuation">)</span> <span class="token punctuation">{</span>
      <span class="token comment">// 生成token</span>
      <span class="token keyword">const</span> token <span class="token operator">=</span> jwt<span class="token punctuation">.</span><span class="token function">sign</span><span class="token punctuation">(</span>  
        <span class="token punctuation">{</span>
          <span class="token literal-property property">name</span><span class="token operator">:</span> result<span class="token punctuation">.</span>name
        <span class="token punctuation">}</span><span class="token punctuation">,</span>
        <span class="token string">"test_token"</span><span class="token punctuation">,</span> <span class="token comment">// secret</span>
        <span class="token punctuation">{</span> <span class="token literal-property property">expiresIn</span><span class="token operator">:</span> <span class="token number">60</span> <span class="token operator">*</span> <span class="token number">60</span> <span class="token punctuation">}</span> <span class="token comment">// 过期时间：60 * 60 s</span>
      <span class="token punctuation">)</span><span class="token punctuation">;</span>
      <span class="token keyword">return</span> ctx<span class="token punctuation">.</span>body <span class="token operator">=</span> <span class="token punctuation">{</span>
        <span class="token literal-property property">code</span><span class="token operator">:</span> <span class="token string">"0"</span><span class="token punctuation">,</span>
        <span class="token literal-property property">message</span><span class="token operator">:</span> <span class="token string">"登录成功"</span><span class="token punctuation">,</span>
        <span class="token literal-property property">data</span><span class="token operator">:</span> <span class="token punctuation">{</span>
          token
        <span class="token punctuation">}</span>
      <span class="token punctuation">}</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span> <span class="token keyword">else</span> <span class="token punctuation">{</span>
      <span class="token keyword">return</span> ctx<span class="token punctuation">.</span>body <span class="token operator">=</span> <span class="token punctuation">{</span>
        <span class="token literal-property property">code</span><span class="token operator">:</span> <span class="token string">"000002"</span><span class="token punctuation">,</span>
        <span class="token literal-property property">message</span><span class="token operator">:</span> <span class="token string">"用户名或密码错误"</span>
      <span class="token punctuation">}</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
  <span class="token punctuation">}</span>
<span class="token punctuation">}</span>

module<span class="token punctuation">.</span>exports <span class="token operator">=</span> UserController<span class="token punctuation">;</span>

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br><span class="line-number">7</span><br><span class="line-number">8</span><br><span class="line-number">9</span><br><span class="line-number">10</span><br><span class="line-number">11</span><br><span class="line-number">12</span><br><span class="line-number">13</span><br><span class="line-number">14</span><br><span class="line-number">15</span><br><span class="line-number">16</span><br><span class="line-number">17</span><br><span class="line-number">18</span><br><span class="line-number">19</span><br><span class="line-number">20</span><br><span class="line-number">21</span><br><span class="line-number">22</span><br><span class="line-number">23</span><br><span class="line-number">24</span><br><span class="line-number">25</span><br><span class="line-number">26</span><br><span class="line-number">27</span><br><span class="line-number">28</span><br><span class="line-number">29</span><br><span class="line-number">30</span><br><span class="line-number">31</span><br><span class="line-number">32</span><br><span class="line-number">33</span><br><span class="line-number">34</span><br><span class="line-number">35</span><br><span class="line-number">36</span><br><span class="line-number">37</span><br><span class="line-number">38</span><br><span class="line-number">39</span><br><span class="line-number">40</span><br></div></div><p>在前端接收到token后，一般情况会通过localStorage进行缓存，然后将token放到HTTP请求头Authorization 中，关于Authorization 的设置，前面要加上 Bearer ，注意后面带有空格</p>
<div class="language-javascript ext-js line-numbers-mode"><pre v-pre class="language-javascript"><code>axios<span class="token punctuation">.</span>interceptors<span class="token punctuation">.</span>request<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span><span class="token parameter">config</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
  <span class="token keyword">const</span> token <span class="token operator">=</span> localStorage<span class="token punctuation">.</span><span class="token function">getItem</span><span class="token punctuation">(</span><span class="token string">'token'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  config<span class="token punctuation">.</span>headers<span class="token punctuation">.</span>common<span class="token punctuation">[</span><span class="token string">'Authorization'</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token string">'Bearer '</span> <span class="token operator">+</span> token<span class="token punctuation">;</span> <span class="token comment">// 留意这里的 Authorization</span>
  <span class="token keyword">return</span> config<span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span>
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br></div></div><p>#校验token
使用 koa-jwt 中间件进行验证，方式比较简单</p>
<p>/ 注意：放在路由前面</p>
<div class="language-javascript ext-js line-numbers-mode"><pre v-pre class="language-javascript"><code>app<span class="token punctuation">.</span><span class="token function">use</span><span class="token punctuation">(</span><span class="token function">koajwt</span><span class="token punctuation">(</span><span class="token punctuation">{</span>
  <span class="token literal-property property">secret</span><span class="token operator">:</span> <span class="token string">'test_token'</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">unless</span><span class="token punctuation">(</span><span class="token punctuation">{</span> <span class="token comment">// 配置白名单</span>
  <span class="token literal-property property">path</span><span class="token operator">:</span> <span class="token punctuation">[</span><span class="token regex"><span class="token regex-delimiter">/</span><span class="token regex-source language-regex">\/api\/register</span><span class="token regex-delimiter">/</span></span><span class="token punctuation">,</span> <span class="token regex"><span class="token regex-delimiter">/</span><span class="token regex-source language-regex">\/api\/login</span><span class="token regex-delimiter">/</span></span><span class="token punctuation">]</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br></div></div><p>secret 必须和 sign 时候保持一致
可以通过 unless 配置接口白名单，也就是哪些 URL 可以不用经过校验，像登陆/注册都可以不用校验
校验的中间件需要放在需要校验的路由前面，无法对前面的 URL 进行校验
获取token用户的信息方法如下：</p>
<div class="language-javascript ext-js line-numbers-mode"><pre v-pre class="language-javascript"><code>router<span class="token punctuation">.</span><span class="token function">get</span><span class="token punctuation">(</span><span class="token string">'/api/userInfo'</span><span class="token punctuation">,</span><span class="token keyword">async</span> <span class="token punctuation">(</span><span class="token parameter">ctx<span class="token punctuation">,</span>next</span><span class="token punctuation">)</span> <span class="token operator">=></span><span class="token punctuation">{</span>
    <span class="token keyword">const</span> authorization <span class="token operator">=</span>  ctx<span class="token punctuation">.</span>header<span class="token punctuation">.</span>authorization <span class="token comment">// 获取jwt</span>
    <span class="token keyword">const</span> token <span class="token operator">=</span> authorization<span class="token punctuation">.</span><span class="token function">replace</span><span class="token punctuation">(</span><span class="token string">'Beraer '</span><span class="token punctuation">,</span><span class="token string">''</span><span class="token punctuation">)</span>
    <span class="token keyword">const</span> result <span class="token operator">=</span> jwt<span class="token punctuation">.</span><span class="token function">verify</span><span class="token punctuation">(</span>token<span class="token punctuation">,</span><span class="token string">'test_token'</span><span class="token punctuation">)</span>
    ctx<span class="token punctuation">.</span>body <span class="token operator">=</span> result

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br></div></div><p>注意：上述的HMA256加密算法为单秘钥的形式，一旦泄露后果非常的危险</p>
<p>在分布式系统中，每个子系统都要获取到秘钥，那么这个子系统根据该秘钥可以发布和验证令牌，但有些服务器只需要验证令牌</p>
<p>这时候可以采用非对称加密，利用私钥发布令牌，公钥验证令牌，加密算法可以选择RS256</p>
<p>#三、优缺点
优点：</p>
<p>json具有通用性，所以可以跨语言
组成简单，字节占用小，便于传输
服务端无需保存会话信息，很容易进行水平扩展
一处生成，多处使用，可以在分布式系统中，解决单点登录问题
可防护CSRF攻击
缺点：</p>
<p>payload部分仅仅是进行简单编码，所以只能用于存储逻辑必需的非敏感信息
需要保护好加密密钥，一旦泄露后果不堪设想
为避免token被劫持，最好使用https协议</p>
</template>
