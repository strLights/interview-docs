<template><h2 id="方法1" tabindex="-1"><a class="header-anchor" href="#方法1" aria-hidden="true">#</a> 方法1</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>&lt;meta name="viewport" content="width=device-width"/>
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><p>站点内包含了 width=device-width 这个 <meta> 标签，也就意味着这个网站是响应式的网站，那么移动端浏览器就可以自动禁止掉双击缩放行为并且去掉 300ms 的点击延迟。</p>
<p>这个方案相对方案1 的好处在于，它没有完全禁止缩放，只是禁用了默认的双击缩放行为，但用户仍然可以通过双指缩放来缩放页面。</p>
<h2 id="方法2-fastclick" tabindex="-1"><a class="header-anchor" href="#方法2-fastclick" aria-hidden="true">#</a> 方法2 FastClick</h2>
<p>FastClick 在检测到 touched 事件的时候，会通过 DOM 自定义事件立即出发一个模拟 click 事件，并把浏览器在 300 毫秒之后真正触发的 click 事件阻止掉。</p>
</template>
