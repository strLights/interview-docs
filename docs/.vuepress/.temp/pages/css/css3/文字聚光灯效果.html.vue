<template>  <div id="app">qdleader</div>
```css
 #app {
            font-weight: bold;
            width: max-content;
            color: gray;
            position: relative;
            text-transform: uppercase;
            font-size: 100px;
        }
<pre><code>    #app::after {
        content: &quot;qdleader&quot;;
        position: absolute;
        inset: 0;
        background-image: linear-gradient(to right, rgb(236, 72, 153), rgb(239, 68, 68), rgb(234, 179, 8));
        background-clip: text;
        -webkit-background-clip: text;
        color: transparent;
        clip-path: ellipse(100px 100px at 0 50%);
        animation: qd 3s ease-in infinite;
    }

    @keyframes qd {
        50% {
            clip-path: ellipse(100px 100px at 100% 50%);
        }

        to {
            clip-path: ellipse(100px 100px at 0% 50%);
        }
    }
</code></pre>
<div class="language-text ext-text line-numbers-mode"><pre v-pre class="language-text"><code></code></pre><div class="line-numbers" aria-hidden="true"></div></div></template>
