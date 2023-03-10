# 关于如何使用合适的前端降低应用成本的指南

> 原文：<http://web.archive.org/web/20230307163032/https://www.netguru.com/blog/guide-on-how-to-reduce-your-app-costs-with-the-right-frontend>

 介绍

在规划阶段，应用程序的成本可能是您要考虑的关键因素之一。如果您做出正确的决定，有时小的调整可以降低应用程序的总成本。总有改进的空间，也总是做出改变变得更好的好时机。我会尽量给你一些细节，告诉你在构建前端时应该考虑哪些事情，应该避免哪些事情，以及怎样做才能降低开发过程的成本。

## 应用程序的成本由什么组成？

要理解问题，我们需要分析原因。毫不奇怪，你的前端成本只是开发时间乘以每小时的费用。文章可以到此结束，但这并不是有些项目贵，有些项目便宜的原因。因此，我将试着向您介绍依赖于开发人员在构建应用程序上花费的时间的因素。

*   功能的数量和复杂性——与集成了多个外部 API 的复杂财务应用程序相比，包含身份验证和一些其他常见功能的简单应用程序需要的工作量更少。将两者结合起来需要大量的工作。
*   内部业务逻辑的数量——在创建应用程序之前，开发人员大多对他们的应用程序将要运行的行业知之甚少或一无所知。他们必须了解业务环境、功能需求、客户需求，并将一切转换成代码。这是一个艰难的过程，需要就细节进行大量磋商。
*   架构——我不想深入分析哪种架构更好，因为没有好的、普适的答案。我们必须记住，多个开发人员将在项目中工作，选择的架构应该对每个人都很清楚。从长远来看，处理好这件事是值得的。有了一个好的架构，在应用程序中查找数据就更容易了，而且不需要开发人员为每一个功能去探索它。
*   文档——关于项目的信息，例如如何在本地设置它的技巧、使用的模式、解决方案以及许多其他东西。有时它被边缘化了，尤其是当有压力要快速开发产品的时候。从更广泛的角度来看，忽视文档可能会导致混乱，并且会更加耗时。每次开发人员在项目中遇到一些问题，他都会从实际工作中分心。
*   代码的复杂性——一个模块/组件中有多少逻辑，以及如何(如果有的话)将它分割成更小的代码块。这也可能意味着开发人员需要投入多少精力来添加/重构功能。当相对简单的任务难以完成时，过度复杂会导致极端情况。从项目开始到结束都是同一批开发人员，这种情况很少见。每当一个新人加入，他可能会被复杂性吓到，他的生产力会在很长一段时间内非常低。这也会迫使你雇佣或指派更有经验的开发人员。
*   使用的技术——根据你的选择，它可以加快或减慢你的开发。您需要特别记住两个方面:什么技术最适合您的项目，以及您的开发人员已经知道了什么。将两者结合起来是最好的，但是有时开发者需要学习新技术，这些新技术会导致他们以前没有面对过的问题。
*   一个项目需要多长时间——预测的持续时间在开发一个应用程序的过程中实施了一个变化框方法。长期项目需要很好地配置、管理和记录，以包容将从事该项目的开发人员。否则，可能会出现大问题。
*   开发者——最重要的一点。有些人认为一个有经验的开发人员可能会被几个没什么经验的程序员所取代，他们的工资会更低。但是在实践中，这几乎总是会导致问题，需要由另一个团队来重构。您知道开发人员将大部分时间花在代码重构上吗？

上面提到的因素会减少/增加你的前端开发人员花费在任务上的时间。意识到它们并以正确的方式照顾它们可以确保你对你的储蓄感到满意。但是有一个最重要的问题。 ***作为前端开发者，你能做些什么来降低 app 成本？***

## **关注你的架构**

不要害怕雇佣技术领导，他会为你的项目选择最好的技术和工具。错误的工具会让您付出很多额外的工作，甚至需要迁移到另一种可以满足您需求的技术。

## **构建直观的项目结构**

它应该是细粒度的、一致的、正确地划分到文件夹中，并且易于扩展。无论何时我们建立一个项目，我们都需要考虑它不仅在几周内，而且在几年内会是什么样子。

![Project Structure 1](img/7f9e6ee417acdfc2457516d13edd5668.png)

在上面的例子中，项目结构(Vue、Typescript、Vuex、Vue-router)在 src 目录中有四个主要的子文件夹:

*   组件-在单独的文件夹中包含 UI 元素

*   静态-包含不变的数据(例如要显示和迭代的窗格列表)

*   存储-包含 Vuex 逻辑，并被分成模块文件夹

*   视图-包含 Vue-路由器页面

这些文件夹中不包括其他配置文件。这种结构易于理解和扩展。

