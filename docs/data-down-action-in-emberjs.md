# 数据下降动作...在 Emberjs -使用 Ember。事件

> 原文：<http://web.archive.org/web/20230307163032/https://www.netguru.com/blog/data-down-action-in-emberjs>

 如果你已经使用 Ember 有一段时间了，这篇文章的主题对你来说就像异端邪说。数据下行动作下行？不会吧！另一方面，如果你不熟悉这个概念，你可能想知道这四个词是什么意思。

数据向下操作向上(DDAU)是今年[月](http://web.archive.org/web/20221007200007/https://www.netguru.com/services/vue-js-development)的一个最佳实践概念。它假设您的数据从上(数据的所有者，如路由)流向下(数据的呈现者，如组件)。另一方面，**动作改变来自这些动作的接收者的数据流，从用户**(像组件的按钮)到负责执行它们的所有者(像路由)。这种架构应该有助于您维护代码和应用程序。我是 DDAU 的忠实粉丝和支持者，但我也遇到过它不适用的边缘案例。

那么，为什么要以不同的方式设计数据流呢？基本上，有时动作不是由用户直接在组件上触发的。假设我们有一个可以通过键盘控制的待办事项列表。用户可以在列表中上下移动，并通过单击 Enter 扩展描述。我们希望它独立于当前有焦点的 DOM 元素来控制。所以我们使用一些插件，在控制器层面上神奇地拦截键盘事件(具体如何并不重要)。要查看大图，看看这个[余烬旋转](http://web.archive.org/web/20221007200007/https://ember-twiddle.com/dc85ac9d49e49c5663a1?numColumns=1&openFiles=twiddle.json%2C)，它在底部模拟了上/下/回车键。那么，当直接接收到控制器时，我们如何在当前活动的组件上触发一个动作呢？

这是我们可以利用数据下降、行动下降的地方。

## 可组合组件

每次我在写或谈论组件和数据流时，我都忍不住要提到 Miguel Camba 的一个非常好的演示，叫做 T2 的可组合组件。简单总结一下这个想法——Miguel 设法通过产生组件的公共 API 来提供一种恢复动作流的极好方法。**这让你可以通过处理公共 API 来使用它，例如在另一个组件中，在 yielding one** 中呈现:

不幸的是，这种用法有限。它不能用在我们的用例中。尽管它很聪明，但它只利用了 JavaScript 闭包，而真正的动作执行者是屈服组件中的 DOM 元素。我们希望在不构建任何会指出最终接收者的闭包的情况下处理事件。

## 烬。事件

什么是[灰烬。事件](http://web.archive.org/web/20221007200007/http://emberjs.com/api/classes/Ember.Evented.html)？你听说过吗？这是一个可以在任何你想要的 Ember 对象中使用的 mixin。它提供了一个非常简单但功能强大的 API 来触发和接收浏览器文档中的事件。

Ember 的最佳用例是什么？事件？创建一个混合在 Ember.Evented 中的 Ember 服务。然后，我们可以使用它作为任何我们希望能够与之通信的对象之间的代理。在我们的例子中，**我们将把服务注入到一个控制器中，当按键发生时**触发控制器上的事件。另一方面，我们将在每个应该对这些事件执行某些操作的组件中监听这些事件。这种简单的模式允许您在由于父子关系而无法轻松通信的对象之间进行通信。[在这里你可以查看服务、组件和控制器的完整代码](http://web.archive.org/web/20221007200007/https://ember-twiddle.com/dc85ac9d49e49c5663a1?numColumns=3&openFiles=application.controller.js%2Ctodos-list.component.js%2Ckeyboard-dispatcher.service.js)。下面你可以看到一小段:

其背后的逻辑相当明显。基本上，我们在运行`on`时所做的就是将方法添加到存储所有监听器的元对象中。当触发事件时，它遍历侦听器数组，并直接从元对象开始以相反的顺序执行每个函数。简单，但功能强大。

## 摘要

数据向下操作向下不是我们应该经常使用的模式，因为它会给我们的应用程序带来难以预料的后果。**当我们忘记通过在对象** destroy 上运行`off`来删除监听器时，也很容易引入内存泄漏。烬。Evented 更适合边缘情况的解决方案。意识到这些可能性并理解它们是如何工作的是很有用的。

你用过 Ember 吗？在你的工作中发生了什么？你碰到过这种模式的一些问题吗？滴个评论，分享一下经验吧！

如果你对 Ember.js 隐藏的机会和陷阱感兴趣，请查看我的关于 Ember Run Loop 的电子书。