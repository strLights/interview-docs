<template><h2 id="_1、pm2是什么" tabindex="-1"><a class="header-anchor" href="#_1、pm2是什么" aria-hidden="true">#</a> 1、PM2是什么</h2>
<p>PM2 是一个带有负载均衡功能的 Node 应用的进程管理器。我们都知道nodejs是单进程执行的，当程序出现错误死掉之后需要能够自动，这时候就需要PM2了。当然进程管理工具有很多，例如forever等等；</p>
<p>入门教程
挑我们最爱的express应用来举例。一般我们都是通过npm start启动应用，其实就是调用node ./bin/www。那么，换成pm2就是
注意，这里用了--watch参数，意味着当你的express应用代码发生变化时，pm2会帮你重启服务，多贴心。
pm2 start ./bin/www --watch</p>
<h3 id="_2、主要特性" tabindex="-1"><a class="header-anchor" href="#_2、主要特性" aria-hidden="true">#</a> 2、主要特性</h3>
<p>1）启动多子进程，充分使用CPU</p>
<p>2）子进程之间负载均衡</p>
<p>3）0秒重启</p>
<p>4）界面友好</p>
<p>5）提供进程交互（例如：监控）接口</p>
<h3 id="_3、安装" tabindex="-1"><a class="header-anchor" href="#_3、安装" aria-hidden="true">#</a> 3、安装</h3>
<div class="language-javascript ext-js line-numbers-mode"><pre v-pre class="language-javascript"><code>npm install pm2 <span class="token operator">-</span>g
</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br></div></div><h3 id="_4、使用" tabindex="-1"><a class="header-anchor" href="#_4、使用" aria-hidden="true">#</a> 4、使用</h3>
<div class="language-javascript ext-js line-numbers-mode"><pre v-pre class="language-javascript"><code>pm2 start app<span class="token punctuation">.</span>js <span class="token operator">-</span>i <span class="token number">4</span> <span class="token operator">-</span>n customer   <span class="token comment">//-i 4启动4个进程 -n customer指定进程名称</span>

pm2 list  <span class="token comment">//查看进程状态</span>

pm2 info customer <span class="token comment">//查看单个进程的详细启动信息</span>

pm2 logs customer   <span class="token comment">//查看实时日志</span>

pm2 restart  all <span class="token operator">||</span> customer <span class="token comment">//直接重启进程</span>

pm2 reload customer  <span class="token comment">//0秒停机重启进程</span>

pm2 gracefulReload customer  <span class="token comment">//等待网络连接处理完之后重启进程;避免请求处理中断导致可能的业务错误</span>

pm2 <span class="token keyword">delete</span> all<span class="token operator">|</span>customer <span class="token comment">//删除所有的或者指定的进程</span>

pm2 stop  all <span class="token operator">||</span>customer  <span class="token comment">//停止进程，但是进程仍然存在</span>

pm2 monit    <span class="token comment">//监控进程信息</span>

pm2 update <span class="token comment">//升级pm2之后需要升级老版本启动的进程</span>

pm2 start start<span class="token punctuation">.</span>json <span class="token comment">//通过配置文件启动 </span>

start<span class="token punctuation">.</span>json示例

<span class="token punctuation">[</span><span class="token punctuation">{</span>

    <span class="token string">"name"</span> <span class="token operator">:</span> <span class="token string">"project"</span><span class="token punctuation">,</span>    <span class="token comment">//进程名称</span>

    <span class="token string">"script"</span> <span class="token operator">:</span> <span class="token string">"app.js"</span><span class="token punctuation">,</span>    <span class="token comment">//入口文件</span>

    <span class="token string">"exec_mode"</span> <span class="token operator">:</span> <span class="token string">"cluster"</span><span class="token punctuation">,</span> <span class="token comment">//模式</span>

    <span class="token string">"instances"</span> <span class="token operator">:</span> <span class="token number">3</span><span class="token punctuation">,</span>   <span class="token comment">//进程实例个数</span>

    <span class="token string">"cwd"</span> <span class="token operator">:</span> <span class="token string">"./project/"</span><span class="token punctuation">,</span>  <span class="token comment">//路径</span>

    <span class="token string">"env"</span><span class="token operator">:</span> <span class="token punctuation">{</span>   <span class="token comment">//环境变量</span>

        <span class="token string">"NODE_ENV"</span><span class="token operator">:</span> <span class="token string">"development"</span><span class="token punctuation">,</span> 

        <span class="token string">"DEBUG"</span><span class="token operator">:</span> <span class="token string">"*"</span><span class="token punctuation">,</span> <span class="token comment">//打印debug日志</span>

        <span class="token string">"DEBUG_FD"</span> <span class="token operator">:</span> <span class="token number">1</span> <span class="token comment">//debug日志默认输出到process.stderr；该参数将日志输出到process.stdout</span>

    <span class="token punctuation">}</span>

<span class="token punctuation">}</span><span class="token punctuation">]</span>

</code></pre><div class="line-numbers" aria-hidden="true"><span class="line-number">1</span><br><span class="line-number">2</span><br><span class="line-number">3</span><br><span class="line-number">4</span><br><span class="line-number">5</span><br><span class="line-number">6</span><br><span class="line-number">7</span><br><span class="line-number">8</span><br><span class="line-number">9</span><br><span class="line-number">10</span><br><span class="line-number">11</span><br><span class="line-number">12</span><br><span class="line-number">13</span><br><span class="line-number">14</span><br><span class="line-number">15</span><br><span class="line-number">16</span><br><span class="line-number">17</span><br><span class="line-number">18</span><br><span class="line-number">19</span><br><span class="line-number">20</span><br><span class="line-number">21</span><br><span class="line-number">22</span><br><span class="line-number">23</span><br><span class="line-number">24</span><br><span class="line-number">25</span><br><span class="line-number">26</span><br><span class="line-number">27</span><br><span class="line-number">28</span><br><span class="line-number">29</span><br><span class="line-number">30</span><br><span class="line-number">31</span><br><span class="line-number">32</span><br><span class="line-number">33</span><br><span class="line-number">34</span><br><span class="line-number">35</span><br><span class="line-number">36</span><br><span class="line-number">37</span><br><span class="line-number">38</span><br><span class="line-number">39</span><br><span class="line-number">40</span><br><span class="line-number">41</span><br><span class="line-number">42</span><br><span class="line-number">43</span><br><span class="line-number">44</span><br><span class="line-number">45</span><br><span class="line-number">46</span><br><span class="line-number">47</span><br><span class="line-number">48</span><br><span class="line-number">49</span><br><span class="line-number">50</span><br></div></div></template>
