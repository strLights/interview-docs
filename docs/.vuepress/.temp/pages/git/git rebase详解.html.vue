<template><h2 id="merge-和rebase什么关系" tabindex="-1"><a class="header-anchor" href="#merge-和rebase什么关系" aria-hidden="true">#</a> merge 和rebase什么关系</h2>
<blockquote>
<p>git rebase 和git merge 做的事其实是一样的。它们都被设计来将一个分支的更改并入另一个分支，只不过方式有些不同。</p>
</blockquote>
<h4 id="merge" tabindex="-1"><a class="header-anchor" href="#merge" aria-hidden="true">#</a> merge</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git checkout feature
git merge master
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br></div></div><p>这样feature 分支中新的合并提交（merge commit）将两个分支的历史连在了一起
Merge 好在它是一个安全的操作。现有的分支不会被更改
每次合并上游更改时 feature 分支都会引入一个外来的合并提交。如果上游分支 非常活跃的话，这或多或少会污染你的分支历史</p>
<h4 id="rebase" tabindex="-1"><a class="header-anchor" href="#rebase" aria-hidden="true">#</a> Rebase</h4>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git checkout feature
git rebase master
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br></div></div><p>它会把整个 feature 分支移动到 master 分支的后面，有效地把所有 master 分支上新的提交并入过来
但是，rebase 为原分支上每一个提交创建一个新的提交，重写了项目历史，并且不会带来合并提交。</p>
<h2 id="rebase的优点和缺点" tabindex="-1"><a class="header-anchor" href="#rebase的优点和缺点" aria-hidden="true">#</a> rebase的优点和缺点</h2>
<h4 id="优点" tabindex="-1"><a class="header-anchor" href="#优点" aria-hidden="true">#</a> 优点</h4>
<p><strong>rebase最大的好处是你的项目历史会非常整洁</strong>
<strong>rebase 导致最后的项目历史呈现出完美的线性——你可以从项目终点到起点浏览而不需要任何的 fork。这让你更容易使用 git log、git bisect 和 gitk 来查看项目历史</strong></p>
<h4 id="缺点" tabindex="-1"><a class="header-anchor" href="#缺点" aria-hidden="true">#</a> 缺点</h4>
<p><strong>安全性，如果你违反了 rebase 黄金法则，重写项目历史可能会给你的协作工作流带来灾难性的影响</strong>
<strong>可跟踪性，rebase 不会有合并提交中附带的信息——你看不到 feature 分支中并入了上游的哪些更改交互式的rebase</strong>
<strong>交互式的 rebase 允许你更改并入新分支的提交。这比自动的 rebase 更加强大,因为它提供了对分支上提交历史完整的控制</strong></p>
<p>一般来说，这被用于将 feature 分支并入 master 分支之前，清理混乱的历史。</p>
<p>命令示例：</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git checkout feature
git rebase -i master
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br></div></div><p>它会打开一个文本编辑器，显示所有将被移动的提交：</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>pick 33d5b7a Message for commit #1
pick 9480b3d Message for commit #2

