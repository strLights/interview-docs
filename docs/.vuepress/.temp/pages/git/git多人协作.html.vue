<template><h1 id="多人协作" tabindex="-1"><a class="header-anchor" href="#多人协作" aria-hidden="true">#</a> 多人协作</h1>
<p>图形化工具有很多，我们下载后直接用就行，现在我们主要说一下命令行的git 的使用。</p>
<p>下面我们说一下，在工作常见的多人协作使用命令行场景：</p>
<blockquote>
<p>假设现在有三个人，A，B都是开发，C是负责人。
任务需求到达，A来开发登录板块。B来开发注册板块。</p>
</blockquote>
<p><strong>1</strong>
A 首先把git 项目克隆到本地，（就一开始没有项目时候使用一次即可）</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git clone http//XXX

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br></div></div><p>cd 到下载的这个文件夹，进入的默认是master分支。</p>
<p>A 同学开发的是login板块，所以，A新建了个分支来开发。</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git checkout -b feature-login

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br></div></div><p>此时新建了个feature-login的分支，并且当前分支就是feature-login分支了，</p>
<p>当A 在分支修改完后就直接提交</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git status //看看自己改了哪些文件
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git add --all或 git add .
git commit -m "登录板块开发完毕"

git push origin feature-login
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br></div></div><p><strong>2</strong>
B 同学开发与A同理</p>
<p><strong>3</strong>
当A与B都已经开发完毕了，C出场了</p>
<p>C 合并代码</p>
<p>C首先合并A代码</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git fetch  //把线上所有的分支都下载下来

git branch //查看有几条分支

git checkout feature-login //转到feature-login分支

git pull origin feature-login  //把feature-login代码下载下来

git checkout master  //转到master分支

git merge feature-login  //将feature-login代码合并到master分支上来

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br><span class="line-number">7</span><br><span class="line-number">8</span><br><span class="line-number">9</span><br><span class="line-number">10</span><br><span class="line-number">11</span><br><span class="line-number">12</span><br></div></div><p>同理再合并B代码</p>
<p>merge时候有时候会冲突，就进入文件把冲突解决掉，再merge就可以了。</p>
<p>等都合并完了，C再正常的提交一下，master分支，即可！</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git status
git add .
git commit -m "添加登录注册功能"
git push origin master
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br></div></div><p><strong>以上就是多人协作啦</strong></p>
<h2 id="多人协作常见意外情况" tabindex="-1"><a class="header-anchor" href="#多人协作常见意外情况" aria-hidden="true">#</a> 多人协作常见意外情况</h2>
<p>开发一开始，你忘了新建分支。但此时，你已经在master分支上开发了半天了，写了好多代码。</p>
<p>如果你现在新建分支是不可以了，你得先提交，但那不就提到master分支了吗。。。。</p>
<h3 id="如何解决" tabindex="-1"><a class="header-anchor" href="#如何解决" aria-hidden="true">#</a> 如何解决</h3>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git statsh //把已经修改的代码暂存到另外一个地方

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br></div></div><p>现在你再切换分支就可以了</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git checkout -b new-feature  //切换到new-feature分支

git stash pop //把修改的释放出来

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br></div></div><p>然后正常那个提交即可</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git add .
git commit -m "新增XX"
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br></div></div></template>
