<template><h1 id="pnpm软链接和硬链接" tabindex="-1"><a class="header-anchor" href="#pnpm软链接和硬链接" aria-hidden="true">#</a> pnpm软链接和硬链接</h1>
<h2 id="软链接" tabindex="-1"><a class="header-anchor" href="#软链接" aria-hidden="true">#</a> 软链接</h2>
<p>在计算机中我们文件夹中的文件实际上是一个指针，但这个指针并不是直接指向我们在磁盘中存储文件的位置，而是指向一个 inode 块，inode 中存储着文件在磁盘中的各种信息，一般我们的文件都是指向 对应文件的 inode，我们把这类链接成为硬链接，但是还有一种链接，它存储的并不是实际的值，而是另一个硬链接的地址，我们把这类链接成为软链接。</p>
<h4 id="硬链接特点" tabindex="-1"><a class="header-anchor" href="#硬链接特点" aria-hidden="true">#</a> 硬链接特点</h4>
<p>具有相同inode节点号的多个文件互为硬链接文件；
删除硬链接文件或者删除源文件任意之一，文件实体并未被删除；
只有删除了源文件和所有对应的硬链接文件，文件实体才会被删除；
硬链接文件是文件的另一个入口；
可以通过给文件设置硬链接文件来防止重要文件被误删；
创建硬链接命令 ln 源文件 硬链接文件；
硬链接文件是普通文件，可以用rm删除；
对于静态文件（没有进程正在调用），当硬链接数为0时文件就被删除。注意：如果有进程正在调用，则无法删除或者即使文件名被删除但空间不会释放。</p>
<h4 id="软链接特点" tabindex="-1"><a class="header-anchor" href="#软链接特点" aria-hidden="true">#</a> 软链接特点</h4>
<p>软链接类似windows系统的快捷方式；
软链接里面存放的是源文件的路径，指向源文件；
删除源文件，软链接依然存在，但无法访问源文件内容；
软链接失效时一般是白字红底闪烁；
创建软链接命令 ln -s 源文件 软链接文件；
软链接和源文件是不同的文件，文件类型也不同，inode号也不同；
软链接的文件类型是“l”，可以用rm删除。</p>
<p>可以看到 node_modules 结构非常清晰，但是这个 express 文件夹只是一个软链接, 它的真正存储的地方在图中的 .pnpm 文件夹中。</p>
<h3 id="pnpm-为什么要使用软链接和硬链接" tabindex="-1"><a class="header-anchor" href="#pnpm-为什么要使用软链接和硬链接" aria-hidden="true">#</a> pnpm 为什么要使用软链接和硬链接</h3>
<h5 id="pnpm-的软链接" tabindex="-1"><a class="header-anchor" href="#pnpm-的软链接" aria-hidden="true">#</a> pnpm 的软链接</h5>
<p>这样的通过软链接的设计既保证了不会出现幽灵依赖的问题，同时也能兼容 node 的寻找模块方式。
所以说 pnpm 的软链接就是将 node_modules 里的文件软链接到对应的 .pnpm/[package_name]@version/node_modules/[package_name] 中。</p>
<h5 id="pnpm-的硬链接" tabindex="-1"><a class="header-anchor" href="#pnpm-的硬链接" aria-hidden="true">#</a> pnpm 的硬链接</h5>
<p>pnpm 有个根目录，一般都是保存在 user/.pnpm-store 下，pnpm 通过硬链接的方式保证了相同的包不会被重复下载，比如说我们已经在 repoA 中下载过一次 express@4.17.1 版本，那我们后续在 repoB 中安装 express@4.17.1 的时候是会被复用的，具体就是 repoA 中的 express 中的文件和 repoB 中的 express 中的文件指向的是同一个 inode</p>
</template>
