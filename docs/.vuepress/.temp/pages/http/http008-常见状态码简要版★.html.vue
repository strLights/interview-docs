<template><h1 id="常见状态码" tabindex="-1"><a class="header-anchor" href="#常见状态码" aria-hidden="true">#</a> 常见状态码</h1>
<h2 id="_1xx-服务器接收请求" tabindex="-1"><a class="header-anchor" href="#_1xx-服务器接收请求" aria-hidden="true">#</a> 1XX 服务器接收请求</h2>
<h2 id="_2xx-请求成功-如-200" tabindex="-1"><a class="header-anchor" href="#_2xx-请求成功-如-200" aria-hidden="true">#</a> 2XX 请求成功 如 200</h2>
<h2 id="_3xx-重定向-如-302" tabindex="-1"><a class="header-anchor" href="#_3xx-重定向-如-302" aria-hidden="true">#</a> 3XX 重定向 如 302</h2>
<h2 id="_4xx-客户端错误-如-404" tabindex="-1"><a class="header-anchor" href="#_4xx-客户端错误-如-404" aria-hidden="true">#</a> 4XX 客户端错误 如 404</h2>
<h2 id="_5xx-服务端错误-如-500" tabindex="-1"><a class="header-anchor" href="#_5xx-服务端错误-如-500" aria-hidden="true">#</a> 5XX 服务端错误 如 500</h2>
<p>##常见状态码</p>
<p>200 请求成功</p>
<p>301 永久重定向 （配合location，浏览器自动处理）
比如有个网站的域名到期了，而且不用了，我们就可以把老的域名定到新域名下</p>
<p>302 临时重定向 （配合location，浏览器自动处理）</p>
<p>比如百度一个网站，然后打开，检查代码时候，会发现这是个百度的地址，打开这个地址然后重定向到你要访问的地址。</p>
<p>304</p>
<p>比如访问之前一个打开的页面，一些css的js的链接请求，代码都没有改变，返回304，用浏览器缓存的即可，不用获取新的资源。</p>
<p>404 资源访问失败</p>
<p>403 没有权限</p>
<p>500 服务端错误</p>
<p>503 网管超时</p>
</template>
