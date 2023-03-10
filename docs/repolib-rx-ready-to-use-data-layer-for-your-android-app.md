# RepoLib Rx -适用于您的 Android 应用程序的现成数据层

> 原文：<http://web.archive.org/web/20230307163032/https://www.netguru.com/blog/repolib-rx-ready-to-use-data-layer-for-your-android-app>

 人们认为移动应用程序的开发漫长而乏味的原因之一是缺乏针对移动应用程序的[特定架构，尤其是 Android。由于谷歌的不同做法，这种情况已经改善了一段时间，谷歌开始为 Android 应用程序建议某种架构。谷歌现在建议使用 MVVM 架构。然而，问题依然存在。](/web/20221004140759/https://www.netguru.com/blog/mobile-application-architecture-why-is-it-so-important)

移动应用程序仍然有非常不明确的架构，或者根本没有。此外，很少有框架或库能够为特定的解决方案提供特定的架构，这一事实加剧了问题的严重性。这使得每个模式的实现更加耗时——您需要编写大量样板代码来构建模式/架构结构。这使得开发变得不必要的漫长。

移动应用程序中的一个问题领域是负责在本地或远程存储中检索和存储数据的数据层。大量关于数据同步的重复操作和特定架构的缺乏将显著延长开发时间，并使代码更容易出错。为了解决这些问题，我们决定开发一个统一的解决方案，其形式是一个现成的库，用于处理来自不同来源的数据同步- [**RepoLib Rx**](http://web.archive.org/web/20221004140759/https://github.com/netguru/repolib-android) 。

## 库概述

RepoLib Rx 是一个 Kotlin 库，它根据选定的同步策略在两个不同的数据源之间提供数据同步逻辑。该库是用 Repository 模式设计的，该模式用于描述数据层结构。下面是存储库模式的一个简化方案。

![repository_pattern](img/ec253fec6f039023f374fe62f8057b87.png)

RepoLib Rx 旨在允许应用程序执行基本的数据操作，如创建、读取/获取、更新、删除(CRUD)。这个库负责管理从业务层组件发送到适当数据源的数据请求。基于由用户实现的策略工厂提供的请求同步策略来选择适当的数据源。下面显示的方案说明了库的架构，包括前面提到的策略。

![PatternLib - diagrams](img/f019eade284f408e2da823718efc10a6.png)

该库使用 Rx 框架来管理数据流。使用 [RxJava](http://web.archive.org/web/20221004140759/https://github.com/ReactiveX/RxJava) / [RxKotlin](http://web.archive.org/web/20221004140759/https://github.com/ReactiveX/RxKotlin) 来利用 Rx 模式。它的主要任务是构造负责向数据源发送请求并从中获取数据的反应性数据流。

该库是通用的——这意味着它不强制任何特定的数据模型或数据源的特定实现。这意味着你可以使用你最喜欢的图书馆来管理数据源，如翻新，房间，领域或其他任何东西。您所需要做的就是确保您的存储控制器类实现了一个数据源接口。

正如前面提到的，库的主要任务是在两个数据源之间同步请求和数据。在源上执行给定的请求会导致请求产生的数据传输到输出数据流。输出数据流可以被更高层永久订阅，因为它被设计为仅发布数据更新。任何错误/异常都将发布在输入请求流上，如创建、更新或删除。这些流由 RxJava 2 Completables 表示。输出数据流由 rx Java 2 flow 表示。

## 使用

我们创建这个库的主要目标是减少在移动应用程序中实现数据层所需的时间。到目前为止，为了实现数据层，必须编写负责管理存储(数据源)的类、数据模型映射器、处理查询的类等。您还需要编写最复杂和最容易出错的元素——负责在数据源之间传递数据的同步逻辑控制器。使用 RepoLib，所有逻辑都被定义一次，为每个数据模型提供了统一的架构。您需要做的就是实现源代码和模型。

### [计] 下载

RepoLib Rx 是一个开源库，在 Apache 2.0 许可下发布。它的源代码发布在 [GitHub](http://web.archive.org/web/20221004140759/https://github.com/netguru/repolib-android) 库中。这个库也可以在 [Bintray/Maven repository](http://web.archive.org/web/20221004140759/https://bintray.com/netguru/maven) 中作为编译后的工件获得。这意味着可以使用 Gradle build 系统直接从 Maven repo 轻松下载 lib。这是下载和附加库作为项目依赖项的推荐方式。

要在您的项目中使用该库，请将 Netguru Maven URLs 添加到 repositories 块:

```
repositories {
	maven { url 'https://dl.bintray.com/netguru/maven/' }
}
```

然后将以下依赖项添加到应用程序的 build.gradle 模块中:

```
dependencies {
	implementation 'com.netguru.repolibrx:repolibrx:0.5'
}
```

### 履行

为了能够使用这个库，除了下载之外，还需要实现几个元素。初始化的整个过程包括以下步骤:

1.  创建数据模型实体。
2.  实现一个请求策略工厂接口。
3.  实现两个数据源( [DataSource 接口](http://web.archive.org/web/20221004140759/https://github.com/netguru/repolib-android/blob/master/repolibrx/src/main/kotlin/com/netguru/repolibrx/datasource/DataSource.kt)):
    1.  远程数据源，
    2.  本地数据源。
4.  初始化库。

一个示例实现可能如下所示:

1.创建数据模型实体。

```
data class DemoDataEntity(val id: Long, val value: String)
```

2.实现一个请求策略工厂接口。

```
class DemoAppRequestStrategyFactoryFactory : RequestsStrategyFactory {

    override fun  select(request: Request): Strategy = when (request) {
        is Request.Create -> RequestStrategy.OnlyRemote
        is Request.Update -> RequestStrategy.OnlyRemote
        is Request.Delete -> RequestStrategy.OnlyRemote
        is Request.Fetch -> RequestStrategy.LocalAfterFullUpdateOrFailureOfRemote
    }
}
```

您也可以跳过这一点，使用[DefaultRequestStrategyFactory](http://web.archive.org/web/20221004140759/https://github.com/netguru/repolib-android/blob/master/repolibrx/src/main/kotlin/com/netguru/repolibrx/strategy/DefaultRequestsStrategyFactory.kt)。

3.实现两个数据源接口:

a.基于[改型](http://web.archive.org/web/20221004140759/https://github.com/square/retrofit)的远程数据源实现

```
 class RetrofitDataSource(private val api: API) : DataSource {

    override fun create(entity: DemoDataEntity): Observable = api.create(entity)
    override fun update(entity: DemoDataEntity): Observable = api.update(entity)

    override fun delete(query: Query)
            : Observable {
        return if (query is QueryWithParams) {
            api.delete(id = query.param("id")).toObservable()
        } else {
            Observable.error(UnsupportedOperationException("Unsupported query: $query"))
        }
    }

    override fun fetch(query: Query): Observable = api.get()
            .flatMap { Observable.fromIterable(it) }
} 
```

b.本地数据源

本地数据源可以以类似于上述改进示例的方式手动实现。您还可以使用我们预定义的适配器之一，它包含数据源接口的现成实现。您可以使用这两种适配器:

4\. Initialize the library

```
val repolib = createRepo {
    		localDataSource = localDemoDataSource
            remoteDataSource = remoteDemoDataSource
            requestsStrategyFactory = demoAppRequestStrategyFactory
    } 
```

你也可以跳过 *requestsStrategyFactory* 的赋值来使用默认工厂。你也可以使用一个构造函数来初始化这个库，而不是使用 *createRepo* 函数

现在您可以在项目中使用全新的 RepoLibRx 实例了。要在数据源上执行请求，只需订阅以下函数之一:

```
    fun create(T):Completable 
    ```

    创建 T 类型的传递实体模型

```
    fun update(T):Completable 
    ```

    更新传递的 T 类型的实体模型

```
    fun delete(Query):Completable 
    ```

    删除与传递的查询对象匹配的实体

```
    fun fetch(Query):Completable 
    ```

    获取与传递的查询对象匹配的所有对象

要接收数据更新，请订阅:

```
fun outputDataStream(): Flowable<T>
```

请记住，从这些函数返回的变量中发出的数据取决于 DataSource 接口的实现。如果您不返回某些请求的数据，您将无法在此流中获得数据更新。

## 数据源实现

整个库初始化过程中最复杂的阶段是数据源的实现——本地的和远程的。此任务要求您根据数据源接口和 Rx API 提供的要求调整存储库的 API。此外，有必要实现负责将通用查询对象翻译成特定于工具的查询的映射器(例如 RealmQuery for Realm 或 SQL String query for Room)。此外，一些工具要求您使用它们特定的数据模型，例如，Realm 要求数据模型扩展一个 RealmObject 抽象类以存储在其数据库中。这要求您实现额外的功能，将数据模型从特定于业务的模型转换到 RealmObjects，反之亦然。此外，添加负责处理单个操作的逻辑会使此类非常复杂，并且需要大量样板文件。

为了减少编写如此复杂的类的需要，我们为两个最流行的存储库- [领域](http://web.archive.org/web/20221004140759/https://realm.io/blog/realm-for-android/)和[房间](http://web.archive.org/web/20221004140759/https://developer.android.com/topic/libraries/architecture/room)准备了两个适配器。适配器包含一个 DataSource 接口的实现，该接口包装了存储 API 以满足接口需求。使用这样的适配器大大减少了编写整个数据源的需要。这意味着它减少了开发所需的时间。使用适配器，您只需要编写查询和数据映射器，让它们理解您的数据模型和查询。自述文件中提供了使用示例的详细说明:

这两个适配器都是开源的，在 Apache 2.0 许可下发布。两者都可以在 Bintray 存储库中找到。您可以通过在 Gradle 文件的 dependency 部分添加下面一行来下载它们:

对于房间适配器:

```
implementation 'com.netguru.repolibrx:roomadapter:0.5'
```

对于领域适配器:

```
implementation 'com.netguru.repolibrx:realmadapter:0.5'
```

请记住将相关的存储工具——房间或领域——添加到您的配置中，并根据相关文档对它们进行初始化。这两个步骤都是使用上述适配器所必需的，因为适配器只是这些工具的包装器，以满足 RepoLib Rx 的 DataSource 接口所提供的需求。

更多信息

## 你可以在 [Github](http://web.archive.org/web/20221004140759/https://github.com/netguru/repolib-android) 库和每个适配器- [领域适配器](http://web.archive.org/web/20221004140759/https://github.com/netguru/repolib-android/tree/master/realmadapter)和[房间适配器](http://web.archive.org/web/20221004140759/https://github.com/netguru/repolib-android/tree/master/roomadapter)的自述文件中找到更多细节。该库还包含一个示例应用程序，它是在工作应用程序中使用该库的一个例子。该应用非常简单，向用户展示了如何将 RepoLib Rx 与基于 [Dagger 2](http://web.archive.org/web/20221004140759/https://github.com/google/dagger) 的依赖注入模式和基于 [Android 架构组件](http://web.archive.org/web/20221004140759/https://developer.android.com/topic/libraries/architecture)的示例 MVVM 架构相集成。该应用程序允许你创建简单的笔记，并将其存储在本地或远程数据库中。远程数据库是用 retreate 和 OkHttp 实现的。请注意，web 服务器在使用 OkHttp [请求拦截器](http://web.archive.org/web/20221004140759/https://github.com/square/okhttp/wiki/Interceptors)的应用程序中被模仿。该应用程序还实现了适配器。默认情况下，使用 Realm 适配器，但是也包括了 Room 适配器的完整实现。

可以在源代码中以 [KDoc](http://web.archive.org/web/20221004140759/https://kotlinlang.org/docs/reference/kotlin-doc.html) s 的形式找到对库、适配器和示例应用程序的各个组件的更详细描述。如果您发现任何 bug，请不要犹豫，在 GitHub 上开一张罚单，或者创建一个带有修复程序的 PR 并提及我们。我们希望我们的库可以帮助您加快开发速度，让您节省一些时间。