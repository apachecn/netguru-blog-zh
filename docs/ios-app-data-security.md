# iOS 应用安全–如何保护移动应用中用户的敏感数据

> 原文：<http://web.archive.org/web/20230307163032/https://www.netguru.com/blog/ios-app-data-security>

 由于其封闭的系统和苹果公司施加的限制，iOS 被认为是最安全的移动操作系统之一。然而，这并不意味着在开发一个 iOS 应用程序时可以忽略安全性。有不同的方法可用于保护移动应用中的用户数据，如安全审计、SSL 锁定或用户数据保护工具。

目前，安全性是 IT 界最热门的话题之一。用户、公司和立法者越来越重视数据安全和隐私。这种趋势也适用于移动应用程序，因为它们离用户很近。使用频率和便利性意味着移动应用通常存储重要的私人数据，并且[企业需要优先考虑应用安全性](/web/20220925023046/https://www.netguru.com/services/cybersecurity)。

在本文中，我们将向您介绍几种解决方案，帮助您提高 iOS 应用程序的安全性。

## **潜在风险**

应用安全是一个非常广泛的主题，很难在一篇文章中介绍，但我们可以轻松识别基本威胁:

### 用户数据泄露

通过使用 iOS 应用程序，用户通常会输入他们的私人数据。如果设备落入未经授权的人手中，以不安全的方式存储数据会造成数据泄露的风险。

### 中间人攻击

对于 iOS 应用程序来说，拦截 http(s)请求和响应相对容易。可惜， TLS 不足以让你的 app 安全。使用像 [Charles Proxy](http://web.archive.org/web/20220925023046/https://www.charlesproxy.com/) 这样的工具，即使是一个业余爱好者也可以了解我们的应用程序请求，相应的服务器响应，并通过发送篡改的请求来操纵网络流量。除此之外，数据可以直接从应用程序的网络流量中截取。当用户的 iOS 设备连接到公共 Wi-Fi 网络时，这种情况最常见。

### 逆向工程

由于逆向工程，攻击者可以获得你在应用程序中使用的 URL 地址、标识符、密钥，了解业务逻辑，或者窃取你的知识产权 -尤其是如果你使用复杂的算法。此外，他还可以修改应用程序的行为，例如，省略登录屏幕。

## **如何确保你的应用安全**

如今，大多数企业开发应用程序来提供更好的服务，并与客户进行更好的沟通。将 iOS 中的安全性作为重中之重至关重要。以下是开发 iOS 应用程序时需要考虑的几种解决方案:

### **用户数据保护工具**

为了加强数据保护，重点关注两个方面- **使用正确的数据存储解决方案，以及保护输入的数据。**登录名、密钥和密码应存储在 [钥匙链](http://web.archive.org/web/20220925023046/https://developer.apple.com/library/content/documentation/Security/Conceptual/keychainServConcepts/iPhoneTasks/iPhoneTasks.html#//apple_ref/doc/uid/TP30000897-CH208-SW1) 中。

**Keychain 是苹果公司开发的密码管理系统，**同时在 macOS 和 iOS 上分发。iOS 版本更简单，在 iOS 上无法在不同发行商的应用之间共享钥匙串项目。这意味着 iOS 钥匙串项目只能由创建它们的应用程序或同一开发者的其他应用程序访问。

然而，您可以使用其他工具来存储其他不太重要的用户数据。值得一提的是两个解决方案——[核心数据](http://web.archive.org/web/20220925023046/https://developer.apple.com/documentation/coredata) 和 [境界数据库](http://web.archive.org/web/20220925023046/https://realm.io/products/realm-database/) 。

核心数据是苹果的持久性框架，带有底层的 [SQLite](http://web.archive.org/web/20220925023046/https://www.sqlite.org/index.html) 数据库。这意味着**开发人员与核心数据方法交互，**不是直接与数据库交互，并且与幕后发生的事情绝缘。重要的是，默认情况下，app 解锁时 **SQLite 是不加密的。**苹果有一个名为“ [数据保护](http://web.archive.org/web/20220925023046/https://developer.apple.com/documentation/uikit/core_app/protecting_the_user_s_privacy/encrypting_your_app_s_files) ”的功能，如果设备被密码锁定，该功能会对沙箱进行加密。

但是我们不能总是依赖终端用户的密码来保护他/她的设备。**设备可以被** **越狱** **，**密码很容易被破解，或者被不知情的用户记在手机保护壳上。不是每个人都懂技术。**如果通过密码加密还不够，我们需要使用第三方解决方案**，如 [加密核心数据 SQLite 存储](http://web.archive.org/web/20220925023046/https://github.com/project-imas/encrypted-core-data) ，它允许我们甚至在设备解锁时加密 SQLite。

**另一个解决方案是 Realm 数据库，**SQLite 和核心数据的开源替代方案。它允许您使用强大的 [AES-256 加密](http://web.archive.org/web/20220925023046/https://en.wikipedia.org/wiki/Advanced_Encryption_Standard) 非常容易地加密数据。**即使设备解锁，数据也会被加密，**您的加密密钥可以安全地存储在系统钥匙串中。这意味着只有你的应用程序可以解密这些数据。在安全性方面，Realm 似乎是一个非常好的解决方案。

### 保护用户输入中的数据

我们需要注意的是，iOS 中使用的键盘会导致数据被缓存以便自动更正。对于用于敏感用户数据输入的字段，应关闭自动校正。截图也存在类似的情况。一个 app 去后台，系统截图。如果用户输入敏感数据，并且它在屏幕上可见，我们需要在应用程序进入后台之前实现一个屏蔽屏幕的机制。

### **防止逆向工程**

在逆向工程的情况下，实现安全措施更加复杂。我们不能让攻击者无法完成任务，但我们可以让它变得更加困难。

一个例子是使用安全的方式**为特定环境**存储应用程序密钥——你可以为此使用 [协同密钥](http://web.archive.org/web/20220925023046/https://github.com/orta/cocoapods-keys) 。

另一种加强 iOS 应用安全系统的技术是**代码混淆。这包括使用误导性的文件名和方法名，创建陷阱和假方法，将关键代码隐藏在极其复杂的循环中等等。这些操作可以在连续交付过程中自动执行，但是请记住，高级工具是有价格的。**

### **确保 SSL 锁定**

为了防止操纵网络流量操纵和中间人攻击，应该实现证书锁定。这是一种用于**确保应用程序只与正确的服务器通信的方法。**TLS 证书存储在应用捆绑包中，用于在网络握手期间验证服务器的真实性。

### 通过双因素身份认证增加额外的安全层

iOS 设备中的用户鉴定允许用户识别试图连接到网络资源的人。有许多工具会有所帮助。双因素认证，也称为 2FA，给了一个额外的安全层，允许更好的数据保护。那么它是如何工作的呢？用户在向身份验证工具提交两份证据后，被授予访问应用程序的权限。例如，它可以使用可以通过 SMS 或电子邮件发送的密码和一次性通行码。

### **安全审计**

最后但并非最不重要的一点是，在发布应用程序之前做一次安全审计绝对是值得的。这并不总是意味着花大价钱雇佣外部黑客团队。有时候通过 [OWASP 移动应用安全验证标准](http://web.archive.org/web/20220925023046/https://github.com/OWASP/owasp-masvs) 就够了。

MASVS 是一份针对移动应用的安全清单，由一家致力于提高软件安全性的领先非营利组织**发布。**虽然该文档不是 iOS 专用的，但在发布应用程序之前绝对值得一读。

## **开发安全的 iOS 应用**

iOS 相比其他手机操作系统相对安全。**苹果提供了强大的安全机制，如钥匙链、密码数据加密或应用传输安全，**这迫使开发者使用 TLS。然而，这并不意味着这些解决方案在每种情况下都是足够的。让一个应用程序变得安全并不是火箭科学——关键在于[使用合适的解决方案](/web/20220925023046/https://www.netguru.com/services/native-mobile-app-development)并在发布前花点时间。