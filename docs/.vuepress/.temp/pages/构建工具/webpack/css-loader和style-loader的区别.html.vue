<template><div class="language-javascript ext-js line-numbers-mode"><pre v-pre class="language-javascript"><code>webpack是用<span class="token constant">JS</span>写的，运行在node环境，所以默认webpack打包的时候只会处理<span class="token constant">JS</span>之间的依赖关系。

因为像 <span class="token punctuation">.</span>css 这样的文件不是一个 JavaScript 模块，你需要配置 webpack 使用 css<span class="token operator">-</span>loader 和 style<span class="token operator">-</span>loader 去合理地处理它们。



如果在<span class="token constant">JS</span>中导入了css，那么就需要使用 css<span class="token operator">-</span>loader 来识别这个模块，通过特定的语法规则进行转换内容最后导出。

css<span class="token operator">-</span>loader会处理 <span class="token keyword">import</span> <span class="token operator">/</span> require @<span class="token keyword">import</span> <span class="token operator">/</span> url 引入的内容。
js
<span class="token comment">// base.css</span>
<span class="token punctuation">.</span>bg <span class="token punctuation">{</span>
  <span class="token literal-property property">background</span><span class="token operator">:</span> #<span class="token number">000</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
<span class="token keyword">const</span> style <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'./base.css'</span><span class="token punctuation">)</span>
console<span class="token punctuation">.</span><span class="token function">log</span><span class="token punctuation">(</span>style<span class="token punctuation">,</span> <span class="token string">'css'</span><span class="token punctuation">)</span>



css<span class="token operator">-</span>loader处理之后导出的是一个数组

但是这并不是我们想要的，因为是个数组，页面是无法直接使用，这时我们需要用到零外一个style<span class="token operator">-</span>loader来处理

style<span class="token operator">-</span>loader 是通过一个<span class="token constant">JS</span>脚本创建一个style标签，里面包含一些样式。style<span class="token operator">-</span>loader是不能单独使用的，应为它并不负责解析 css 之前的依赖关系，每个loader的功能都是单一的，各自拆分独立。


## style<span class="token operator">-</span>loader和css<span class="token operator">-</span>loader作用是不同的。

<span class="token operator">></span>  <span class="token number">1</span>、css<span class="token operator">-</span>loader<span class="token operator">:</span> 加载<span class="token punctuation">.</span>css文件

<span class="token operator">></span>  <span class="token number">2</span>、style<span class="token operator">-</span>loader：使用<span class="token operator">&lt;</span>style<span class="token operator">></span>将css<span class="token operator">-</span>loader内部样式注入到我们的<span class="token constant">HTML</span>页面


由于webpack只能处理js相关的文件，所以像图片和css资源是处理不了的，css<span class="token operator">-</span>loader的作用是将css文件转换成webpack能够处理的资源，而style<span class="token operator">-</span>loader就是帮我们直接将css<span class="token operator">-</span>loader解析后的内容挂载到html页面当中。


 css<span class="token operator">-</span>loader帮助我们解析css成为js对象
 sytle<span class="token operator">-</span>loader可以从css<span class="token operator">-</span>loader解析的对象中提取css样式挂载到页面当中


 ### less<span class="token operator">-</span>loader

Less是<span class="token constant">CSS</span>预处理语言，扩展了<span class="token constant">CSS</span>语言，增加了变量、Mixin、函数等特性，Less<span class="token operator">-</span>loader的作用就是将less代码转译为浏览器可以识别的<span class="token constant">CSS</span>代码。
less
<span class="token comment">// demo.less</span>
@base<span class="token operator">:</span> #f938ab<span class="token punctuation">;</span>

