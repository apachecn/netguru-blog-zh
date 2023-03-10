# 网络认证终极指南

> 原文：<http://web.archive.org/web/20230307163032/https://www.netguru.com/blog/web-authentication-guide>

 大多数 web 应用程序需要某种形式的身份验证来验证用户的身份。最佳的 web 身份验证方法取决于应用程序的安全要求。哪些是最好的？

## 什么是身份验证，它与授权有何不同？

当我们谈论身份验证时，我们指的是验证某人是他们所说的那个人的过程。反过来，授权是验证该人有权做某事的过程。

身份验证(AuthN)是验证用户身份的过程。您可以通过多种方式做到这一点，但最常用的方法是基于用户名和密码的身份验证、双因素身份验证或生物特征身份验证。

用户还可以用证书或硬件令牌来验证自己。当身份验证过程失败时，服务会以 HTTP 响应代码“401 未授权”进行响应。

授权(AuthZ)是验证用户权限的过程。在标准设置中，失败的授权会收到 HTTP 响应代码“403 禁止”。

## 不同类型的认证机制

针对服务对用户进行身份验证的第一步是要求用户提供他们的凭据。请求的凭证可以采取多种形式。我们认为用户名和密码是最流行的凭证类型，但是用户也可以提供硬件令牌或证书。

如今，我们越来越多地使用生物特征和一次性密码。以下是用户向应用程序提交凭据的几种方式:

### HTTP 基本身份验证(RFC 1945)

这是最简单的认证形式。它使用标准头发送用户名和密码，然后使用 Base64 编码。

这种方法的优点是容易实现；缺点是凭证是以纯文本形式发送的，因此它不适合具有高安全性要求的应用程序。

### 摘要式身份验证(RFC2617)

这种类型的身份验证提供了比基本身份验证更安全的访问控制。它们不是以纯文本形式发送凭证，而是使用单向哈希算法进行编码。

即使凭据被截获，也无法解码。然而，并不是所有的用户代理都支持摘要认证，所以它并不适合所有的应用程序。

### 基于表单的身份验证

