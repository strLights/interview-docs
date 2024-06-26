<template><h1 id="flex-布局原理" tabindex="-1"><a class="header-anchor" href="#flex-布局原理" aria-hidden="true">#</a> flex 布局原理</h1>
<h2 id="原理" tabindex="-1"><a class="header-anchor" href="#原理" aria-hidden="true">#</a> 原理</h2>
<h4 id="设计" tabindex="-1"><a class="header-anchor" href="#设计" aria-hidden="true">#</a> 设计</h4>
<p>Flex排版的核心是display:flex和flex属性，它们配合使用。具有display:flex的元素可称为flex容器，它的子元素或者盒被称作flex项。
flex项如果有flex属性，就会根据flex方向代替元素的宽和高，用剩余空间填充子元素尺寸，这就是典型的“根据外部容器决定内部尺寸”的思路。</p>
<h4 id="实现" tabindex="-1"><a class="header-anchor" href="#实现" aria-hidden="true">#</a> 实现</h4>
<p>首先，Flex布局支持横向和纵向，这样就需要做一个抽象，我们把Flex延伸的方向称为“主轴”，把跟它垂直的方向称为“交叉轴”。这样，flex项中的width和height就会称为交叉轴尺寸或者主轴尺寸。</p>
<p>同时，Flex又支持反向排布，这样我们又需要抽象出交叉轴起点、交叉轴终点、主轴起点、主轴终点，它们可能是容器top、left、bottom、right。在实际代码中，是用flex-start和flex-end表示主轴和交叉轴的起点和终点。</p>
<p>另外，Flex布局中有一种特殊的情况，那就是flex容器没有被指定主轴尺寸，这个时候，实际上Flex属性完全没有用了，所有Flex尺寸都可以被当做0来处理，Flex容器的主轴尺寸等于其它所有flex项主轴尺寸之和。</p>
<p>上面是Flex布局的实现思想，具体的排版细节可以分为下面三个步骤。</p>
<h5 id="第一步-把flex项分行。" tabindex="-1"><a class="header-anchor" href="#第一步-把flex项分行。" aria-hidden="true">#</a> 第一步，把flex项分行。</h5>
<p>有Flex属性的flex项可以暂且认为主轴尺寸为0，所以，它一定可以放进当前行。</p>
<p>接下来把flex项逐个放入行，不允许换行的话，就直接把所有flex项放进同一行。允许换行的话，就先设定主轴剩余空间为Flex容器主轴尺寸，每放入一个flex项就把主轴剩余空间减掉它的主轴尺寸，直到某个flex项放不进去为止，换下一行，重复前面动作。</p>
<p>分行过程中，会顺便对每一行计算两个属性：交叉轴尺寸和主轴剩余空间，交叉轴尺寸是本行所有交叉轴尺寸的最大值，而主轴剩余空间前面已经说过。</p>
<h5 id="第二步-计算每个flex项的主轴尺寸和位置。" tabindex="-1"><a class="header-anchor" href="#第二步-计算每个flex项的主轴尺寸和位置。" aria-hidden="true">#</a> 第二步，计算每个flex项的主轴尺寸和位置。</h5>
<p>如果Flex容器是不允许换行的，并且最后主轴尺寸超出了Flex容器，就要做等比缩放。如果Flex容器有多行，那么根据前面的分行算法，必然有主轴剩余空间，这时候，我们要找出本行所有的带Flex属性的flex项，把剩余空间按Flex比例分给它们。</p>
<p>之后，就可以根据主轴排布方向，确定每个flex项的主轴位置坐标了。</p>
<p>如果本行完全没有带flex属性的flex项，justify-content机制就要生效了，它的几个不同的值会影响剩余空白如何分配。</p>
<h5 id="第三步-计算flex项的交叉轴的尺寸和位置。" tabindex="-1"><a class="header-anchor" href="#第三步-计算flex项的交叉轴的尺寸和位置。" aria-hidden="true">#</a> 第三步，计算flex项的交叉轴的尺寸和位置。</h5>
<p>交叉轴的计算首先是根据align-content计算每一行的位置，这跟justify-content类似。再根据align-items和flex项的align-self来确定每个元素在行内的位置。</p>
<p>计算完主轴和交叉轴，每个flex项的坐标、尺寸就都确定了，这样就完成了整个的flex布局。</p>
</template>
