<template><h2 id="字面量类型" tabindex="-1"><a class="header-anchor" href="#字面量类型" aria-hidden="true">#</a> 字面量类型</h2>
<p>例如</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>let str1 = 'helloACN'
const str2 = 'helloACN'
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br></div></div><p>大家可以猜一下，str1 是什么类型的，str2 是什么类型？</p>
<p>这里是正确答案：
str1 的类型为 string 类型，str2 的类型为 helloACN类型</p>
<p>这是为啥呢？</p>
<p>str1 是一个变量(let)，它的值可以是任意字符串，所以类型为:string
str2 是一个常量(const)，它的值不能变化只能是 'helloACN'，所以，它的类型为:'helloACN'</p>
<p>注意：此处的 'helloACN'，就是一个字面量类型，也就是说某个特定的字符串也可以作为 TS 中的类型
这时候就有人好奇了，那字面量类型有啥作用呢？
字面量类型一般是配合联合类型一起使用的， 用来表示一组明确的可选值列表。
例如下面的例子：</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>type ProjectType = 'ACN' | 'Alpha'
// 声明一个类型，他的值 是 'ACN' 或者是 'Alpha'
let g1: ProjectType = 'ACN' // 正确
let g2: ProjectType = 'Alpha' // 正确
let g3: ProjectType = 'llll' // 错误

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br></div></div></template>
