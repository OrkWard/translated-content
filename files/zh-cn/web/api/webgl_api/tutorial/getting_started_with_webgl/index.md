---
title: 初识 WebGL
slug: Web/API/WebGL_API/Tutorial/Getting_started_with_WebGL
---

{{DefaultAPISidebar("WebGL")}} {{Next("Web/API/WebGL_API/Tutorial/Adding_2D_content_to_a_WebGL_context")}}

[WebGL](http://www.khronos.org/webgl/) 使得在支持 HTML 的 [`canvas`](/zh-CN/HTML/Canvas) 标签的浏览器中，不需要安装任何插件，便可以使用基于 [OpenGL ES](http://www.khronos.org/opengles/) 2.0 的 API 进行 2D 和 3D 渲染。

WebGL 程序包括用 JavaScript 写的控制代码，以及在图形处理单元（GPU, Graphics Processing Unit）中执行的着色代码（GLSL，注：GLSL 为 OpenGL 着色语言）。WebGL 元素可以和其他 HTML 元素混合使用，并且可以和网页其他部分或者网页背景结合起来。

本文将介绍 WebGL 的基本用法。此处假定您对三维图形方面的数学知识已经有一定的理解，本文也不会介绍 3D 图像概念本身。

文中使用的代码可以在[这里](https://github.com/mdn/dom-examples/tree/main/webgl-examples/tutorial)下载。

值得注意的是，此处介绍的是 WebGL 本身，而 [THREE.js](https://threejs.org/) 和 [BABYLON.js](https://www.babylonjs.com/) 等框架封装了 WebGL，提供了各个平台之间的兼容性。使用这些框架而非原生的 WebGL 可以更容易地开发 3D 应用和游戏。

## 准备 3D 渲染

首先，创建两个文件：

- "index.html"
- "webgl-demo.js"

"index.html" 文件包含以下内容：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>WebGL Demo</title>
    <script src="webgl-demo.js" type="module"></script>
  </head>

  <body>
    <canvas id="glcanvas" width="640" height="480"></canvas>
  </body>
</html>
```

这里创建了一个 canvas 标签用于进行绘制。

### 准备 WebGL 上下文

"webgl-demo.js" 文件包含以下内容：

```js
main();

//
// 从这里开始
//
function main() {
  const canvas = document.querySelector("#glcanvas");
  // 初始化 WebGL 上下文
  const gl = canvas.getContext("webgl");

  // 确认 WebGL 可用的情况下继续
  if (gl === null) {
    alert(
      "初始化失败，你的浏览器或者设备可能不支持 WebGL。"
    );
    return;
  }

  // 设置清除颜色为黑色，不透明
  gl.clearColor(0.0, 0.0, 0.0, 1.0);
  // 使用设置的颜色清除颜色缓冲
  gl.clear(gl.COLOR_BUFFER_BIT);
}
```

当 script 标签加载时，执行 `main()` 函数。它初始化 WebGL 上下文，开始渲染内容。

我们做的第一件事是获取 canvas 标签的引用，赋值给 `canvas` 变量。

随后，我们调用方法 [`getContent('webgl')`](/zh-CN/docs/Web/API/HTMLCanvasElement/getContext) 尝试获取一个 [`WebGLRenderingContext`](/zh-CN/docs/Web/API/WebGLRenderingContext) 对象，以获取一个 WebGL 上下文。如果浏览器不支持 WebGL，`getContent()` 方法将返回 `null`，此时我们向用户展示此信息并退出。

如果上下文成功初始化，`gl` 变量现在是一个对该 canvas 中 WebGL 上下文的引用。此时我们设置清除颜色为黑色，并将整个上下文清除为该颜色（即用该颜色填充整个 canvas）。

此时你已经成功初始化了 WebGL 上下文。你现在应该看到一个准备好绘制任何东西的大纯黑方框。

{{EmbedGHLiveSample('dom-examples/webgl-examples/tutorial/sample1/index.html', 670, 510) }}

[查看完整的源码](https://github.com/mdn/dom-examples/tree/main/webgl-examples/tutorial/sample1) | [在新标签页中查看演示](https://mdn.github.io/dom-examples/webgl-examples/tutorial/sample1/)

## 参见

- [WebGL 介绍](https://dev.opera.com/articles/introduction-to-webgl-part-1/)： 由 Luz Caballero 所著，发布在 dev.opera.com。这篇文章说明 WebGL 是什么，解释了 WebGL 是如何工作的（介绍了渲染管线的概念），并且介绍了一些 WebGL 库。
- [WebGL 基础](http://webglfundamentals.org/)
- [现代 OpenGL 介绍](http://duriansoftware.com/joe/An-intro-to-modern-OpenGL.-Table-of-Contents.html) ：由 Joe Groff 写的一系列关于 OpenGL 的不错的文章，提供了一个清晰的介绍，从 OpenGL 的历史到图形管线概念，也包括一些说明 OpenGL 如何工作的例子，如果你对 OpenGL 没有任何概念的话，这是不错的出发点。

{{Next("Web/API/WebGL_API/Tutorial/Adding_2D_content_to_a_WebGL_context")}}
