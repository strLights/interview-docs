<template><h1 id="有哪些常见的loader-他们是解决什么问题的" tabindex="-1"><a class="header-anchor" href="#有哪些常见的loader-他们是解决什么问题的" aria-hidden="true">#</a> 有哪些常见的Loader？他们是解决什么问题的？</h1>
<p>file-loader：把文件输出到一个文件夹中，在代码中通过相对 URL 去引用输出的文件
url-loader：和 file-loader 类似，但是能在文件很小的情况下以 base64 的方式把文件内容注入到代码中去</p>
<p>source-map-loader：加载额外的 Source Map 文件，以方便断点调试
image-loader：加载并且压缩图片文件
babel-loader：把 ES6 转换成 ES5
css-loader：加载 CSS，支持模块化、压缩、文件导入等特性
style-loader：把 CSS 代码注入到 JavaScript 中，通过 DOM 操作去加载 CSS。
eslint-loader：通过 ESLint 检查 JavaScript 代码</p>
</template>