pick 5c67e61 Message for commit #3

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br></div></div><p>在这里可以编辑提交的记录，具体可以怎么编辑先不详说，见下文</p>
<p>保存后关闭文件，Git 会根据你的指令来执行 rebase</p>
<p>忽略不重要的提交会让你的 feature 分支的历史更清晰易读。这是 git merge 做不到的</p>
<h2 id="rebase黄金法则" tabindex="-1"><a class="header-anchor" href="#rebase黄金法则" aria-hidden="true">#</a> rebase黄金法则</h2>
<p><strong>绝不要在公共的分支上使用它！</strong>
在你运行 git rebase 之前，一定要问问你自己「有没有别人正在这个分支上工作？」。如果答案是肯定的，那就不能rebase</p>
<h4 id="强制推送" tabindex="-1"><a class="header-anchor" href="#强制推送" aria-hidden="true">#</a> 强制推送</h4>
<p>如果你想把 rebase 之后的 master 分支推送到远程仓库，Git 会阻止你这么做，因为两个分支包含冲突。但你可以传入 –force 标记来强行推送</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>git push --force
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><p>rebase在开发中的使用场景
rebase 可以或多或少应用在你们团队的 Git 工作流中
下面的命令对最新的 3 次提交进行了交互式 rebase：</p>
<p>git checkout feature
git rebase -i HEAD~3</p>
<p>你实际上没有移动分支——你只是将之后的 3 次提交合并了</p>
<p>交互式 rebase 是在你工作流中引入 git rebase 的的好办法，因为它只影响本地分支。其他开发者只能看到你已经完成的结果，那就是一个非常整洁、易于追踪的分支历史。</p>
<p>但同样的，这只能用在私有分支上。如果你在同一个 feature 分支和其他开发者合作的话，这个分支是公开的，你不能重写这个历史。</p>
<h4 id="如何选择使用merge还是rebase" tabindex="-1"><a class="header-anchor" href="#如何选择使用merge还是rebase" aria-hidden="true">#</a> 如何选择使用merge还是rebase</h4>
<p>你使用 rebase 之前需要知道的知识点都在这了。如果你想要一个干净的、线性的提交历史，没有不必要的合并提交，你应该使用 git rebase 而不是 git merge 来并入其他分支上的更改。</p>
<p>另一方面，如果你想要保存项目完整的历史，并且避免重写公共分支上的 commit， 你可以使用 git merge。两种选项都很好用，但至少你现在多了 git rebase 这个选择。</p>
<h3 id="交互式rebase的操作" tabindex="-1"><a class="header-anchor" href="#交互式rebase的操作" aria-hidden="true">#</a> 交互式rebase的操作</h3>
<p>例如开启交互式rebase合并最近三次提交</p>
<p>git checkout feature
git rebase -i HEAD~3</p>
<p>这是一个交互式rebase界面：</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>pick 07c5abd Introduce OpenPGP and teach basic usage
pick de9b1eb Fix PostChecker::Post#urls

pick 3e7ee36 Hey kids, stop all the highlighting

pick fa20af3 git interactive rebase, squash, amend



# Rebase 8db7e8b..fa20af3 onto 8db7e8b

#

# Commands:

# p, pick = use commit

# r, reword = use commit, but edit the commit message

# e, edit = use commit, but stop for amending

# s, squash = use commit, but meld into previous commit

# f, fixup = like "squash", but discard this commit's log message

# x, exec = run command (the rest of the line) using shell

#

# These lines can be re-ordered; they are executed from top to bottom.

#

# If you remove a line here THAT COMMIT WILL BE LOST.

#

# However, if you remove everything, the rebase will be aborted.

#

# Note that empty commits are commented out

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br><span class="line-number">7</span><br><span class="line-number">8</span><br><span class="line-number">9</span><br><span class="line-number">10</span><br><span class="line-number">11</span><br><span class="line-number">12</span><br><span class="line-number">13</span><br><span class="line-number">14</span><br><span class="line-number">15</span><br><span class="line-number">16</span><br><span class="line-number">17</span><br><span class="line-number">18</span><br><span class="line-number">19</span><br><span class="line-number">20</span><br><span class="line-number">21</span><br><span class="line-number">22</span><br><span class="line-number">23</span><br><span class="line-number">24</span><br><span class="line-number">25</span><br><span class="line-number">26</span><br><span class="line-number">27</span><br><span class="line-number">28</span><br><span class="line-number">29</span><br><span class="line-number">30</span><br><span class="line-number">31</span><br><span class="line-number">32</span><br><span class="line-number">33</span><br><span class="line-number">34</span><br><span class="line-number">35</span><br><span class="line-number">36</span><br><span class="line-number">37</span><br><span class="line-number">38</span><br><span class="line-number">39</span><br><span class="line-number">40</span><br><span class="line-number">41</span><br><span class="line-number">42</span><br><span class="line-number">43</span><br></div></div><p>上面的互动界面，先列出当前分支最新的4个commit（越下面越新）。每个commit前面有一个操作命令，默认是pick，表示该行commit被选中，要进行rebase操作。4个commit的下面是一大堆注释，列出可以使用的命令。</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>* pick：正常选中
* reword：选中，并且修改提交信息；
* edit：选中，rebase时会暂停，允许你修改这个commit（参考这里）
* squash：选中，会将当前commit与上一个commit合并
* fixup：与squash相同，但不会保存当前commit的提交信息
* exec：执行其他shell命令
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br></div></div><p>上面这6个命令当中，squash和fixup可以用来合并commit。先把需要合并的commit前面的动词，改成squash（或者s）</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>pick 07c5abd Introduce OpenPGP and teach basic usage
s de9b1eb Fix PostChecker::Post#urls

