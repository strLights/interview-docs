<template><h1 id="为什么说vite比webpack更快" tabindex="-1"><a class="header-anchor" href="#为什么说vite比webpack更快" aria-hidden="true">#</a> 为什么说vite比webpack更快</h1>
<p>webpack会先打包，然后启动开发服务器，请求服务器时直接给予打包结果。
vite是直接启动开发服务器，请求哪个模块再对该模块进行实时编译。
vite在启动的时候不需要打包，意味着不需要分析模块的依赖、不需要编译，因此启动速度非常快。
当浏览器请求某个模块时，再根据需要对模块内容进行编译。这种按需动态编译的方式，极大的缩减了编译时间，项目越复杂、模块越多，vite的优势越明显。
在HMR方面，当改动了一个模块后，仅需让浏览器重新请求该模块即可，不像webpack那样需要把该模块的相关依赖模块全部编译一次，效率更高。
当需要打包到生产环境时，vite使用传统的rollup进行打包，因此，vite的主要优势在开发阶段。另外，由于vite利用的是ES Module，因此在代码中不可以使用CommonJS</p>
</template>
