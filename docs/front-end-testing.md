# 前端测试:2022 年及以后的指南

> 原文：<http://web.archive.org/web/20230307163032/https://www.netguru.com/blog/front-end-testing>

 随着越来越多的企业寻求提供以技术为基础的产品和服务，加载速度、带宽消耗和其他性能因素对于确保客户获得他们期望的体验变得至关重要。

这使得前端测试成为软件开发团队关注的[工作流程的关键部分，确保你的技术在其整个生命周期中的质量。](/web/20220926185535/https://www.netguru.com/blog/stages-of-software-development)

本文包含了您需要了解的关于前端测试的一切，以及如何将它应用到您最新的技术产品和应用程序中。

## 什么是前端测试？

首先，我们所说的前端测试是指什么？

前端一般包括通过使用不同的技术(如 HTML、CSS 或 JavaScript)开发网站的图形用户界面(GUI ),以便用户可以查看该网站或 web 应用程序并与之交互。本质上，前端是数字网络产品的一部分，用户可以看到并与之交互。

因此，前端测试是指为测试应用程序 GUI 的可用性和功能性而进行的检查。通常，这包括对最终用户可见的菜单、表单、按钮和其他应用程序元素的验证。

### 为什么前端测试很重要？

当你开发一个应用程序时，最重要的事情是确保开发的应用程序正确工作，并且对于生产部署是[安全的。](/web/20220926185535/https://www.netguru.com/blog/how-to-ensure-your-app-security-and-why-you-should-care)

这可以通过考虑用户可以通过你的应用程序的最无缝的方式来实现，优化导航体验。

虽然您当然希望确保安全的生产部署(即，该应用程序简单地工作)，但是您也希望确保应用程序在用户交互的整个周期中保持稳定。这意味着您还需要保护应用程序中易受攻击或关键部分的边缘情况，包括无限的加载时间或用户无法退出的错误状态。

根据特定的需求，您所执行的检查这些东西的测试可以是手动的，也可以是自动的。您在这里所做的基本上是测试应用程序的客户端(浏览器)部分。

例如，如果您有一个“提交”按钮，您希望确保当它被单击时，它实际上触发了相关的操作，并链接到服务器上发生的数据处理(尽管数据处理当然是后端测试的责任)。

前端测试为你的应用提供强大的保护，防止回归。可能会有这样的情况，您编写的代码可以帮助您部署庞大或复杂的功能，但反过来可能会使您没有意识到的应用程序的其他部分崩溃。

团队甚至个人开发人员在开发过程中忘记一些之前编写的代码，然后在现有代码中添加新代码，这可能会在前端的其他地方造成问题，这种情况并不罕见。

这在有多个开发人员的项目中会更加明显。随着现代应用程序越来越复杂，你很少能够单独交付一个大项目。没有人能够简单地知道其他程序员写的每一段代码的一切。这就是前端测试如此重要的原因——仔细检查代码是否不一致，前端功能是否完整。

您需要在您的代码和最终应用程序中建立信任。否则用户可能永远不会下载你的应用程序或在短时间内删除它。无论何时一个 bug 出现，无论是你的团队还是用户发现的，它都应该被修复——但也应该被一个额外的测试套件覆盖，这样你就知道它不会意外地再次出现。

您越信任您的代码，部署就越容易，压力就越小。此外，企业领导无疑会更高兴地知道，他们的应用程序正在以稳定的速度发展，使公司能够更容易地规划和准备路线图。

保持良好维护的测试的另一个很好的理由是它们可以作为实时文档。编写测试需要对特定测试(以及相关的应用程序组件)的作用进行适当的描述。

为了运行一个合适的测试，您需要使用组件的 API 来添加模拟，这可以作为其他开发人员或您的团队在将来如何使用这些东西的指南。

此外，与自述文件中的手写文档相反，这些准则存在于您的项目中。这意味着，如果一个测试过时了，它可能会导致错误，迫使您更新文档——当手动处理时，这有时可能是一个被遗忘的任务。

编写测试套件还可以(并且可能应该)提高可读性，减少应用程序代码中的耦合。当开发人员想要测试一小部分应用程序，但还需要构建一些不一定与测试相关的依赖组件和模拟时，这可能是他们需要改造部分代码的迹象。这表明代码部分之间的依赖关系过于紧密。

更干净的代码更易测试，而可测试的代码会更干净。这是一个对[前端开发者](/web/20220926185535/https://www.netguru.com/services/front-end-development)和最终你的应用程序的最终用户双赢的场景。

有了这些，我们就能明白为什么前端测试很重要了——但是你实际上需要测试什么呢？让我们来看看。

### 前端测试什么？

前端测试完全面向性能优化和增强用户体验。在 Web 2.0 技术出现之前，大多数 Web 应用程序都是静态的。

这就是为什么大部分处理是在服务器端完成的，这意味着性能优化是通过后端实现的。现在，随着应用程序变得更加动态，优化前端代码的需求越来越大。

测试应用程序的前端时，有几个方面需要关注。它们包括:

*   **跨浏览器和跨平台功能** -检查您的应用在不同浏览器、平台和设备上的特性和响应能力

*   可访问性 -你需要检查每个人都可以访问你的应用程序，包括那些有视觉或听觉障碍的人

*   **端到端检查** -需要通过模拟用户可能采取的真实行动来检查和确认应用程序的端到端工作流(后端到前端)

*   **图像分析测试**——如今大多数网站和应用程序都有大量的图像——从标准显示图像到徽标、信息图和横幅。它们会显著增加应用程序的大小，因此您需要运行测试，看看可以在哪些地方优化图像，以帮助应用程序运行得更快。

*   **层叠样式表(CSS)测试**——CSS 用于帮助构建应用程序的组件并为其设计风格。虽然用户永远看不到样式表代码，但如果它写得不好，他们肯定会看到它的负面影响，所以您需要运行测试来确保两个主要 CSS 元素的性能:语法和显示。虽然语法是开发人员日常工作的一个领域，但在对应用程序的特定部分进行更改后，需要对显示的视图进行回归测试。

## 前端测试的挑战

前端测试至关重要。但是，在处理它时，您需要注意一些常见的挑战并做好准备。

### 确定最关键的前端元素

前端测试通常包括测试许多不同的用户界面(UI)元素。这些包括格式、可见文本、图形和样式/布局(CSS)以及应用程序的所有功能方面，如按钮、提交表单和可点击的链接。

这里的过程包括测试这些特性的响应速度；它们的加载速度有多快，对用户操作的响应时间有多长，它们执行用户请求的速度够快吗？

显然，有这么多要测试，你需要优先考虑最重要的前端功能。要做到这一点，给每个组件分配一个粗略的优先级，首先确保基本的文本和页面容易加载，关键元素放在正确的位置。

接下来，在最后检查格式和图形加载是否正常之前，要确保所有的功能元素都是可见的，并且完全响应动作和请求。

### 模拟真实世界的环境

前端测试最常见的挑战之一是模拟您的应用程序在现实世界中的工作方式。你的测试环境总是受控的，所以很难客观地了解应用程序在受控环境之外的表现。

虽然很难精确匹配用户的真实情况，但是您的测试团队可以通过定制影响页面性能的环境因素来设置与用户的真实情况非常接近的案例。

例如，您可以增加应用程序负载，以反映对系统的并发访问和多个用户请求。或者，您可以限制客户端系统的可用内存、CPU 性能或连接速度。在您的测试用例中建模这些条件，很有可能反映真实的生产环境。

### 选择测试工具

前端测试需要使用不同的测试工具和套件，您需要为任务选择正确的工具和套件。

我们将在下面讨论一些最好的前端测试工具，但是现在这里要考虑的最重要的方面是测试工具提供的特性。市场上有很多软件供应商，很难发现它们之间的差异。最好的前端测试工具包括:

*   容易创建和维护测试脚本，
*   绩效指标洞察，
*   高端报告功能，
*   无缝集成
*   重要的是，自动化工具。

自动化对于有效和快速的前端测试是必不可少的，因为不能期望手动测试人员在每次更新时都运行测试。

### 人性因素

从自动化的重要性出发，在前端测试过程中需要考虑“更软”的挑战。而这些都是人为因素。

这并不一定意味着人们会在测试中犯错误，尽管这是有可能发生的。有时，开发人员可能会因为许多不同的原因而被迫跳过测试。客户可能需要加快发布速度，或者目前没有可用的资源。

有时，通常如果在内部完成，团队可能根本没有意识到需要前端测试。

把它想象成一扇破窗的隐喻。这一理论认为，如果某件事是可见的，但没有得到解决，它很可能会被重复。也就是说，如果很明显测试没有正确运行或者代码没有正确编写，那么这些实践很可能会在将来重复，从而使您的应用程序出现问题。因此，确保始终坚持最佳前端测试实践至关重要。

## 前端测试的最佳实践

前端测试是至关重要的，但是在运行测试时，坚持某些原则以确保最佳实践也很重要，否则您可能无法完全依赖测试结果。以下是前端测试的最佳实践，归类为 F.I.R.S.T .原则。

### F.国税局的原则

为了确保您坚持前端测试的最佳实践，您需要一个框架来遵循。幸运的是，你可以用 F.I.R.S.T .的原则。

自由印度公司的原则代表着:

*   快的
*   孤立/独立
*   可重复的
*   自我验证
*   彻底的

其中大多数是不言自明的。测试应该快速运行(在生命周期的任何必要点)，与未测试的组件隔离，易于在未来重复，能够验证自己是否通过了测试，并覆盖所有必要的变量。

### 从测试金字塔开始

测试金字塔是一个帮助开发团队创建高质量软件的框架。它减少了开发人员识别任何对他们的代码产生负面影响的变更所需的时间，并支持构建可靠的测试套件。

测试金字塔有时被称为'[测试自动化](/web/20220926185535/https://www.netguru.com/services/test-automation)金字塔'。它列出了您应该包括在自动化测试中的测试类型，并概述了这些测试应该遵循的顺序和频率。目的是提供即时反馈，确保代码更改不会破坏现有功能。

这个测试金字塔分为三个级别:

*   单元测试
*   集成测试
*   端到端测试

### 区分前端元素的优先级

正如我们前面提到的，前端测试意味着分析和验证成百上千的 UI 和功能元素。UI 元素包括格式、CSS、文本、图形等，而功能元素包括表单、链接、按钮等。

您需要优先考虑首先测试哪些，以确保有效的测试过程。明智的做法是先测试页面加载速度、基本文本、图像和基本功能(例如，向购物车添加商品、支付工具)，然后再测试图形和弹出窗口。检查这些元素是否可见和响应，然后继续验证图形和布局。

### 使用真正的浏览器和设备

使用真实的浏览器和设备是进行无错误、可靠的前端测试的一个重要方面，它尽可能地反映了真实世界的环境。避免使用仿真器和模拟器，通过使用真正的浏览器和设备来节省时间和资源——这样，您将能够更加依赖您的软件测试结果。

## 前端测试的类型

由于前端有不同的元素要测试，所以有几种不同类型的测试可以考虑运行。其中每一个都集中在前端的不同组件上，共同确保应用程序的前端测试成功。

单元测试

![frontend tests types](img/5bb6ba9034dc428883d8d90dae8f278e.png)

单元测试是前端测试的基本构件。它分析单个组件和功能，以确保它们按预期工作。这对于任何前端应用程序都是至关重要的，根据您期望它们在生产中的表现来测试您的组件和功能，从而为您的客户带来稳定的代码库和可靠的应用程序。您还可以对边缘案例和测试 API 之类的事情使用单元测试。

### 验收测试

执行验收测试是为了确认前端的用户输入、用户流和任何指定动作都已编码并正常运行。开发团队执行它们以确保应用程序的最终模型如最终用户所期望的那样工作。

### 视觉回归测试

视觉回归测试是一种独特的前端测试。其他类型的测试侧重于代码，因此也可以针对后端堆栈运行。反过来，可视化回归测试将应用程序的实际/现有接口与相应的“预期”版本进行比较，以识别任何差距。这是通过比较来自无头的、服务器运行的浏览器的截图来实现的，并且使用机器来进行它们之间的图像比较，识别并突出任何差异。

### 可访问性测试

易访问性测试检查应用程序或网站是否容易被每个潜在用户使用，包括有视觉障碍或其他额外需求的个人。它有时被认为是可用性测试的一个子类，确保特定的、不可改变的条件不会阻止任何人访问应用程序的任何特性或功能，并且他们可以像其他人一样轻松地浏览界面。

### 性能试验

性能测试在特定参数范围内分析应用程序的性能，包括速度、稳定性、可伸缩性、互操作性和响应性。它对前端测试至关重要，因为它有助于确保当用户负载增加时，产品保持其期望的质量，并且它对用户请求和动作快速响应。

### 端到端(E2E)测试

[端到端测试用于检查和确认应用程序的流程从开始到结束](/web/20220926185535/https://www.netguru.com/blog/e2e-testing-vs-integration-testing)都按照预期工作。这主要是通过在真实场景中模拟真实用户的动作来实现的，以确保应用程序接口和 API 之间的通信顺畅。这样做可以洞察耦合在一起的多个系统元素的组合行为。

### 集成测试

大多数现代应用程序都是由大量模块构建而成的。如果这些模块没有正确集成，不能很好地协同工作，就会破坏最终用户体验。您需要运行集成测试，以确保一切都有效地协同工作。

### 跨浏览器测试

执行跨浏览器测试是为了确认应用程序在不同的 web 浏览器中都能正常工作。这个过程包括在不同的浏览器上运行相同的测试用例集，以检查应用程序在每种浏览器上的兼容性。因为这些测试每次都是相同的，所以这个过程可以自动化。

### 通用前端测试工具

正如我们已经提到的，有数百家——如果不是数千家——不同的供应商提供前端测试工具，很难决定选择哪一家。这里有一个列表，列出了满足您需求的一些最好和最常用的前端测试工具。

## 玩笑

Jest 是最流行的 JavaScript 测试框架之一，专注于简单性。通过确保您的测试具有唯一的全局状态，Jest 可以可靠地并行运行测试。为了快速完成任务，Jest 首先运行以前失败的测试，然后根据测试文件花费的时间重新组织运行。它还提供了强大的代码覆盖和简单的模仿工具。

### Selenium WebDriver

Selenium WebDriver 是一个 web 框架，允许开发人员执行跨浏览器测试。它用于自动化基于 web 的应用程序测试，以验证兼容性。该工具允许您选择一种编程语言来创建用于跨浏览器测试的测试脚本。

### 柏树

Cypress 是一个用于 web 测试自动化的端到端测试框架。它使前端开发人员能够用 JavaScript 编写自动化 web 测试，JavaScript 是用于网站开发的最流行的编程语言之一。JavaScript 的使用使得 Cypress 成为对开发者特别有吸引力的工具。就开发人员的体验而言，Cypress 语法非常容易使用——有时就像用英语写句子一样简单！

### 网络驱动

WebdriverIO 是一个渐进式自动化框架，旨在自动化现代 web 和移动应用程序。它简化了与您的应用程序的交互，并提供了一组插件来帮助您创建一个可扩展的、健壮的和稳定的测试套件。

### webdriver js

WebDriverJs 是 Selenium 的官方 Javascript 实现，使用 Selenium 的 Json-wire-protocol 与浏览器进行交互。WebDriverJS 执行的功能基本上与 Selenium WebDriver 相同。

### 测试咖啡馆

测试咖啡馆是一个节点。js 端到端的免费开源自动化工具，可用于测试 web 应用程序。它适用于所有流行的环境，如 Windows、MacOS 和 Linux。借助单个命令中易于安装的特性，您可以用 JavaScript 或 TypeScript 编写脚本。

### 如何创建前端测试计划？

所以你知道测试什么，为什么你需要运行测试，并且知道一些不同的前端测试工具。但是，如何着手实施前端测试计划呢？这些是您应该遵循的关键步骤:

## 定义您的测试预算

在您购买工具或雇佣测试工程师，并决定时间表之前，您需要知道您的测试预算是多少。通常，这将被考虑到你最初的项目预算中，但是当你进入测试阶段时，对照现实来检查期望是有好处的。

### 选择您的工具

根据您的前端中包含的组件和元素，不同的工具可能会为您完成这项工作。根据上面列出的常用工具来检查您的需求，或者如果您不确定，请联系网络专家。

### 设定时间表

你的项目截止日期是什么时候？在应用程序最终发布之前，您需要留出足够的时间进行测试和修改。虽然截止日期可能会很严格，并给你的开发团队一些工作目标，但尽可能灵活也很重要。毕竟你不想发布一个不能正常运行的 app，哪怕是按时发布。

### 定义项目的范围

同样，这可能是你最初的项目计划中的一个因素，但是在这里再回顾一下。在任何应用程序开发中，您都需要决定所需测试的范围。

### 应用程序在发布时是否需要完美，或者是否有可能以工作版本投入生产，并观察用户的反应？有时候，用户的反馈和你从自动化测试中获得的洞察力一样有用。

根据这里的答案，您可以定义项目的范围，这样您就不会使用不必要的资源。

准备好前端测试了吗？

正如我们所看到的，前端测试对于一个企业构建一个新的应用程序或网站来说是一项至关重要的活动。它确保你的潜在客户看到的和与之互动的一切都运行良好，所以这可能是一个成功的产品和一个永远卖不出去的产品之间的区别。

## 这也是一个相当复杂的过程，有许多工具可供选择，有多种不同的类型和测试，还有各种各样的挑战要克服。当然，项目的范围和预算也会影响前端测试，所以在开始之前有很多事情要考虑。

还不确定？立即联系 Netguru 专家，帮助优化您的前端性能测试，并帮助您的开发团队向市场发布成功的应用程序。

It is also quite a complicated process, with lots of tools to choose from, multiple different types and testing and various challenges to overcome. Of course, the scope and budget of your project will impact your frontend testing too, so there’s lots to consider before you get started.

Still unsure? Get in touch with a Netguru expert today to help optimize your frontend performance testing, and empower your development teams to release a successful application to market.