s 3e7ee36 Hey kids, stop all the highlighting

pick fa20af3 git interactive rebase, squash, amend
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br></div></div><p>这样一改，执行后，当前分支只会剩下两个commit。第二行和第三行的commit，都会合并到第一行的commit。提交信息会同时包含，这三个commit的提交信息。</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code># This is a combination of 3 commits.
# The first commit's message is:

Introduce OpenPGP and teach basic usage



# This is the 2nd commit message:

Fix PostChecker::Post#urls

# This is the 3rd commit message:

Hey kids, stop all the highlighting


</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br><span class="line-number">7</span><br><span class="line-number">8</span><br><span class="line-number">9</span><br><span class="line-number">10</span><br><span class="line-number">11</span><br><span class="line-number">12</span><br><span class="line-number">13</span><br><span class="line-number">14</span><br><span class="line-number">15</span><br><span class="line-number">16</span><br></div></div><p>如果将第三行的squash命令改成fixup命令。</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>pick 07c5abd Introduce OpenPGP and teach basic usage
s de9b1eb Fix PostChecker::Post#urls

f 3e7ee36 Hey kids, stop all the highlighting

pick fa20af3 git interactive rebase, squash, amend
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br></div></div><p>运行结果相同，还是会生成两个commit，第二行和第三行的commit，都合并到第一行的commit。但是，新的提交信息里面，第三行commit的提交信息，会被注释掉</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code># This is a combination of 3 commits.
# The first commit's message is:

Introduce OpenPGP and teach basic usage



# This is the 2nd commit message:

Fix PostChecker::Post#urls

# This is the 3rd commit message:

# Hey kids, stop all the highlighting
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br><span class="line-number">7</span><br><span class="line-number">8</span><br><span class="line-number">9</span><br><span class="line-number">10</span><br><span class="line-number">11</span><br><span class="line-number">12</span><br><span class="line-number">13</span><br><span class="line-number">14</span><br></div></div><p>Pony Foo提出另外一种合并commit的简便方法，就是先撤销过去5个commit，然后再建一个新的。</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>$ git reset HEAD~5
$ git add .

$ git commit -am "Here's the bug fix that closes #28"

$ git push --force
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br></div></div><p>squash和fixup命令，还可以当作命令行参数使用，自动合并commit。</p>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code>$ git commit --fixup
$ git rebase -i --autosquash

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br></div></div><p>推送到远程仓库
合并commit后，就可以推送当前分支到远程仓库了</p>
<p>$ git push --force origin myfeature</p>
<p>git push命令要加上force参数，因为rebase以后，分支历史改变了，跟远程分支不一定兼容，有可能要强行推送</p>
<p>提交到远程仓库以后，就可以发出 Pull Request 到master分支，然后请求别人进行代码review，确认可以合并到master。</p>
<p>如果你从 master 分支拉了个feature分支出来，然后你提交了几个commit，这时候刚好有人把他的分支和到了master，</p>
<p>这时候master 分支就比你拉的分支多了几个commit，如果你这时候在feature分支rebase master的话</p>
<p>就会把你当前的这几个commit 放到那人的commit后面。</p>
</template>