这是最常见的 web 身份验证形式。它使用 HTML 表单[收集用户名和密码](http://web.archive.org/web/20230112223239/https://www.netguru.com/blog/authentication-with-login-and-password)，然后提交给服务器。这种方法的优点是实现简单，并且受所有浏览器的支持。

然而，缺点是凭证是以纯文本形式发送的，因此它不适合具有高安全性要求的应用程序。

### 证书验证

这种方法比上述方法更安全。根据需要，可以实现相互身份验证或客户端证书身份验证，并且通信通过安全的 HTTPS 访问通道进行。

### WebAuthn

[WebAuthn](http://web.archive.org/web/20230112223239/https://webauthn.guide/#authentication) 是一种现代的无密码开放标准，它使用非对称公钥加密而不是基于密码的认证。这种强身份验证方法包含一个私钥和一个公钥，被视为一种多因素身份验证。

所有主流浏览器、用户代理和操作系统都支持无密码身份验证。事实上，许多人认为我们正走向一个没有密码的未来。

一旦用户通过所配置的任何方式提供了他们的凭据，服务就会继续进行身份验证流程中的后续步骤。有两种主要类型的身份验证流:有状态和无状态。

接下来的章节将深入这些过程的技术细节，突出它们的区别、用例以及各自的优缺点。

### 状态认证

有状态身份验证是一种更传统的方法，它依赖于在服务器上存储有关用户登录状态的信息。这意味着对于每个请求，服务器都会验证用户是否仍处于登录状态，以及是否有权访问所请求的资源。例如，有状态认证使用会话 cookie。

一旦服务器收到用户的凭据，它将创建一个会话，并通过三种主要方式将数据存储在已配置的存储中:

1.  服务器内存
2.  缓存(例如，Redis 或 Memcached)
3.  数据库(例如，MongoDB 或 Postgres)

然后，服务器将 sessionID 发送回用户。通常，它以 cookie 值的形式发送，也称为不透明引用。这意味着除了服务器之外，用户的信息不能被任何人提取。SessionID 是一个随机字符串，只有服务器可以将其映射回用户的数据。

不仅如此，包含 sessionID 的 cookie 也受到保护，用服务器存储的秘密进行签名。此外，会话 cookie 受到适当标志的保护。有关 cookie 安全性的更多信息，请参见 [RFC6265](http://web.archive.org/web/20230112223239/https://www.rfc-editor.org/rfc/rfc6265) (第 8 章)。

状态认证最常用于 SSR(服务器端呈现)web 应用程序、Spring 之类的框架和脚本语言。

### 无状态认证

另一方面，无状态身份验证不依赖于服务器来跟踪用户的登录状态。相反，它使用一个令牌，该令牌随每个凭证请求一起传递。这个令牌包含服务器验证用户身份所需的所有信息。

最常见的无状态身份验证方法是 OAuth 和 OpenID。

*   OAuth 是一种流行的身份验证协议，允许用户通过第三方服务(如脸书或谷歌)进行身份验证。这种方法非常安全，因为凭据从不发送到服务器。然而，实现起来可能很复杂。
*   OpenID 是一种认证协议，允许用户通过第三方服务(如脸书或谷歌)进行认证。它很容易实现，但不如 OAuth 安全，因为凭证被发送到服务器。

使用这种类型的身份验证，所有关于用户会话的信息都存储在令牌中，而不是跟踪 sessionID 并将会话信息存储在应用服务器上。令牌保存在客户端，并随每个用户请求一起发送。标准是令牌作为 HTTP 授权头中的一个值发送。

与有状态身份验证相比，该流程的不同之处在于，一旦服务器收到用户的凭证，它就会生成一个令牌并将其发送回用户。服务器不负责以任何方式记住令牌——这是客户端的职责。

令牌是自包含的，这意味着它包含验证用户的所有必要信息。这有减少数据库查找次数的优点，但主要缺点是容易受到 XSS 攻击。

无状态身份验证最常用于 SPAs(单页应用程序)、web APIs 和移动应用程序。

JWT (JSON Web Token)是通过令牌进行身份验证的最常用实现。JWT 是一个开放标准，它提供了一个紧凑的、独立的、URL 安全的令牌，可以用对称或非对称密钥进行签名。

它很容易实现，并且有多种方法来确保应用程序的安全性。更多详情请参考 [RFC7519](http://web.archive.org/web/20230112223239/https://www.rfc-editor.org/rfc/rfc7519) 。

## 不同身份验证方法的优点和缺点

有状态身份验证的好处是它通常更安全，实现起来也不复杂。通过正确配置 cookie 标志(即 HTTPOnly、SameSite)来加强安全性。

弊端？它可能会很慢，并且不能很好地扩展，因为服务器必须保存每个用户会话的数据。此外，还有对 CSRF(跨站点请求伪造)攻击的担忧，应用程序必须针对这种攻击媒介进行保护。

同时，无状态身份验证的好处是它通常更快，更具可伸缩性。缺点是什么？它不太安全(容易受到 XSS 攻击)，而且实现起来更复杂。

您必须记住，即使会话数据没有存储在服务器上，它仍然必须维护一个被无效或撤销的令牌的数据库。

无论选择哪种认证机制，[确保您的 web 应用程序受到良好保护](http://web.archive.org/web/20230112223239/https://www.netguru.com/services/cybersecurity)免受跨站点脚本攻击。这些漏洞会通过从本地存储中泄漏用户凭据或拦截带有 AJAX 请求的会话来危害用户凭据。

因此，必须正确实现 HTTP 安全头和 TLS 加密。

您选择的身份验证方法取决于您的特定需求。但是希望这个概述能让您更好地理解身份验证是如何工作的，以及您可以使用的选项。