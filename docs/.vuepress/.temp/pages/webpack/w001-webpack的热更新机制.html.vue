<template><h3 id="w001-webpack的热更新机制" tabindex="-1"><a class="header-anchor" href="#w001-webpack的热更新机制" aria-hidden="true">#</a> w001-webpack的热更新机制</h3>
<p>HMR全称 Hot Module Replacement，可以理解为模块热替换，指在应用程序运行过程中，替换、添加、删除模块，而无需重新刷新整个应用。</p>
<p>例如，我们在应用运行过程中修改了某个模块，通过自动刷新会导致整个应用的整体刷新，那页面中的状态信息都会丢失</p>
<p>如果使用的是 HMR，就可以实现只将修改的模块实时替换至应用中，不必完全刷新整个应用</p>
<p>在webpack中配置开启热模块也非常的简单，如下代码：</p>
<div class="language-javascript ext-js line-numbers-mode"><pre v-pre class="language-javascript"><code><span class="token keyword">const</span> webpack <span class="token operator">=</span> <span class="token function">require</span><span class="token punctuation">(</span><span class="token string">'webpack'</span><span class="token punctuation">)</span> 
module<span class="token punctuation">.</span>exports <span class="token operator">=</span> <span class="token punctuation">{</span> 
  <span class="token comment">// ... </span>
  <span class="token literal-property property">devServer</span><span class="token operator">:</span> <span class="token punctuation">{</span> 
    <span class="token comment">// 开启 HMR 特性 </span>
    <span class="token literal-property property">hot</span><span class="token operator">:</span> <span class="token boolean">true</span> 
    <span class="token comment">// hotOnly: true </span>
  <span class="token punctuation">}</span> 
<span class="token punctuation">}</span> 
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br><span class="line-number">7</span><br><span class="line-number">8</span><br><span class="line-number">9</span><br></div></div><p>通过上述这种配置，如果我们修改并保存css文件，确实能够以不刷新的形式更新到页面中</p>
<h2 id="原理" tabindex="-1"><a class="header-anchor" href="#原理" aria-hidden="true">#</a> 原理</h2>
<p>Webpack-complier ：webpack 的编译器，将 JavaScript 编译成 bundle（就是最终的输出文件）
HMR Server：将热更新的文件输出给 HMR Runtime
Bunble Server：提供文件在浏览器的访问，也就是我们平时能够正常通过 localhost 访问我们本地网站的原因
HMR Runtime：开启了热更新的话，在打包阶段会被注入到浏览器中的 bundle.js，这样 bundle.js 就可以跟服务器建立连接，通常是使用 websocket ，当收到服务器的更新指令的时候，就   去更新文件的变化
bundle.js：构建输出的文件
启动阶段</p>
<p>文件经过 Webpack-complier 编译好后传输给 Bundle Server，Bundle Server 可以让浏览器访问到我们打包出来的文件</p>
<p>文件经过 Webpack-complier 编译好后传输给 HMR Server，HMR Server 知道哪个资源(模块)发生了改变，并通知 HMR Runtime 有哪些变化（也就是上面我们看到的两个请求），HMR Runtime 就会更新我们的代码，这样我们浏览器就会更新并且不需要刷新</p>
<p>当某一个文件或者模块发生变化时，webpack监听到文件变化对文件重新编译打包，编译生成唯一的hash值，这个hash值用来作为下一次热更新的标识</p>
<p>根据变化的内容生成两个补丁文件：manifest(包含了 hash 和 chundId，用来说明变化的内容)和chunk.js 模块</p>
<p>由于socket服务器在HMR Runtime 和 HMR Server之间建立 websocket链接，当文件发生改动的时候，服务端会向浏览器推送一条消息，消息包含文件改动后生成的hash值，作为下一次热更新的标识</p>
<p>在浏览器接受到这条消息之前，浏览器已经在上一次socket 消息中已经记住了此时的hash 标识，这时候我们会创建一个 ajax 去服务端请求获取到变化内容的 manifest 文件</p>
<p>mainfest文件包含重新build生成的hash值，以及变化的模块，</p>
<p>浏览器根据 manifest 文件获取模块变化的内容，从而触发render流程，实现局部模块更新</p>
<h2 id="总结" tabindex="-1"><a class="header-anchor" href="#总结" aria-hidden="true">#</a> 总结</h2>
<p>通过webpack-dev-server创建两个服务器：提供静态资源的服务(express)和Socket服务
express server 负责直接提供静态资源的服务(打包后的资源直接被浏览器请求和解析)
socket server 是一个 websocket 的长连接，双方可以通信
当 socket server 监听到对应的模块发生变化时，会生成两个文件.json(manifest文件)和.js文件(update chunk)
通过长连接，socket server 可以直接将这两个文件主动发送给客户端(浏览器)
浏览器拿到两个新的文件后，通过HMR runtime机制，加载这两个文件，并且针对修改的模块进行更新</p>
<h2 id="详细版" tabindex="-1"><a class="header-anchor" href="#详细版" aria-hidden="true">#</a> 详细版</h2>
<p>在 webpack 的运行时中 <strong>webpack__modules</strong> 用以维护所有的模块。</p>
<p>而热模块替换的原理，即通过 chunk 的方式加载最新的 modules，找到 <strong>webpack__modules</strong> 中对应的模块逐一替换，并删除其上下缓存。</p>
<blockquote>
<p>webpack-dev-server 将打包输出 bundle 使用内存型文件系统控制，而非真实的文件系统。此时使用的是 memfs 模拟 node.js fs API
每当文件发生变更时，webpack 将会重新编译，webpack-dev-server 将会监控到此时文件变更事件，并找到其对应的 module。此时使用的是 chokidar 监控文件变更
webpack-dev-server 将会把变更模块通知到浏览器端，此时使用 websocket 与浏览器进行交流。此时使用的是 ws
浏览器根据 websocket 接收到 hash，并通过 hash 以 JSONP 的方式请求更新模块的 chunk
浏览器加载 chunk，并使用新的模块对旧模块进行热替换，并删除其缓存</p>
</blockquote>
</template>
