<template><h2 id="下载一个项目和它的整个代码历史" tabindex="-1"><a class="header-anchor" href="#下载一个项目和它的整个代码历史" aria-hidden="true">#</a> 下载一个项目和它的整个代码历史</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git clone [url]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h2 id="列出所有本地分支" tabindex="-1"><a class="header-anchor" href="#列出所有本地分支" aria-hidden="true">#</a> 列出所有本地分支</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git branch
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h2 id="新建一个分支-但依然停留在当前分支" tabindex="-1"><a class="header-anchor" href="#新建一个分支-但依然停留在当前分支" aria-hidden="true">#</a> 新建一个分支，但依然停留在当前分支</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git branch [branch-name]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h2 id="新建一个分支-并切换到该分支" tabindex="-1"><a class="header-anchor" href="#新建一个分支-并切换到该分支" aria-hidden="true">#</a> 新建一个分支，并切换到该分支</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git checkout -b [branch-name]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h2 id="合并指定分支到当前分支" tabindex="-1"><a class="header-anchor" href="#合并指定分支到当前分支" aria-hidden="true">#</a> 合并指定分支到当前分支</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git merge [branch-name]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h2 id="添加当前目录的所有文件到暂存区" tabindex="-1"><a class="header-anchor" href="#添加当前目录的所有文件到暂存区" aria-hidden="true">#</a> 添加当前目录的所有文件到暂存区</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git add .
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h2 id="提交暂存区到仓库区" tabindex="-1"><a class="header-anchor" href="#提交暂存区到仓库区" aria-hidden="true">#</a> 提交暂存区到仓库区</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git commit -m 'XXX'
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h2 id="取回远程仓库的变化-并与本地分支合并" tabindex="-1"><a class="header-anchor" href="#取回远程仓库的变化-并与本地分支合并" aria-hidden="true">#</a> 取回远程仓库的变化，并与本地分支合并</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git pull origin master
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h2 id="上传本地指定分支到远程" tabindex="-1"><a class="header-anchor" href="#上传本地指定分支到远程" aria-hidden="true">#</a> 上传本地指定分支到远程</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git push origin master
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h2 id="切换到指定分支-并更新工作区" tabindex="-1"><a class="header-anchor" href="#切换到指定分支-并更新工作区" aria-hidden="true">#</a> 切换到指定分支，并更新工作区</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git checkout [branch-name]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h2 id="显示当前分支的版本历史" tabindex="-1"><a class="header-anchor" href="#显示当前分支的版本历史" aria-hidden="true">#</a> 显示当前分支的版本历史</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git log
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h2 id="查看当前的用户名" tabindex="-1"><a class="header-anchor" href="#查看当前的用户名" aria-hidden="true">#</a> 查看当前的用户名</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git config user.name

git config user.email
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br></div></div><h4 id="使用一次新的commit-替代上一次提交" tabindex="-1"><a class="header-anchor" href="#使用一次新的commit-替代上一次提交" aria-hidden="true">#</a> 使用一次新的commit，替代上一次提交</h4>
<h4 id="如果代码没有任何新变化-则用来改写上一次commit的提交信息" tabindex="-1"><a class="header-anchor" href="#如果代码没有任何新变化-则用来改写上一次commit的提交信息" aria-hidden="true">#</a> 如果代码没有任何新变化，则用来改写上一次commit的提交信息</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git commit --amend -m [message]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h2 id="修改用户名和邮箱" tabindex="-1"><a class="header-anchor" href="#修改用户名和邮箱" aria-hidden="true">#</a> 修改用户名和邮箱：</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>
git config --global user.name “Your_username”

git config --global user.email “Your_email”

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br></div></div><h2 id="git-只提交某一文件夹下的文件" tabindex="-1"><a class="header-anchor" href="#git-只提交某一文件夹下的文件" aria-hidden="true">#</a> git 只提交某一文件夹下的文件</h2>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git status ./           查看这个文件夹下的文件状态
git add ./*             把这个文件下的所有应该加入追踪的，加入到暂存区
git commit -m 日志描述 ./           把这个文件夹下提交的修改commit到本地库
git push                push到远程库

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br></div></div></template>
