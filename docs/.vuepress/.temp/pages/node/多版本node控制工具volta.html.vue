<template><h2 id="下载" tabindex="-1"><a class="header-anchor" href="#下载" aria-hidden="true">#</a> 下载</h2>
<div class="language-javascript ext-js line-numbers-mode"><pre v-pre class="language-javascript"><code>curl https<span class="token operator">:</span><span class="token operator">/</span><span class="token operator">/</span>get<span class="token punctuation">.</span>volta<span class="token punctuation">.</span>sh <span class="token operator">|</span> bash
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><p>您可以使用两个命令控制由 Volta 工具链管理的工具：volta install和volta uninstall。</p>
<p>安装节点引擎
要将工具安装到您的工具链，您需要设置该工具的默认版本。Volta 将始终使用此默认值，除非您在已将 Volta 配置为使用不同版本的项目目录中工作。当您选择默认版本时，Volta 也会将该版本下载到本地缓存。</p>
<p>例如，您可以选择一个确切的版本node作为您的默认版本：</p>
<p>volta install node@14.15.5
你不需要指定一个精确的版本，在这种情况下，Volta 会选择一个合适的版本来满足你的要求：</p>
<p>volta install node@14
您还可以指定latest— 甚至完全不使用版本，Volta 将选择最新的 LTS 版本：</p>
<p>volta install node</p>
<p>固定节点引擎
该volta pin命令允许您为项目选择 Node 引擎和包管理器版本：</p>
<p>volta pin node@12.20.2
volta pin yarn@1.19.2</p>
<p>Volta 将其存储在您的文件中package.json，因此您可以将您选择的工具提交给版本控制：
&quot;volta&quot;: {
&quot;node&quot;: &quot;12.20.2&quot;,
&quot;yarn&quot;: &quot;1.19.2&quot;
}</p>
<p>这样，使用 Volta 处理项目的每个人都会自动获得您选择的相同版本。
node --version # 12.20.2
yarn --version # 1.19.2</p>
<p>volta list // 查看当前环境依赖
volta list all // 查看所有环境依赖</p>
<p>volta 官网[https://docs.volta.sh/guide/getting-started]</p>
<p>如在mac 上重启 zsh 后还一直报  volta command is not found  试试如下：</p>
<h2 id="给zsh-shell-设置环境变量" tabindex="-1"><a class="header-anchor" href="#给zsh-shell-设置环境变量" aria-hidden="true">#</a> 给zsh shell 设置环境变量</h2>
<p>vi ~/.zshrc
// 如果跟目录没有.zshrc的话，执行下面的命令
cash  ~/.zshrc
vi ~/.zshrc
在最下面添加</p>
<div class="language-javascript ext-js line-numbers-mode"><pre v-pre class="language-javascript"><code><span class="token keyword">export</span> <span class="token constant">VOLTA_HOME</span><span class="token operator">=</span><span class="token string">"$HOME/.volta"</span>
<span class="token keyword">export</span> <span class="token constant">PATH</span><span class="token operator">=</span><span class="token string">"$VOLTA_HOME/bin:$PATH"</span>
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br></div></div><p>重新打开 shell 窗口或重载shell
即可
source ~/.zshrc</p>
</template>