<span class="token punctuation">.</span>box<span class="token operator">-</span><span class="token function">shadow</span><span class="token punctuation">(</span>@style<span class="token punctuation">,</span> @c<span class="token punctuation">)</span> <span class="token function">when</span> <span class="token punctuation">(</span><span class="token parameter"><span class="token function">iscolor</span><span class="token punctuation">(</span>@c<span class="token punctuation">)</span></span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token operator">-</span>webkit<span class="token operator">-</span>box<span class="token operator">-</span>shadow<span class="token operator">:</span> @style @c<span class="token punctuation">;</span>
  box<span class="token operator">-</span>shadow<span class="token operator">:</span>         @style @c<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
<span class="token punctuation">.</span>box<span class="token operator">-</span><span class="token function">shadow</span><span class="token punctuation">(</span>@style<span class="token punctuation">,</span> @alpha<span class="token operator">:</span> <span class="token number">50</span><span class="token operator">%</span><span class="token punctuation">)</span> <span class="token function">when</span> <span class="token punctuation">(</span><span class="token parameter"><span class="token function">isnumber</span><span class="token punctuation">(</span>@alpha<span class="token punctuation">)</span></span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token punctuation">.</span>box<span class="token operator">-</span><span class="token function">shadow</span><span class="token punctuation">(</span>@style<span class="token punctuation">,</span> <span class="token function">rgba</span><span class="token punctuation">(</span><span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> @alpha<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>
<span class="token punctuation">.</span>box <span class="token punctuation">{</span>
  <span class="token literal-property property">color</span><span class="token operator">:</span> <span class="token function">saturate</span><span class="token punctuation">(</span>@base<span class="token punctuation">,</span> <span class="token number">5</span><span class="token operator">%</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  border<span class="token operator">-</span>color<span class="token operator">:</span> <span class="token function">lighten</span><span class="token punctuation">(</span>@base<span class="token punctuation">,</span> <span class="token number">30</span><span class="token operator">%</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  div <span class="token punctuation">{</span> <span class="token punctuation">.</span>box<span class="token operator">-</span><span class="token function">shadow</span><span class="token punctuation">(</span><span class="token number">0</span> <span class="token number">0</span> 5px<span class="token punctuation">,</span> <span class="token number">30</span><span class="token operator">%</span><span class="token punctuation">)</span> <span class="token punctuation">}</span>
<span class="token punctuation">}</span>


上面的less代码会被less<span class="token operator">-</span>loader转译为：
css
<span class="token comment">// demo.css</span>
<span class="token punctuation">.</span>box <span class="token punctuation">{</span>
  <span class="token literal-property property">color</span><span class="token operator">:</span> #fe33ac<span class="token punctuation">;</span>
  border<span class="token operator">-</span>color<span class="token operator">:</span> #fdcdea<span class="token punctuation">;</span>
<span class="token punctuation">}</span>
<span class="token punctuation">.</span>box div <span class="token punctuation">{</span>
  <span class="token operator">-</span>webkit<span class="token operator">-</span>box<span class="token operator">-</span>shadow<span class="token operator">:</span> <span class="token number">0</span> <span class="token number">0</span> 5px <span class="token function">rgba</span><span class="token punctuation">(</span><span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0.3</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
  box<span class="token operator">-</span>shadow<span class="token operator">:</span> <span class="token number">0</span> <span class="token number">0</span> 5px <span class="token function">rgba</span><span class="token punctuation">(</span><span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0</span><span class="token punctuation">,</span> <span class="token number">0.3</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>



所以less<span class="token operator">-</span>loader的原理很简单，就是调用less库提供的方法，转译less语法后输出，如下：
js
<span class="token comment">// less-loader实现（经简化）</span>
<span class="token keyword">const</span> less <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'less'</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

module<span class="token punctuation">.</span><span class="token function-variable function">exports</span> <span class="token operator">=</span> <span class="token keyword">function</span><span class="token punctuation">(</span><span class="token parameter">content</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token keyword">const</span> callback <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span><span class="token function">async</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 转译比较耗时，采用异步方式</span>
  <span class="token keyword">const</span> options <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span><span class="token function">getOptions</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 获取配置文件中less-loader的options</span>
  
  less<span class="token punctuation">.</span><span class="token function">render</span><span class="token punctuation">(</span>
    content<span class="token punctuation">,</span>
    <span class="token function">createOptions</span><span class="token punctuation">(</span>options<span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token comment">// less转译的配置</span>
    <span class="token punctuation">(</span><span class="token parameter">err<span class="token punctuation">,</span> output</span><span class="token punctuation">)</span> <span class="token operator">=></span> <span class="token punctuation">{</span>
      <span class="token function">callback</span><span class="token punctuation">(</span>err<span class="token punctuation">,</span> output<span class="token punctuation">.</span>css<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 将生成的css代码传递给下一个loader</span>
    <span class="token punctuation">}</span>
  <span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>


### css<span class="token operator">-</span>loader

Css<span class="token operator">-</span>loader的作用主要是解析css文件中的@<span class="token keyword">import</span>和url语句，处理css<span class="token operator">-</span>modules，并将结果作为一个js模块返回。
假如我们有a<span class="token punctuation">.</span>css、b<span class="token punctuation">.</span>css、c<span class="token punctuation">.</span>css：


<span class="token comment">// a.css</span>
css

@<span class="token keyword">import</span> <span class="token string">'./b.css'</span><span class="token punctuation">;</span> <span class="token comment">// 导入b.css</span>
<span class="token punctuation">.</span>a <span class="token punctuation">{</span>
  font<span class="token operator">-</span>size<span class="token operator">:</span> 16px<span class="token punctuation">;</span>
<span class="token punctuation">}</span>




<span class="token comment">// b.css</span>
css

@<span class="token keyword">import</span> <span class="token string">'./c.css'</span><span class="token punctuation">;</span> <span class="token comment">// 导入c.css</span>
<span class="token punctuation">.</span>b <span class="token punctuation">{</span>
  <span class="token literal-property property">color</span><span class="token operator">:</span> red<span class="token punctuation">;</span>
<span class="token punctuation">}</span>




<span class="token comment">// c.css</span>
css

<span class="token punctuation">.</span>c <span class="token punctuation">{</span>
  font<span class="token operator">-</span>weight<span class="token operator">:</span> bolder<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

来看看css<span class="token operator">-</span>loader对a<span class="token punctuation">.</span>css的编译输出：

js


<span class="token comment">// css-loader输出</span>

exports <span class="token operator">=</span> module<span class="token punctuation">.</span>exports <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">"../../../node_modules/css-loader/lib/css-base.js"</span><span class="token punctuation">)</span><span class="token punctuation">(</span><span class="token boolean">false</span><span class="token punctuation">)</span><span class="token punctuation">;</span>


<span class="token comment">// imports</span>
<span class="token comment">// 文件需要的依赖js模块，这里为空</span>

<span class="token comment">// module</span>
exports<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span><span class="token punctuation">[</span> <span class="token comment">// 模块导出内容</span>
  module<span class="token punctuation">.</span>id<span class="token punctuation">,</span> 
  <span class="token string">".src-components-Home-index__c--3riXS {\n  font-weight: bolder;\n}\n.src-components-Home-index__b--I-yI3 {\n  color: red;\n}\n.src-components-Home-index__a--3EFPE {\n  font-size: 16px;\n}\n"</span><span class="token punctuation">,</span> 
  <span class="token string">""</span>
<span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span> 

<span class="token comment">// exports</span>
exports<span class="token punctuation">.</span>locals <span class="token operator">=</span> <span class="token punctuation">{</span> <span class="token comment">// css-modules的类名映射</span>
  <span class="token string-property property">"c"</span><span class="token operator">:</span> <span class="token string">"src-components-Home-index__c--3riXS"</span><span class="token punctuation">,</span>
  <span class="token string-property property">"b"</span><span class="token operator">:</span> <span class="token string">"src-components-Home-index__b--I-yI3"</span><span class="token punctuation">,</span>
  <span class="token string-property property">"a"</span><span class="token operator">:</span> <span class="token string">"src-components-Home-index__a--3EFPE"</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>



可以理解为css<span class="token operator">-</span>loader将a<span class="token punctuation">.</span>css、b<span class="token punctuation">.</span>css和c<span class="token punctuation">.</span>css的样式内容以字符串的形式拼接在一起，并将其作为js模块的导出内容。

####  css<span class="token operator">-</span>loader源码（经简化）

js
<span class="token comment">// https://github.com/webpack-contrib/css-loader/blob/master/src/index.js</span>
<span class="token keyword">import</span> postcss <span class="token keyword">from</span> <span class="token string">'postcss'</span><span class="token punctuation">;</span>

module<span class="token punctuation">.</span><span class="token function-variable function">exports</span> <span class="token operator">=</span> <span class="token keyword">async</span> <span class="token keyword">function</span> <span class="token punctuation">(</span><span class="token parameter">content<span class="token punctuation">,</span> map<span class="token punctuation">,</span> meta</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token keyword">const</span> options <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span><span class="token function">getOptions</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 获取配置</span>

  <span class="token keyword">const</span> plugins <span class="token operator">=</span> <span class="token punctuation">[</span><span class="token punctuation">]</span><span class="token punctuation">;</span> <span class="token comment">// 转译源码所需的postcss插件</span>
  <span class="token function">shouldUseModulesPlugins</span><span class="token punctuation">(</span>options<span class="token punctuation">,</span> <span class="token keyword">this</span><span class="token punctuation">)</span> <span class="token operator">&amp;&amp;</span> plugins<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>modulesPlugins<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 处理css-modules</span>
  <span class="token function">shouldUseImportPlugin</span><span class="token punctuation">(</span>options<span class="token punctuation">,</span> <span class="token keyword">this</span><span class="token punctuation">)</span> <span class="token operator">&amp;&amp;</span> plugins<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>importPlugin<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 处理@import语句</span>
  <span class="token function">shouldUseURLPlugin</span><span class="token punctuation">(</span>options<span class="token punctuation">,</span> <span class="token keyword">this</span><span class="token punctuation">)</span> <span class="token operator">&amp;&amp;</span> plugins<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>urlPlugin<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 处理url()语句</span>
  <span class="token function">shouldUseIcssPlugin</span><span class="token punctuation">(</span>options<span class="token punctuation">,</span> <span class="token keyword">this</span><span class="token punctuation">)</span> <span class="token operator">&amp;&amp;</span> plugins<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>icssPlugin<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 处理icss相关逻辑</span>

  <span class="token keyword">if</span> <span class="token punctuation">(</span>meta <span class="token operator">&amp;&amp;</span> meta<span class="token punctuation">.</span>ast<span class="token punctuation">)</span> <span class="token punctuation">{</span> <span class="token comment">// 复用前面loader生成的CSS AST（如postcss-loader）</span>
    content <span class="token operator">=</span> meta<span class="token punctuation">.</span>ast<span class="token punctuation">.</span>root<span class="token punctuation">;</span>
  <span class="token punctuation">}</span>

  <span class="token keyword">const</span> result <span class="token operator">=</span> <span class="token keyword">await</span> <span class="token function">postcss</span><span class="token punctuation">(</span>plugins<span class="token punctuation">)</span><span class="token punctuation">.</span><span class="token function">process</span><span class="token punctuation">(</span>content<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 使用postcss转译源码</span>

  <span class="token keyword">const</span> importCode <span class="token operator">=</span> <span class="token function">getImportCode</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 需要导入的依赖语句</span>
  <span class="token keyword">const</span> moduleCode <span class="token operator">=</span> <span class="token function">getModuleCode</span><span class="token punctuation">(</span>result<span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 模块导出内容</span>
  <span class="token keyword">const</span> exportCode <span class="token operator">=</span> <span class="token function">getExportCode</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 其他需要导出的信息，如css-modules的类名映射等</span>

  <span class="token keyword">const</span> callback <span class="token operator">=</span> <span class="token keyword">this</span><span class="token punctuation">.</span><span class="token function">async</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span> <span class="token comment">// 异步返回</span>
  <span class="token function">callback</span><span class="token punctuation">(</span><span class="token keyword">null</span><span class="token punctuation">,</span> <span class="token template-string"><span class="token template-punctuation string">`</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>importCode<span class="token interpolation-punctuation punctuation">}</span></span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>moduleCode<span class="token interpolation-punctuation punctuation">}</span></span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>exportCode<span class="token interpolation-punctuation punctuation">}</span></span><span class="token template-punctuation string">`</span></span><span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>



## style<span class="token operator">-</span>loader
经过css<span class="token operator">-</span>loader的转译，我们已经得到了完整的css样式代码，style<span class="token operator">-</span>loader的作用就是将结果以style标签的方式插入<span class="token constant">DOM</span>树中。
直觉上似乎我们只需要像下面这样返回一段js代码，将css<span class="token operator">-</span>loader返回的结果插入<span class="token constant">DOM</span>就行：
js
module<span class="token punctuation">.</span><span class="token function-variable function">exports</span> <span class="token operator">=</span> <span class="token keyword">function</span> <span class="token punctuation">(</span><span class="token parameter">content</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token keyword">return</span> <span class="token template-string"><span class="token template-punctuation string">`</span><span class="token string">
    const style = document.createElement('style');
    style.innerHTML = '</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>content<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">';
    document.head.appendChild(style);
  </span><span class="token template-punctuation string">`</span></span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>



但css<span class="token operator">-</span>loader返回的不是css样式代码的文本，而是一个js模块的代码，将这些js代码直接放进style标里显然是不行的。
我们来看看style<span class="token operator">-</span>loader的实现：
 style<span class="token operator">-</span>loader

 js
<span class="token keyword">import</span> loaderUtils <span class="token keyword">from</span> <span class="token string">'loader-utils'</span><span class="token punctuation">;</span>

module<span class="token punctuation">.</span><span class="token function-variable function">exports</span> <span class="token operator">=</span> <span class="token keyword">function</span> <span class="token punctuation">(</span><span class="token parameter">content</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token comment">// do nothing</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>

module<span class="token punctuation">.</span>exports<span class="token punctuation">.</span><span class="token function-variable function">pitch</span> <span class="token operator">=</span> <span class="token keyword">function</span> <span class="token punctuation">(</span><span class="token parameter">remainingRequest</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
  <span class="token comment">/*
  * 用require语句获取css-loader返回的js模块的导出
  * 用'!!'前缀跳过配置中的loader，避免重复执行
  * 用remainingRequest参数获取loader链的剩余部分，在本例中是css-loader、less-loader
  * 用loaderUtils的stringifyRequest方法将request语句中的绝对路径转为相对路径
  */</span>
  <span class="token keyword">const</span> requestPath <span class="token operator">=</span> loaderUtils<span class="token punctuation">.</span><span class="token function">stringifyRequest</span><span class="token punctuation">(</span><span class="token keyword">this</span><span class="token punctuation">,</span> <span class="token string">'!!'</span> <span class="token operator">+</span> remainingRequest<span class="token punctuation">)</span><span class="token punctuation">;</span>

  <span class="token comment">// 本例中requestPath为:</span>
  <span class="token comment">// '!!../node_modules/css-loader/index.js!../node_modules/less-loader/dist/cjs.js!src/styles/index.less'</span>

  <span class="token keyword">return</span> <span class="token template-string"><span class="token template-punctuation string">`</span><span class="token string">
    const content = require(</span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>requestPath<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">)
    const style = document.createElement('style');
    style.innerHTML = content;
    document.head.appendChild(style);
  </span><span class="token template-punctuation string">`</span></span><span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>



### style<span class="token operator">-</span>loader的几个设计思路：

css<span class="token operator">-</span>loader返回的样式只能通过其js模块的运行时得到，故使用require语句取得
normal方法实际上什么都没做，在pitch方法里中断loader链的执行，再以inline方式调用了后方的loader来加载当前的less文件
如果将pitch中的实现放到normal方法里，就会造成loader链执行两遍
如果requestPath中没有<span class="token string">'!!'</span>前缀，就会造成loader链被无限循环调用

style<span class="token operator">-</span>loader的实现逻辑比较绕，也是一个比较经典的pitch应用，理解了它的原理，就可以是说对loader的调用链、执行顺序和模块化输出等有了一个比较全面的认识，推荐细细体会。



</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br><span class="line-number">7</span><br><span class="line-number">8</span><br><span class="line-number">9</span><br><span class="line-number">10</span><br><span class="line-number">11</span><br><span class="line-number">12</span><br><span class="line-number">13</span><br><span class="line-number">14</span><br><span class="line-number">15</span><br><span class="line-number">16</span><br><span class="line-number">17</span><br><span class="line-number">18</span><br><span class="line-number">19</span><br><span class="line-number">20</span><br><span class="line-number">21</span><br><span class="line-number">22</span><br><span class="line-number">23</span><br><span class="line-number">24</span><br><span class="line-number">25</span><br><span class="line-number">26</span><br><span class="line-number">27</span><br><span class="line-number">28</span><br><span class="line-number">29</span><br><span class="line-number">30</span><br><span class="line-number">31</span><br><span class="line-number">32</span><br><span class="line-number">33</span><br><span class="line-number">34</span><br><span class="line-number">35</span><br><span class="line-number">36</span><br><span class="line-number">37</span><br><span class="line-number">38</span><br><span class="line-number">39</span><br><span class="line-number">40</span><br><span class="line-number">41</span><br><span class="line-number">42</span><br><span class="line-number">43</span><br><span class="line-number">44</span><br><span class="line-number">45</span><br><span class="line-number">46</span><br><span class="line-number">47</span><br><span class="line-number">48</span><br><span class="line-number">49</span><br><span class="line-number">50</span><br><span class="line-number">51</span><br><span class="line-number">52</span><br><span class="line-number">53</span><br><span class="line-number">54</span><br><span class="line-number">55</span><br><span class="line-number">56</span><br><span class="line-number">57</span><br><span class="line-number">58</span><br><span class="line-number">59</span><br><span class="line-number">60</span><br><span class="line-number">61</span><br><span class="line-number">62</span><br><span class="line-number">63</span><br><span class="line-number">64</span><br><span class="line-number">65</span><br><span class="line-number">66</span><br><span class="line-number">67</span><br><span class="line-number">68</span><br><span class="line-number">69</span><br><span class="line-number">70</span><br><span class="line-number">71</span><br><span class="line-number">72</span><br><span class="line-number">73</span><br><span class="line-number">74</span><br><span class="line-number">75</span><br><span class="line-number">76</span><br><span class="line-number">77</span><br><span class="line-number">78</span><br><span class="line-number">79</span><br><span class="line-number">80</span><br><span class="line-number">81</span><br><span class="line-number">82</span><br><span class="line-number">83</span><br><span class="line-number">84</span><br><span class="line-number">85</span><br><span class="line-number">86</span><br><span class="line-number">87</span><br><span class="line-number">88</span><br><span class="line-number">89</span><br><span class="line-number">90</span><br><span class="line-number">91</span><br><span class="line-number">92</span><br><span class="line-number">93</span><br><span class="line-number">94</span><br><span class="line-number">95</span><br><span class="line-number">96</span><br><span class="line-number">97</span><br><span class="line-number">98</span><br><span class="line-number">99</span><br><span class="line-number">100</span><br><span class="line-number">101</span><br><span class="line-number">102</span><br><span class="line-number">103</span><br><span class="line-number">104</span><br><span class="line-number">105</span><br><span class="line-number">106</span><br><span class="line-number">107</span><br><span class="line-number">108</span><br><span class="line-number">109</span><br><span class="line-number">110</span><br><span class="line-number">111</span><br><span class="line-number">112</span><br><span class="line-number">113</span><br><span class="line-number">114</span><br><span class="line-number">115</span><br><span class="line-number">116</span><br><span class="line-number">117</span><br><span class="line-number">118</span><br><span class="line-number">119</span><br><span class="line-number">120</span><br><span class="line-number">121</span><br><span class="line-number">122</span><br><span class="line-number">123</span><br><span class="line-number">124</span><br><span class="line-number">125</span><br><span class="line-number">126</span><br><span class="line-number">127</span><br><span class="line-number">128</span><br><span class="line-number">129</span><br><span class="line-number">130</span><br><span class="line-number">131</span><br><span class="line-number">132</span><br><span class="line-number">133</span><br><span class="line-number">134</span><br><span class="line-number">135</span><br><span class="line-number">136</span><br><span class="line-number">137</span><br><span class="line-number">138</span><br><span class="line-number">139</span><br><span class="line-number">140</span><br><span class="line-number">141</span><br><span class="line-number">142</span><br><span class="line-number">143</span><br><span class="line-number">144</span><br><span class="line-number">145</span><br><span class="line-number">146</span><br><span class="line-number">147</span><br><span class="line-number">148</span><br><span class="line-number">149</span><br><span class="line-number">150</span><br><span class="line-number">151</span><br><span class="line-number">152</span><br><span class="line-number">153</span><br><span class="line-number">154</span><br><span class="line-number">155</span><br><span class="line-number">156</span><br><span class="line-number">157</span><br><span class="line-number">158</span><br><span class="line-number">159</span><br><span class="line-number">160</span><br><span class="line-number">161</span><br><span class="line-number">162</span><br><span class="line-number">163</span><br><span class="line-number">164</span><br><span class="line-number">165</span><br><span class="line-number">166</span><br><span class="line-number">167</span><br><span class="line-number">168</span><br><span class="line-number">169</span><br><span class="line-number">170</span><br><span class="line-number">171</span><br><span class="line-number">172</span><br><span class="line-number">173</span><br><span class="line-number">174</span><br><span class="line-number">175</span><br><span class="line-number">176</span><br><span class="line-number">177</span><br><span class="line-number">178</span><br><span class="line-number">179</span><br><span class="line-number">180</span><br><span class="line-number">181</span><br><span class="line-number">182</span><br><span class="line-number">183</span><br><span class="line-number">184</span><br><span class="line-number">185</span><br><span class="line-number">186</span><br><span class="line-number">187</span><br><span class="line-number">188</span><br><span class="line-number">189</span><br><span class="line-number">190</span><br><span class="line-number">191</span><br><span class="line-number">192</span><br><span class="line-number">193</span><br><span class="line-number">194</span><br><span class="line-number">195</span><br><span class="line-number">196</span><br><span class="line-number">197</span><br><span class="line-number">198</span><br><span class="line-number">199</span><br><span class="line-number">200</span><br><span class="line-number">201</span><br><span class="line-number">202</span><br><span class="line-number">203</span><br><span class="line-number">204</span><br><span class="line-number">205</span><br><span class="line-number">206</span><br><span class="line-number">207</span><br><span class="line-number">208</span><br><span class="line-number">209</span><br><span class="line-number">210</span><br><span class="line-number">211</span><br><span class="line-number">212</span><br><span class="line-number">213</span><br><span class="line-number">214</span><br><span class="line-number">215</span><br><span class="line-number">216</span><br><span class="line-number">217</span><br><span class="line-number">218</span><br><span class="line-number">219</span><br><span class="line-number">220</span><br><span class="line-number">221</span><br><span class="line-number">222</span><br><span class="line-number">223</span><br><span class="line-number">224</span><br><span class="line-number">225</span><br><span class="line-number">226</span><br><span class="line-number">227</span><br><span class="line-number">228</span><br><span class="line-number">229</span><br><span class="line-number">230</span><br><span class="line-number">231</span><br><span class="line-number">232</span><br><span class="line-number">233</span><br><span class="line-number">234</span><br><span class="line-number">235</span><br><span class="line-number">236</span><br><span class="line-number">237</span><br><span class="line-number">238</span><br><span class="line-number">239</span><br><span class="line-number">240</span><br><span class="line-number">241</span><br><span class="line-number">242</span><br><span class="line-number">243</span><br><span class="line-number">244</span><br><span class="line-number">245</span><br><span class="line-number">246</span><br><span class="line-number">247</span><br><span class="line-number">248</span><br><span class="line-number">249</span><br></div></div></template>
