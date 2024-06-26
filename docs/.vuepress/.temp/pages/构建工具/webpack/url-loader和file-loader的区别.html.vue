<template><h1 id="url-loader和file-loader的区别" tabindex="-1"><a class="header-anchor" href="#url-loader和file-loader的区别" aria-hidden="true">#</a> url-loader和file-loader的区别</h1>
<h3 id="什么是-url-loader" tabindex="-1"><a class="header-anchor" href="#什么是-url-loader" aria-hidden="true">#</a> 什么是 url-loader</h3>
<p>url-loader 会将引入的文件进行编码，生成 DataURL，相当于把文件翻译成了一串字符串，再把这个字符串打包到 JavaScript。</p>
<pre><code>使用 base64 来加载图片也是有两面性的：

优点：节省请求，提高页面性能
缺点：增大本地文件大小，降低加载性能
所以我们得有取舍，只对部分小 size 的图片进行 base64 编码，其它的大图片还是发请求吧。
</code></pre>
<h3 id="什么是-file-loader" tabindex="-1"><a class="header-anchor" href="#什么是-file-loader" aria-hidden="true">#</a> 什么是 file-loader</h3>
<p>在css文件中定义background的属性或者在html中引入image的src，我们知道在webpack打包后这些图片会打包至定义好的一个文件夹下，和开发时候的相对路径会不一样，这就会导致导入图片路径的错误。而file-loader正是为了解决此类问题而产生的，他修改打包后图片的储存路径，再根据配置修改我们引用的路径，使之对应引入。</p>
<h2 id="两者之间的联系" tabindex="-1"><a class="header-anchor" href="#两者之间的联系" aria-hidden="true">#</a> 两者之间的联系</h2>
<p>url-loader内部封装了 file-loader。url-loader不依赖于file-loader，即使用url-loader时，只需要安装url-loader即可，不需要安装file-loader。</p>
<h1 id="总结" tabindex="-1"><a class="header-anchor" href="#总结" aria-hidden="true">#</a> 总结</h1>
<p>通过上面的介绍，我们可以看到，url-loader工作分两种情况：</p>
<p>文件大小小于limit参数，url-loader将会把文件转为DataURL； 文件大小大于limit，url-loader会调用file-loader进行处理，参数也会直接传给file-loader。因此我们只需要安装url-loader即可。</p>
<p>工程中配置</p>
<p>如下：webpack.config.js</p>
<div class="language-javascript ext-js line-numbers-mode"><pre v-pre class="language-javascript"><code>module<span class="token punctuation">.</span>exports <span class="token operator">=</span> <span class="token punctuation">(</span><span class="token punctuation">{</span>
    <span class="token operator">...</span>
    <span class="token literal-property property">module</span> <span class="token operator">:</span> <span class="token punctuation">{</span>
        <span class="token literal-property property">rules</span><span class="token operator">:</span> <span class="token punctuation">[</span>
            <span class="token punctuation">{</span>
                <span class="token comment">// 小于10k的图片在img下不会有图片文件，而是直接把图片的base64值写到html引入图片的地方</span>
                <span class="token comment">// 大于10k的图片会放在img下，需要的时候通过http请求下载</span>
                <span class="token literal-property property">test</span><span class="token operator">:</span> <span class="token regex"><span class="token regex-delimiter">/</span><span class="token regex-source language-regex">\.(png|jpe?g|gif|svg)(\?.*)?$</span><span class="token regex-delimiter">/</span></span><span class="token punctuation">,</span>
                <span class="token literal-property property">loader</span><span class="token operator">:</span> <span class="token string">'url-loader'</span><span class="token punctuation">,</span>
                <span class="token literal-property property">options</span><span class="token operator">:</span> <span class="token punctuation">{</span>
                    <span class="token literal-property property">limit</span><span class="token operator">:</span> <span class="token number">10000</span><span class="token punctuation">,</span>
                    <span class="token literal-property property">name</span><span class="token operator">:</span> utils<span class="token punctuation">.</span><span class="token function">assetsPath</span><span class="token punctuation">(</span><span class="token string">'img/[name].[hash:7].[ext]'</span><span class="token punctuation">)</span>
                <span class="token punctuation">}</span>
            <span class="token punctuation">}</span><span class="token punctuation">,</span>
            <span class="token punctuation">{</span>
                <span class="token literal-property property">test</span><span class="token operator">:</span> <span class="token regex"><span class="token regex-delimiter">/</span><span class="token regex-source language-regex">(\.(eot|ttf|woff|woff2|otf)|font)$</span><span class="token regex-delimiter">/</span></span><span class="token punctuation">,</span>
                <span class="token literal-property property">loader</span><span class="token operator">:</span> <span class="token string">'file-loader'</span><span class="token punctuation">,</span>
                <span class="token literal-property property">options</span><span class="token operator">:</span> <span class="token punctuation">{</span> <span class="token literal-property property">outputPath</span><span class="token operator">:</span> <span class="token string">'fonts/'</span> <span class="token punctuation">}</span>
            <span class="token punctuation">}</span>
        <span class="token punctuation">]</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span><span class="token punctuation">)</span>

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br><span class="line-number">7</span><br><span class="line-number">8</span><br><span class="line-number">9</span><br><span class="line-number">10</span><br><span class="line-number">11</span><br><span class="line-number">12</span><br><span class="line-number">13</span><br><span class="line-number">14</span><br><span class="line-number">15</span><br><span class="line-number">16</span><br><span class="line-number">17</span><br><span class="line-number">18</span><br><span class="line-number">19</span><br><span class="line-number">20</span><br><span class="line-number">21</span><br><span class="line-number">22</span><br><span class="line-number">23</span><br></div></div></template>