## **更新自述文件**

如果您还没有在这个文件中描述项目实践，请更改它！每个项目都需要有一个真实的来源，可以告诉其他前端开发人员关于最佳实践、项目配置、结构和其他东西，以避免团队中的误解。这里应该包括什么？人们问的一切。假设人们可能不知道许多事情，每件事情都应该深入描述。https://github.com/matiassingers/awesome-readme 有很好的自述文件的例子。

## **记录业务需求**

这不是一种常见的方法，但我看到很多时候，一些人什么都知道，而其他人却不知道。这是不健康的——知识必须在团队中传播。

## **最大化你的代码质量**

有很多工具可以帮助你实现这个目标:ide(pre tiers，code formatters)，服务器 CI 工具(Travis，Jenkins，code climate)，linters (eslint，tslint)，precommit/prepush 工具，这些工具可以分析你的代码并阻止任何不符合项目代码约定的东西。

## **关注前端生产力**

使用快捷方式、扩展(IDE 和浏览器)，为开发人员设定一个他们不会分心的每日专注时间，自动化重复的过程，最大限度地减少分心，不要忘记你的健康——每小时休息一会儿，让你的头脑清醒，睡个好觉。

## **使代码可重用**

积极地懒惰。你在你的代码中看到可以重用的东西了吗？不要犹豫去做！它节省了很多时间。

## **考虑长远**

疯狂地追求最后期限会导致代码质量下降。所以要注意你代码的质量，仔细检查代码。质量差的代码更难修改或调试。

## **测试你的代码**

并不意味着越多越好。我们可以测试几乎所有的东西，但是这不是正确的方法(除非它是一个不能失败的医疗应用)。尤其是当需求是动态的时候。正确的测试意味着数据的每个关键部分都被测试覆盖并且是稳定的。此外，bug 修复的一部分应该是编写适当的测试来避免将来的问题。测试还能让你更好地了解代码和应用程序。

## **遵循最佳实践**

有很多规则可以写成一篇文章。简而言之，它是:自我解释的代码，DRY，模块模式，避免不必要的注释，从 console.logs 和未使用的代码/文件夹/文件/资源中清理代码，使用正确的代码缩进，尽可能使代码好，不要等待重构(调试更难，这是获得意大利面条代码的一种方式)，使用开发工具，ES6/ES7，框架，CSS 预处理程序和代码约定，在专用文件夹中组织代码。还有很多技术可以让代码更简洁、更友好，我鼓励你去学习。

## **使用故事书**

一个外部库，允许你单独存储你的 UI 组件。它有助于维持更大的项目和保持干燥。每当我加入项目时，我都花太多时间寻找可以节省时间的组件。这正是故事书来拯救的时候！

## **使用打字稿**

Typescript 是 Javascript 的超集，它引入了静态类型。它有很多优点。最让我欣赏的是 IDE 惊人的支持，它能温和地捕捉你所有的错误，迫使你写出更好的代码，而且在重构过程中也很棒。代码中的类型是文档，它可以加速您的工作，并使您免于日志记录和调试。我还想指出的是，Typescript 可以逐渐引入到项目中，这是一个很大的优势。

## **避免 HDD(炒作驱动开发)**

这是一种开发者根据当前趋势选择技术的现象。它尤其指前端世界，在那里我们有大量的新技术和新东西。技术决策对创建和维护项目有着至关重要的影响。因此，尽量避免实施可能阻碍您工作的未经证实的解决方案。[在这里](http://web.archive.org/web/20220929112437/https://blog.daftcode.pl/hype-driven-development-3469fc2e9b22)你可以找到一篇关于硬盘的精彩文章。

![Hype Driven Development](img/ac54c7532d55f7ac02f6cebeb430169d.png)

来源:[https://blog . daft code . pl/hype-driven-development-3469 fc 2 e9 b 22](http://web.archive.org/web/20220929112437/https://blog.daftcode.pl/hype-driven-development-3469fc2e9b22)

## **总结**

我们已经介绍了应用程序的成本构成，以及作为前端开发人员，您可以做些什么来降低应用程序的成本。每一点都是指一个行动，它可以节省你的时间，使你的工作更容易，使你更满意，并保护你的项目不被新的团队成员访问。一个快乐的开发人员能够很容易地在他的项目中找到任何数据，他就是一个高效的开发人员。请记住，这永远是引入质量变革的好时机。我祝你在那个目标上好运！

* * *

照片由[Immo Wegmann](http://web.archive.org/web/20220929112437/https://unsplash.com/photos/tYvUNvcGa-c?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)上 [Unsplash](http://web.archive.org/web/20220929112437/https://unsplash.com/search/photos/computer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)