# Kubernetes 部署 101 -内容、方式和原因

> 原文：<http://web.archive.org/web/20230307163032/https://www.netguru.com/blog/kubernetes-deployment>

 Kubernetes 是一个领先的容器化编排平台，改变了软件开发的方式。开源解决方案使容器变得更加容易访问和流行。

作为一名软件开发人员、架构师或 DevOps 工程师，想想有多少领域

当软件被创建时，在发布给最终用户之前和之后，都需要被覆盖。[可用性、可扩展性、可靠性、安全性](http://web.archive.org/web/20230310132506/https://www.netguru.com/blog/building-scalable-cloud-infrastructure)-这是一个永无止境的列表。但是如果这些事情中的一些可以自动化或者至少更容易实现呢？

Kubernetes 是一个开源的容器化编排平台，提供了许多特性和功能，有助于使用内置和附加组件覆盖这些领域。在本文中，我们将探索 Kubernetes 的核心组件，尤其是一个叫做 Deployment 的组件。

## 基本 Kubernetes 组件

在深入了解 Kubernetes 部署是什么以及它是如何工作的之前，有必要了解 Kubernetes 的基本概念:pod 和控制器。因此，让我们利用这一术语表章节来更好地理解大背景。

### 什么是古巴三明治？

一个 Pod 是 Kubernetes 中最小的工作量单位。通常[会误解 Pod 和 Container 是同一个东西](/web/20230310132506/https://www.netguru.com/blog/kubernetes-vs-docker)，因为它们之间有相似之处。例如，Pod 规范确定它使用 Linux 名称空间、组和其他类型的隔离——与容器隔离使用的一样。

Pod 定义为一组包含一个或多个共享存储和网络资源的容器，以及如何运行它们的规范。这样，荚是一个或多个容器上的附加层或包装。

要使用 Kubernetes Pods 运行您的容器化应用程序，在将图像发布到注册中心后，创建一个 YAML 清单。在那里，用强制或可选的 Kubernetes 部署元数据、标签等指定哪个容器必须在 Pod 内部运行。

通常，您不需要直接创建 pod，甚至不需要创建 singleton Pods。相反，您可以利用内置的 Kubernetes 控制器，并使用工作负载资源(如[部署](http://web.archive.org/web/20230310132506/https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)、作业或有状态应用程序的有状态集)来创建 Pods。

### 什么是 Kubernetes 控制器？

如上所述，pod 通常不是手动创建的。Kubernetes 使用称为控制器的组件为您创建和管理 Pod 的生命周期。

解释 Kubernetes 控制器的最佳方式是使用 Kubernetes 官方文档中提供的常见示例。想象一下，你有一个恒温器，你觉得冷，所以你把室温调得更高。

那一瞬间房间的温度是实际状态，你在恒温器上设置的温度是想要的状态。

该机制工作，使实际温度尽可能接近理想温度。在一个有全功能恒温器的房间里，一段时间后，实际温度与期望温度相同。

Kubernetes 控制器的行为与此类似:您在 YAML 清单中指定所需的状态，Kubernetes 就会施展魔法达到所需的状态。控制器在一个循环中运行，该循环检查 Kubernetes 集群的当前状态，并做出更改以使实际状态与期望状态同步。

控制器跟踪至少一种 Kubernetes 资源类型。现在，想象一下，在您想要的状态下，您希望有三个 pod 运行特定的应用程序。

在 Kubernetes 集群中只有一个 Pod 运行该应用程序的情况下，控制器将改变环境，以便添加两个额外的 Pod。

一段时间后，将有三个吊舱运行。如果 Pod 内的应用程序出现故障，控制器将循环运行，检查所需状态是否与实际状态不同，并尝试添加另一个 Pod 来代替出现故障的 Pod。

#### Kubernetes 控制器有哪些不同类型？

更令人困惑的是，根据您的需要，您可以为您的应用程序使用多种类型的控制器。有不同类型的控制器可以让您在 Kubernetes 集群上配置行为，下面列出了简短的说明:

*   **复制集**–用于保证指定数量的相同 pod 的可用性。换句话说，ReplicaSet 确保指定数量的 Pod 副本在任何给定时间运行。
*   **Deployment**——管理复制集并提供 Pods 声明性更新的高级概念，以及其他有用的特性，我们将在本文后面深入讨论。
*   **DaemonSet**–用于确保 Pods 在 Kubernetes 集群中指定数量的节点上运行(每个节点或节点子集一个节点)。DaemonSet 的一个典型用例是在每个节点上运行日志收集器或节点监控守护程序。
*   **stateful set**–用于管理一组 pod 的部署和扩展，提供关于 pod 的排序和唯一性的保证。与部署不同，StatefulSet 为每个 Pod 维护一个粘性标识。这些 Pods 是根据相同的规范创建的，但是不可互换:每个 Pods 都有一个在重新调度时维护的持久标识符。
*   **作业**–用于创建执行任务直到完成的 pod。作业也可用于运行批处理任务或临时操作。作业与其他 Kubernetes 控制器的不同之处在于，它们运行任务直到完成，而不是像部署和状态集那样管理所需的状态。

因此，除了内置控制器之外，Kubernetes 被设计为通过编写客户端程序来实现自动化，因此可以编写我们自己的控制器或使用自定义控制器。

## 深入了解 Kubernetes 部署

现在我们知道了基础知识，并有了大致的概念，我们可以深入到 Kubernetes 主要控制器之一的细节:部署。

### 什么是 Kubernetes 部署控制器？

部署处理一组没有唯一标识的 pod。它用于无状态应用程序，即不存储任何数据或状态的前端应用程序。部署是一个更高层次的概念，它管理副本集并向 pod 提供声明性更新。那么，为什么在 ReplicaSets 上还需要另一个控制器，它已经是一个控制器了？

基本上，关键的区别在于 Kubernetes 部署控制器比 ReplicaSet 提供了更多的配置选项。通过使用 Kubernetes 部署，您可以更好地控制副本集的生命周期，从而更好地控制底层 pod 的生命周期。

Kubernetes 部署控制器还为您提供了扩展、更新和回滚到先前版本的选项。

### 如何使用 Kubernetes 部署

在深入讨论细节之前，让我们看一下部署清单以及如何创建它。部署清单是一个 YAML 文件，包含有关部署本身和 Pod 模板的信息，以及如何运行 Pod 的说明。

我们可以使用一个示例来指定您应该有多少个副本，应该运行哪个版本的容器映像，应该在容器上附加什么标签和注释等等。下面是一个非常简单的部署 YAML 清单的例子:

```
 apiVersion: apps/v1
kind: Deployment
metadata:
  name: busybox-deployment
  labels:
    app: busybox
spec:
  replicas: 10
  strategy: 
    type: RollingUpdate
  selector:
    matchLabels:
      app: busybox
  template:
    metadata:
      labels:
        app: busybox
    spec:
      containers:
      - name: busybox
        image: busybox
        imagePullPolicy: IfNotPresent
        command: ['sh', '-c', 'echo Container 1 is Running ; sleep 3600'] 
```

要在 YAML 之外创建部署，您需要运行下面的命令:
`kubectl create -f myDeployment.yaml`

值得一提的是，在 Pod 出现故障的情况下，部署会检查所需状态是否与实际状态不同，并尝试添加一个新的 Pod 来替换出现故障的 Pod。当新的 Pod 运行时，故障 Pod 将被终止。

### 有哪些不同的部署策略？

使用部署的一个好处是，您可以选择更新策略，甚至在不停机的情况下执行部署部署状态更新。Kubernetes 基于配置，为你处理整个更新过程，这太棒了。

在部署中进行更改后，即通过运行 below 命令并更新 YAML 清单中的标签或图像版本，默认行为是 Kubernetes 触发部署展示状态更新。

请注意，只有一定数量的 pod 在更新时关闭，并且只有一定数量的 pod 被创建为超过所需的 pod 数量(默认情况下，最大 25%不可用，最大 25%激增)。

`kubectl edit deployment/foo-deployment`

但是，如果您的新镜像版本不稳定，并且您的 pod 处于无限崩溃循环中，该怎么办呢？不要担心，Kubernetes 保留了一个首次展示的历史，所以如果出现问题，您可以回滚到以前的版本。如果您想同时应用许多更改，甚至可以暂停和恢复卷展栏。

如上所述，默认的更新策略是 rollout，但是还有其他策略。以下是部署更新策略的非详尽列表:

*   **首次展示部署**–默认策略，其中 pod 以滚动更新部署方式更新。在旧 Pod 终止之前，新 Pod 需要完全运行。此外，还配置了最大不可用和最大浪涌来控制更新过程。
*   **重新创建部署**–在创建新的 pod 之前，所有现有的 pod 都被终止。
*   **金丝雀部署**–由 Kubernetes 文档涵盖，可以创建带有特定标签(即稳定和金丝雀)的单独部署。然后，使用大量副本，您可以在稳定/旧部署和金丝雀/新部署之间实现流量负载平衡。
*   **蓝/绿部署**–部署一个新的应用程序版本，作为一个名为“绿”的单独部署，在同一 Kubernetes 集群中仍然保留“蓝”部署，以防新应用程序出现问题。成功部署后，将流量重新路由到“绿色”。

选择正确的部署策略对于维护应用程序的可用性和可靠性至关重要。

### 确保可扩展性

假设您有一个 Pod 在运行，并且您知道流量很快会增加，因此一个 Pod 不足以让您的应用程序保持可用性和可靠性。

通过使用部署，您可以通过使用 Kubernetes CLI 或编辑 YAML 清单，简单地将副本的数量扩展到所需的值。下面是如何使用 CLI 扩展 Kubernetes 部署的示例:

`kubectl scale deployment/foo-deployment --replicas=5`

您可以通过在等式中再添加一个组件来利用部署:水平 Pod 自动缩放器(HPA)。在现代社会，没有时间和人力来手动扩展一切。通过在部署中使用 HPA，基于特定的指标，您可以让 [Kubernetes 为您扩展您的应用](http://web.archive.org/web/20230310132506/https://www.netguru.com/blog/kubernetes-autoscaling)。

当流量增加时，Kubernetes 会自动在部署清单中添加副本数量，即通过检查 CPU 利用率是否高于配置值，然后在流量恢复正常时删除副本数量。以下是如何使用 CLI 自动扩展 Kubernetes 部署的示例:

`kubectl autoscale deployment/foo-deployment --min=1 --max=10 --cpu-percent=80`

## 部署与状态设置

最大的问题之一是何时使用 Deployment 和 Statefulset，因为这两个是最相似的 Kubernetes 控制器。最大的区别是部署用于无状态应用；部署创建没有唯一身份的 pod，并且 pod 是可互换的。

另一方面，Statefulset 用于有状态的应用程序(即数据库)；它按顺序创建 pod，并且 pod 具有唯一的身份，因此它们不可互换——它们在重新启动后保持其身份。

## Kubernetes 部署:内幕

在将容器化的应用程序部署到 Kubernetes 环境中时，最好了解核心概念以及关键组件的优缺点，以便在部署您的[云应用程序](http://web.archive.org/web/20230310132506/https://www.netguru.com/services/cloud-application-development)时，它是可用的、可伸缩的、可靠的和安全的。

在本文中，我概述了不同类型的内置 Kubernetes 控制器，深入探讨了 Kubernetes 部署及其工作原理。

希望在读完这篇文章后，你能理解有许多不同的控制器，每个都有自己的角色。在某些情况下，使用作业是好的，在其他情况下，部署就足够了。

当您想在所有节点上运行您的应用程序时，DaemonSet 会完成这项工作。当您需要为您的 pod 贴上一个唯一的标识时，请使用 StatefulSets 当用于部署的 pod 可互换时。

最后，您可以利用部署作为控制器，为您的应用程序设置合适的部署策略。此外，通过将其与 [CI/CD 管道](http://web.archive.org/web/20230310132506/https://www.netguru.com/blog/ci-cd-pipeline)混合，您可以创建一个强大的解决方案，在该解决方案中，您可以在零宕机的情况下更新您的应用——例如，使用 Canary 部署策略。