<template><h2 id="常用命令大全" tabindex="-1"><a class="header-anchor" href="#常用命令大全" aria-hidden="true">#</a> 常用命令大全</h2>
<p>我们我们开发时候在工作区，当我们把修改，add之后，修改内容会被提到暂存区，当我们commit 之后修改的内容
会被提到我们本地的仓库（repository）,当我们push之后，会被提到远程仓库（remote）</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>Workspace：工作区
Index / Stage：暂存区
Repository：仓库区（或本地仓库）
Remote：远程仓库
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br></div></div><h1 id="一、新建代码库" tabindex="-1"><a class="header-anchor" href="#一、新建代码库" aria-hidden="true">#</a> 一、新建代码库</h1>
<h4 id="在当前目录新建一个git代码库" tabindex="-1"><a class="header-anchor" href="#在当前目录新建一个git代码库" aria-hidden="true">#</a> 在当前目录新建一个Git代码库</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code> git init
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="新建一个目录-将其初始化为git代码库" tabindex="-1"><a class="header-anchor" href="#新建一个目录-将其初始化为git代码库" aria-hidden="true">#</a> 新建一个目录，将其初始化为Git代码库</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git init [project-name]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="下载一个项目和它的整个代码历史" tabindex="-1"><a class="header-anchor" href="#下载一个项目和它的整个代码历史" aria-hidden="true">#</a> 下载一个项目和它的整个代码历史</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git clone [url]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h1 id="生成ssh" tabindex="-1"><a class="header-anchor" href="#生成ssh" aria-hidden="true">#</a> 生成ssh</h1>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git config --global user.name "yk"
添加邮箱
git config --global user.email "youremail@163.com"
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br></div></div><h4 id="生成公钥" tabindex="-1"><a class="header-anchor" href="#生成公钥" aria-hidden="true">#</a> 生成公钥</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>生成ssh-keygen -t rsa -C "你的邮箱"  连续回车  
ssh-keygen -t rsa
生成公钥
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br></div></div><blockquote>
<p>（然后有个C盘的路径，沿着那个路径找到那个文件，把里面的内容粘贴过来，在GitHub上那个ssh，设置秘钥，密码粘进去）</p>
</blockquote>
<h1 id="添加到暂存区" tabindex="-1"><a class="header-anchor" href="#添加到暂存区" aria-hidden="true">#</a> 添加到暂存区</h1>
<h4 id="添加指定文件到暂存区" tabindex="-1"><a class="header-anchor" href="#添加指定文件到暂存区" aria-hidden="true">#</a> 添加指定文件到暂存区</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git add [file1] [file2] ...
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="添加指定目录到暂存区-包括子目录" tabindex="-1"><a class="header-anchor" href="#添加指定目录到暂存区-包括子目录" aria-hidden="true">#</a> 添加指定目录到暂存区，包括子目录</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>$ git add [dir]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="添加当前目录的所有文件到暂存区" tabindex="-1"><a class="header-anchor" href="#添加当前目录的所有文件到暂存区" aria-hidden="true">#</a> 添加当前目录的所有文件到暂存区</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>$ git add .
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h5 id="添加每个变化前-都会要求确认-对于同一个文件的多处变化-可以实现分次提交" tabindex="-1"><a class="header-anchor" href="#添加每个变化前-都会要求确认-对于同一个文件的多处变化-可以实现分次提交" aria-hidden="true">#</a> 添加每个变化前，都会要求确认 对于同一个文件的多处变化，可以实现分次提交</h5>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git add -p
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="删除工作区文件-并且将这次删除放入暂存区" tabindex="-1"><a class="header-anchor" href="#删除工作区文件-并且将这次删除放入暂存区" aria-hidden="true">#</a> 删除工作区文件，并且将这次删除放入暂存区</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git rm [file1] [file2] ...
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="改名文件-并且将这个改名放入暂存区" tabindex="-1"><a class="header-anchor" href="#改名文件-并且将这个改名放入暂存区" aria-hidden="true">#</a> 改名文件，并且将这个改名放入暂存区</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code> git mv [file-original] [file-renamed]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h1 id="代码提交" tabindex="-1"><a class="header-anchor" href="#代码提交" aria-hidden="true">#</a> 代码提交</h1>
<h4 id="提交暂存区到仓库区" tabindex="-1"><a class="header-anchor" href="#提交暂存区到仓库区" aria-hidden="true">#</a> 提交暂存区到仓库区</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code> git commit -m [message]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="提交暂存区的指定文件到仓库区" tabindex="-1"><a class="header-anchor" href="#提交暂存区的指定文件到仓库区" aria-hidden="true">#</a> 提交暂存区的指定文件到仓库区</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git commit [file1] [file2] ... -m [message]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="使用一次新的commit-替代上一次提交" tabindex="-1"><a class="header-anchor" href="#使用一次新的commit-替代上一次提交" aria-hidden="true">#</a> 使用一次新的commit，替代上一次提交</h4>
<h4 id="如果代码没有任何新变化-则用来改写上一次commit的提交信息" tabindex="-1"><a class="header-anchor" href="#如果代码没有任何新变化-则用来改写上一次commit的提交信息" aria-hidden="true">#</a> 如果代码没有任何新变化，则用来改写上一次commit的提交信息</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git commit --amend -m [message]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h1 id="分支" tabindex="-1"><a class="header-anchor" href="#分支" aria-hidden="true">#</a> 分支</h1>
<h4 id="查看所有分支" tabindex="-1"><a class="header-anchor" href="#查看所有分支" aria-hidden="true">#</a> 查看所有分支</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git branch -a
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="查看所有远程分支" tabindex="-1"><a class="header-anchor" href="#查看所有远程分支" aria-hidden="true">#</a> 查看所有远程分支</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git branch -r
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="查看所有本地分支" tabindex="-1"><a class="header-anchor" href="#查看所有本地分支" aria-hidden="true">#</a> 查看所有本地分支</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git branch
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="新建一个分支-但依然停留在当前分支" tabindex="-1"><a class="header-anchor" href="#新建一个分支-但依然停留在当前分支" aria-hidden="true">#</a> 新建一个分支，但依然停留在当前分支</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git branch [branch-name]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="新建一个分支-并切换到该分支" tabindex="-1"><a class="header-anchor" href="#新建一个分支-并切换到该分支" aria-hidden="true">#</a> 新建一个分支，并切换到该分支</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git checkout -b [branch]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="切换到指定分支-并更新工作区" tabindex="-1"><a class="header-anchor" href="#切换到指定分支-并更新工作区" aria-hidden="true">#</a> 切换到指定分支，并更新工作区</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git checkout [branch-name]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="切换到上一个分支" tabindex="-1"><a class="header-anchor" href="#切换到上一个分支" aria-hidden="true">#</a> 切换到上一个分支</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git checkout -
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="合并指定分支到当前分支" tabindex="-1"><a class="header-anchor" href="#合并指定分支到当前分支" aria-hidden="true">#</a> 合并指定分支到当前分支</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code> git merge [branch]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="删除本地分支" tabindex="-1"><a class="header-anchor" href="#删除本地分支" aria-hidden="true">#</a> 删除本地分支</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git branch -d &lt;branchName>
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="强制删除本地分支" tabindex="-1"><a class="header-anchor" href="#强制删除本地分支" aria-hidden="true">#</a> 强制删除本地分支</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git branch -D &lt;branchName>
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="删除远程分支" tabindex="-1"><a class="header-anchor" href="#删除远程分支" aria-hidden="true">#</a> 删除远程分支</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git push origin --delete [branch-name]
git branch -dr [remote/branch]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br></div></div><h4 id="新建一个分支-与指定的远程分支建立追踪关系" tabindex="-1"><a class="header-anchor" href="#新建一个分支-与指定的远程分支建立追踪关系" aria-hidden="true">#</a> 新建一个分支，与指定的远程分支建立追踪关系</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git branch --track [branch] [remote-branch]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><blockquote>
<p>git branch -d 删除分支，会在删除前检查merge状态，避免误删没有合并的分支。
git branch -D 是git branch --delete --force的简写，它会强制删除该分支。
如果想要删除远程分支以及追踪分支需使用: git push --origin -delete branch</p>
</blockquote>
<h1 id="查看信息" tabindex="-1"><a class="header-anchor" href="#查看信息" aria-hidden="true">#</a> 查看信息</h1>
<h4 id="显示有变更的文件" tabindex="-1"><a class="header-anchor" href="#显示有变更的文件" aria-hidden="true">#</a> 显示有变更的文件</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code> git status
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="显示当前分支的版本历史" tabindex="-1"><a class="header-anchor" href="#显示当前分支的版本历史" aria-hidden="true">#</a> 显示当前分支的版本历史</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git log
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><p>如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数：</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code> git log --pretty=oneline
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="搜索提交历史-根据关键词" tabindex="-1"><a class="header-anchor" href="#搜索提交历史-根据关键词" aria-hidden="true">#</a> 搜索提交历史，根据关键词</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>$ git log -S [keyword]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="显示某个文件的版本历史-包括文件改名" tabindex="-1"><a class="header-anchor" href="#显示某个文件的版本历史-包括文件改名" aria-hidden="true">#</a> 显示某个文件的版本历史，包括文件改名</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code> git log --follow [file]
git whatchanged [file]

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br></div></div><h4 id="显示过去5次提交" tabindex="-1"><a class="header-anchor" href="#显示过去5次提交" aria-hidden="true">#</a> 显示过去5次提交</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git log -5 --pretty --oneline
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="显示暂存区和工作区的差异" tabindex="-1"><a class="header-anchor" href="#显示暂存区和工作区的差异" aria-hidden="true">#</a> 显示暂存区和工作区的差异</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git diff
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="显示当前分支的最近几次提交" tabindex="-1"><a class="header-anchor" href="#显示当前分支的最近几次提交" aria-hidden="true">#</a> 显示当前分支的最近几次提交</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code> git reflog
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h1 id="远程同步" tabindex="-1"><a class="header-anchor" href="#远程同步" aria-hidden="true">#</a> 远程同步</h1>
<h4 id="上传本地指定分支到远程仓库" tabindex="-1"><a class="header-anchor" href="#上传本地指定分支到远程仓库" aria-hidden="true">#</a> 上传本地指定分支到远程仓库</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git push [remote] [branch]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="强行推送当前分支到远程仓库-即使有冲突" tabindex="-1"><a class="header-anchor" href="#强行推送当前分支到远程仓库-即使有冲突" aria-hidden="true">#</a> 强行推送当前分支到远程仓库，即使有冲突</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git push [remote] --force
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="推送所有分支到远程仓库" tabindex="-1"><a class="header-anchor" href="#推送所有分支到远程仓库" aria-hidden="true">#</a> 推送所有分支到远程仓库</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git push [remote] --all
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="下载远程仓库的所有变动" tabindex="-1"><a class="header-anchor" href="#下载远程仓库的所有变动" aria-hidden="true">#</a> 下载远程仓库的所有变动</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git fetch [remote]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="显示所有远程仓库" tabindex="-1"><a class="header-anchor" href="#显示所有远程仓库" aria-hidden="true">#</a> 显示所有远程仓库</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git remote -v
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="增加一个新的远程仓库-并命名" tabindex="-1"><a class="header-anchor" href="#增加一个新的远程仓库-并命名" aria-hidden="true">#</a> 增加一个新的远程仓库，并命名</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git remote add [shortname] [url]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="取回远程仓库的变化-并与本地分支合并" tabindex="-1"><a class="header-anchor" href="#取回远程仓库的变化-并与本地分支合并" aria-hidden="true">#</a> 取回远程仓库的变化，并与本地分支合并</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git pull [remote] [branch]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h1 id="撤销" tabindex="-1"><a class="header-anchor" href="#撤销" aria-hidden="true">#</a> 撤销</h1>
<h4 id="恢复暂存区的指定文件到工作区" tabindex="-1"><a class="header-anchor" href="#恢复暂存区的指定文件到工作区" aria-hidden="true">#</a> 恢复暂存区的指定文件到工作区</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git checkout [file]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="恢复暂存区的所有文件到工作区" tabindex="-1"><a class="header-anchor" href="#恢复暂存区的所有文件到工作区" aria-hidden="true">#</a> 恢复暂存区的所有文件到工作区</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git checkout .
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="重置暂存区的指定文件-与上一次commit保持一致-但工作区不变" tabindex="-1"><a class="header-anchor" href="#重置暂存区的指定文件-与上一次commit保持一致-但工作区不变" aria-hidden="true">#</a> 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git reset [file]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="重置暂存区与工作区-与上一次commit保持一致" tabindex="-1"><a class="header-anchor" href="#重置暂存区与工作区-与上一次commit保持一致" aria-hidden="true">#</a> 重置暂存区与工作区，与上一次commit保持一致</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git reset --hard
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="恢复某个commit的指定文件到暂存区和工作区" tabindex="-1"><a class="header-anchor" href="#恢复某个commit的指定文件到暂存区和工作区" aria-hidden="true">#</a> 恢复某个commit的指定文件到暂存区和工作区</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git checkout [commit] [file]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="重置当前分支的指针为指定commit-同时重置暂存区-但工作区不变" tabindex="-1"><a class="header-anchor" href="#重置当前分支的指针为指定commit-同时重置暂存区-但工作区不变" aria-hidden="true">#</a> 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git reset [commit]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="重置当前分支的head为指定commit-同时重置暂存区和工作区-与指定commit一致" tabindex="-1"><a class="header-anchor" href="#重置当前分支的head为指定commit-同时重置暂存区和工作区-与指定commit一致" aria-hidden="true">#</a> 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git reset --hard [commit]
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git reset --hard 1094a  //返回到指定某一版本
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><blockquote>
<p>Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交1094adb...（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。</p>
</blockquote>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git reset --hard HEAD^ //返回上一个版本
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h4 id="暂时将未提交的变化移除-稍后再移入" tabindex="-1"><a class="header-anchor" href="#暂时将未提交的变化移除-稍后再移入" aria-hidden="true">#</a> 暂时将未提交的变化移除，稍后再移入</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>$ git stash
$ git stash pop
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br></div></div><h3 id="拉取远程所有分支" tabindex="-1"><a class="header-anchor" href="#拉取远程所有分支" aria-hidden="true">#</a> 拉取远程所有分支</h3>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>


git branch -r | grep -v '\->' | while read remote; do git branch --track "${remote#origin/}" "$remote"; done
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br></div></div><h2 id="首先同步所有远程分支-如上" tabindex="-1"><a class="header-anchor" href="#首先同步所有远程分支-如上" aria-hidden="true">#</a> 首先同步所有远程分支，如上：</h2>
<h3 id="将本地所有分支与远程保持同步" tabindex="-1"><a class="header-anchor" href="#将本地所有分支与远程保持同步" aria-hidden="true">#</a> 将本地所有分支与远程保持同步</h3>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git fetch --all
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h3 id="最后拉取所有分支代码" tabindex="-1"><a class="header-anchor" href="#最后拉取所有分支代码" aria-hidden="true">#</a> 最后拉取所有分支代码</h3>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code> git pull --all

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br></div></div></template>
