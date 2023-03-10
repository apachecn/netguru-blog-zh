# 托管 Ruby on Rails 应用？–解决方案比较(更新)

> 原文：<http://web.archive.org/web/20230307163032/https://www.netguru.com/blog/hosting-a-ruby-on-rails-app-solutions-comparison>

 在某种程度上，您将不得不决定在哪里托管您的惊人的 RoR 应用程序。

在几十个优秀的主机提供商中进行选择可能并不容易，因为每个提供商在价格、部署/配置灵活性和可扩展性等方面都有自己的权衡。

为了让您的选择更容易，我们比较了五家主要的 RoR 主机提供商——根据您的应用程序要求和预算，您可以正确选择在哪里托管您的应用程序。

## **1。AWS 亚马逊**

[亚马逊网络服务](/web/20220927104505/https://www.netguru.com/blog/3-aws-tricks-for-your-business-lambda-serverless-and-cloud-functions) (AWS)通过亚马逊弹性豆茎(Amazon Elastic Beanstalk)支持 RoR 应用部署的自动化，这是一种管理和自动处理容量供应、负载平衡、应用依赖、扩展和健康监控的服务。

启动您的 RoR 应用程序的关键先决条件是运行一个虚拟 EC2 实例并拥有 S3 磁盘存储。Amazon 允许您选择最实惠的选项(例如，带有一个 CPU 内核和 0.5 GB 内存的 t2.micro)，并在以后扩展您的应用程序。在你[设置好你的云环境](/web/20220927104505/https://www.netguru.com/services/cloud-application-development)后，你可以使用免费的亚马逊弹性豆茎自动配置和部署你的 RoR 应用。另一个好处是，如果您是新用户，您可能有资格使用免费层 AWS 服务一年，包括实例、存储、弹性 IP 等。

### **优点**

-非常稳定且可扩展的平台

-为期一年的免费服务

-对 RubyGems 的出色支持

### **缺点**

-要求对 Linux/Windows 管理和 [DevOps](/web/20220927104505/https://www.netguru.com/services/cloud-application-development) 有很好的了解

当你依赖亚马逊供应商的标准和解决方案，如 S3 和 Lambda 时，你应该谨慎，因为这可能会导致供应商锁定，你可能很难转移到另一个托管服务。

## **2。谷歌云平台**

Google 为在 Google 云平台上部署和运行您的 RoR 应用程序提供了三种选择。

如果你想完全控制底层虚拟机，你可以选择谷歌应用引擎，这是一个用于开发和托管网络应用的谷歌云平台。Google App Engine 可通过免费层访问，并附带预装的 RubyGems、系统库、自定义 Docker 运行时和其他有用的工具，用于 RoR 的快速应用开发(RAD)。使用 Google App Engine，您将需要支付网络流量、存储和搜索查询费用。

第二种选择是使用类似于 Amazon EC2 实例的标准计算引擎部署您的 RoR 应用程序。这与使用 IaaS(基础设施即服务)模型本质上是一样的，在 IaaS 模型中，您需要为计算能力(CPU)和存储付费，并通过标准开发工具手动部署您的 Ruby 环境和应用程序。此选项的自动化功能较少，需要更深入地了解底层 Linux/Windows 系统和工具，以便远程管理您的 RoR 应用程序(例如 SSH)。

最后，谷歌云平台允许设计通过谷歌容器服务部署的 Ruby 微服务。如果您希望开发一个具有松散耦合的[微服务架构](/web/20220927104505/https://www.netguru.com/blog/monolithic-vs-microservices-architecture)的复杂应用程序，这个选项尤其有用。

### **优点**

-灵活的现收现付模式和轻松的可扩展性

-支持多种 RoR 部署选项

-一年免费层服务的提供

### **缺点**

-与亚马逊 AWS 类似，使用谷歌云平台时，供应商锁定可能是一个问题

一旦你离开免费层，谷歌云会变得非常昂贵，尤其是当你的应用程序遇到流量高峰时。

## **3。微软 Azure**

微软 Azure 是微软的云平台，让开发者快速构建、部署和管理用 RoR 构建的网络应用。

要在微软 Azure 上部署 RoR 应用，你应该启动一个 Windows 或 Linux 虚拟机，就像你在谷歌云平台或亚马逊 AWS 上做的一样。Microsoft Azure 支持多种操作系统映像和实例类型，您可以从中找到符合您的应用程序要求的类型。

该平台具有高度的可配置性和灵活性:您可以通过一个易于使用的界面配置端口、DNS 和其他网络功能。一旦你的虚拟机启动并运行，你可以通过 SSH 或任何 FTP 客户端轻松上传你的 RoR 代码，并在你的 Azure 服务器上启动它。

### **优点**

Azure 有一个出色的免费计划，可以在您的虚拟服务器上支持多达 10 个应用程序、1 GB 磁盘空间、FTP、安全扫描和其他功能。

-它提供高可用性(高达 99.9%)和简单的可扩展性，包括支持自动扩展。

-微软让 Azure 用户将 GitHub 与他们的[云托管解决方案](/web/20220927104505/https://www.netguru.com/services/cloud-application-development)集成在一起，这样每次代码改变时你的应用都会更新。 

### **缺点**

你不能使用微软 Azure 作为你的 RoR 应用的平台即服务。这意味着您必须手动配置 RoR 环境，并通过 SSH 或 FTP 上传您的应用程序，这需要 Linux/Window 系统管理方面的专业知识。

RoR 部署可能太慢，而且没有办法从 Mac 上将你的 RoR 应用程序部署到 Azure 云服务。

## **4。Heroku**

作为一个“全服务”PaaS(平台即服务)解决方案，Heroku 是不希望或不需要管理自己的基础设施(如虚拟机、服务器、硬盘等)的团队的绝佳选择。).

与亚马逊 AWS 或谷歌云平台不同，Heroku 提供所有计算服务(vCPUs、硬盘等。)打包，称为“dynos”。这意味着您不必单独启动硬盘和虚拟实例——默认情况下，您的 RoR 应用程序所需的一切都已提供。

此外，Heroku 拥有灵活的定价选项。如果您希望您的应用程序全天候运行，您可以选择每月 7 美元的“业余爱好”帐户。

如果您的应用程序很忙，您可能希望帐户有更多的“dyno ”,每月从 25 美元到 500 美元不等。该帐户启动后，您可以从 Git 上传您的 RoR 应用程序，并在 30 秒内完成部署。

由于 Heroku 是专门为部署 Rails 应用程序而构建的，所以该平台为 Rails 开发而优化的程度并不令人惊讶。

### **优点**

Heroku 针对 RoR 应用的快速高效部署进行了优化。由于 Heroku 是一个 PaaS 系统，您不必处理底层基础设施和系统配置，启动您的 RoR 应用程序所需的一切都是现成的。

Heroku 没有带宽限制。因此，如果流量增加，你可以快速扩展你的应用程序，因为你知道 Heroku 不会关闭你的服务器并过度收费。

-该平台易于使用，因为它提供了直观简单的用户界面，基于开发人员友好的命令行界面。 

### **缺点**

使用 Heroku，你不能完全访问底层基础设施(这是一个 PaaS)。对于寻求配置虚拟服务器环境、操作系统、防火墙、负载平衡、网络和其他深层系统架构的公司来说，这可能是一个问题。

一旦你决定处理更多的流量，服务费往往会大幅上涨。

## **5。数字海洋**

DigitalOcean 是一家虚拟专用服务器(VPS)提供商，设计为液滴，在单个捆绑包中提供适量的 RAM、CPU 和本地存储资源。

这意味着您不需要单独启动不同的服务(硬盘、实例)。最基本的 Droplet 每月花费 5 美元，将包括 512MB RAM、1 个 vCPU、1TB 流量和 20 Gb SSD。与亚马逊 AWS 或谷歌云平台不同，DigitalOcean 不为其托管的 RoR 解决方案提供自由层选项。此外，以前您可以选择将您的 RoR 环境部署为一键式安装。此功能最近已被删除。

现在，要在 Droplet 上安装你的 RoR，你可以使用命令行工具，比如 Ubuntu 上的 rbenv 或 RVM (Ruby 版本管理器)。

### **优点**

-数字海洋比 IaaS 平台(如亚马逊 AWS)更容易管理。所有必要的服务(例如存储、计算)都以固定价格打包提供。

从 Digital Ocean 迁移您的 RoR 应用程序更容易，因为他们的模型不会将客户锁定在他们的云服务上。

你可以根据自己的需求调整数字海洋环境，这比其他托管服务提供商提供的方式要广泛得多。

### **缺点**

-不支持自由层。

该平台规定了每月带宽限制，因此如果你的应用程序遇到零星的流量高峰，你必须将你的系统升级到新的计划。

## **6。其他选择**

除了上面提到的大型虚拟主机公司，还有大量的小型虚拟主机提供商，如 OVH、Aruba cloud 和 Oktawave。

借助 OVH，您可以根据应用的工作负载，在 VPS(虚拟专用服务器)或专用服务器上启动您的 RoR 应用。此外，您可以管理自己的私有云、公共云或混合云，并访问底层系统配置和设置。OVH 保证了出色的 SLA 和性能，因为它是少数几家不将其数据中心管理外包给第三方的公司之一。

如果您想要一个便宜的云 VPS 解决方案用于您的 RoR 应用，Aruba Cloud 提供每月 1 美元的计划，其中包括 SSD 磁盘、一个 IP 地址和每月高达 25 TB 的数据传输。这是托管轻量级 RoR 应用程序的绝佳选择，不过，这些应用程序可以通过 Aruba 的 Cloud Pro 和私有云计划轻松扩展。

最后，波兰云提供商 Oktawave 提供了一种自动扩展 RoR 应用的绝佳方式。一旦您的 RoR 应用程序启动并运行，Oktawave Autoscaler 将跟踪流量动态并自动更改您的实例的类别。结合负载平衡，Oktawave 将确保您的 RoR 应用程序在任何规模下都能稳定运行。

了解更多[2019 年使用 Ruby on Rails 排名前 34 位的公司](/web/20220927104505/https://www.netguru.com/blog/what-is-ruby-on-rails-used-for)。

## **如何为 RoR App 选择合适的主机？**

那么，底线是什么？如果你想对你的 RoR 部署进行精细控制，你应该选择 IaaS 提供商，如谷歌云平台、亚马逊 AWS 或微软 Azure，它们都是稳定和可扩展的解决方案。

然而，代价是使用这些托管提供商将需要雇佣一名 DevOps 专家来管理环境、容器化和部署，以及一个专业的 Linux 或 Windows 管理员团队来配置实例、存储、网络等。

如果您希望您的 RoR 尽快启动并运行，那么 Heroku 等 PaaS 解决方案是更好的选择。Heroku 具有可伸缩性且价格低廉，通过从 Git 存储库中上传 RoR 应用程序，可以很容易地启动它们。代价是，有了 Heroku 这样的提供商，你对底层基础设施的控制就更少了。

最后，如果您希望对虚拟服务器保持更高水平的控制，但不想单独管理不同的云服务，Digital Ocean 是最佳选择。Digital Ocean 为您解决了这一问题，它将所有这些产品打包，称为液滴。

这里有 3 个快速入门的小技巧:

> -检查所有可用的配置选项–您可以从现成的 Droplet 中选择，也可以根据自己的需求创建自己的 Droplet。
> -创建水滴的快照——这是保存和复制水滴内容的最简单方法。
> ——精心选择最适合自己的方案——digital ocean 为水滴提供了四种不同的方案，一种共享 CPU 方案和三种专用 CPU 方案。

![DropletInfo](img/88d9f33f4cef37fa1d438f4683ef1e40.png)