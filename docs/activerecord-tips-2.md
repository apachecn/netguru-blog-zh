# ActiveRecord -第 2 部分:有用的方法

> 原文：<http://web.archive.org/web/20230307163032/https://www.netguru.com/blog/activerecord-tips-2>

 在[第一部分](/web/20221226224529/https://www.netguru.com/blog/activerecord-tips-1)中，我们讨论了“N+1 查询”问题以及如何使用 Rails 的 ActiveRecord 来处理它。在这一部分中，我们将讨论一些其他有用的 ActiveRecord 方法，它们可以帮助我们更快地或者只是以一种更优雅的方式获得一些结果。

## #地图 vs #拔毛

假设我们想获取所有客户的电子邮件地址。我们可以这样做:

```
Client.all.map(&:email)
```

在这种情况下，幕后发生了什么？简单来说:

1.Rails 使用以下查询从数据库获取数据:

```
SELECT "clients".* FROM "clients"
```

2.从所获取的数据中，创建客户端对象的集合

3.Ruby 遍历整个集合，从每个对象获取 email 属性，并将其存储在新的集合(一个数组)中

4.返回新创建的数组

现在，让我们将只从 Ruby 获取客户端电子邮件地址的责任直接转移到数据库。我们可以通过使用# pull*方法来实现:*

```
Client.pluck(:email)
```

在这种情况下，将执行以下查询

```
SELECT "clients"."email" FROM "clients"
```

瞧，我们可以观察到同样的结果。

不同之处在于，在第一个例子中，我们获取了所有的数据，然后 Ruby 必须处理这些数据。在第二个例子中，我们告诉数据库只获取 email 列/属性。

从下表中，您可以看到数据库处理该任务的速度要快得多。

|  | **时间** *【秒】* |
| **#拔毛** | 0.0040 |
| **#地图** | 0.0306 |
| *(数据库中的 1000 个客户端)* |

**重要提示**

我们传递给*#**puck*方法的参数(是的，我们可以一次获取多个属性)只不过是数据库中列的名称。由于这个原因，我们不能使用这个方法来映射记录，例如，在我们的模型中使用一个自定义方法。

```
class Client < ApplicationRecord
  ...
  def visible?
    [true, false].sample
  end
end
```

出于明显的原因，我们不能在*可见的情况下调用*# pull*方法？*论证，仅仅是因为没有*可见吗？*数据库表中的列。在这种情况下，我们只能使用 *#map* 的方法。

**另一个有用的东西**

*# puck*方法的一个典型用例是当我们想从数据库中检索一个 id(主键)列表时。

```
Client.pluck(:id)
```

我们可以通过编写更少的代码并使用 *#* *ids* 方法:来做到这一点

```
Client.ids
```

## #总和

假设我们想知道商店中所有订单的总和。

有两种简单的方法可以实现这一点:

```
1) Order.sum(:total)
2) Order.sum(&:total)
```

这两个代码行看起来非常相似。不同的是，在一种情况下，我们传递一个简单的符号作为参数，而在另一种情况下，我们传递一个块。执行上的差异是显著的。将执行以下查询

```
1) SELECT SUM("orders"."total") FROM "orders"
2) SELECT "orders".* FROM "orders"
```

如我们所见，在第一种情况下，我们将计算订单总数的责任转移到了数据库上。

第二种情况更复杂。首先，Rails 从数据库中获取所有订单。创建一个由*个订单*个对象组成的集合。然后 Ruby 映射集合——它遍历所有项目，并从它们那里获取*总*属性。我们最终得到一个包含每个订单的总属性的数组。现在，ruby 在创建的数组上调用 *#sum* 方法，这将产生所需的值。

同样，正如您在下表中看到的，数据库的速度要快得多。

|  | **时间** *【秒】* |
| **使用符号** | 0.0032 |
| **使用块** | 0.0916 |
| *(数据库中的 5000 个订单)* |

## #uniq

*这对 RAILS 5.x 不再有效，在 Rails 5.x 中，没有静态。ActiveRecord::基类的 uniq 方法。*

另一个有趣的例子说明了执行方法的顺序是多么重要。假设我们想列出在我们店里至少下过一次订单的客户的所有电子邮件地址。这个列表应该包含唯一的值，这样如果有人做了一个以上的订单，他们的电子邮件应该只出现一次。

好吧。有两种简单的方法可以实现这一点:

```
1) Order.pluck(:email).uniq
2) Order.uniq.pluck(:email)
```

正如你所看到的，这些例子只是在我们调用*#**&*#**uniq*方法的顺序上有所不同。在这两个例子中，数据库只负责获取电子邮件地址(所以 Ruby 不需要映射额外的数据)。那么区别在哪里呢？请查看将在以下每种情况下执行的查询:*

```
1) SELECT "orders"."email" FROM "orders"
2) SELECT DISTINCT "orders"."email" FROM "orders"
```

区别就在这里。在第二种情况下，数据库负责筛选唯一值(通过使用 DISTINCT 指令)。在第一种情况下，Rails 获取所有的电子邮件地址，从它们创建一个数组，然后在其上调用 *Array#uniq* 方法。

下表显示了性能差异:

|  | **时间** *【秒】* |
| **#uniq - Array#uniq** | 0.0762 |
| **#独特的** | 0.0197 |
| *(数据库中的 5000 个订单)* |

#更新 _ 全部

此方法用于...批量更新记录:)V 非常有用，但也不是没有缺陷。

假设我们的商店系统中有一些订单。我们希望识别所有尚未完成(即，它们仍处于购物车状态)且一周内未更新的订单。然后我们必须在所有这样的订单上将*无效*标志设置为*真*。

这样做的第一个想法是:

当然，这很有效。但是我们来分析一下解决方案的成本。执行一个查询来获取符合给定标准的所有订单，然后执行 *n* 个查询来更新每个订单。当然， *n* 是第一次查询返回的订单数。成本相当高，尤其是当我们有很多记录要更新的时候。

```
Order.where(state: 'cart').where('updated_at < ?', 7.days.ago).each do |order|
  order.update(inactive: true)
end
```

ActiveRecord 也为我们提供了一个解决方案。是 *#update_all* 方法:

所有记录都将在一次查询中更新。

```
Order.where(state: 'cart').where('updated_at < ?', 7.days.ago).update_all(inactive: true)
```

警告？当然也有一些。通过使用 *#update_all* 方法，我们创建了一个原始 SQL 查询，并将其直接发送到数据库，这意味着该方法省略了在我们的模型上设置的所有回调:验证、after_save 等。正因为如此，如果我们在很大程度上依赖于这样的回调，我们必须非常小心地使用这种方法。否则，我们的应用程序可能会出现数据不一致的情况。

摘要

## 查看所有这些性能比较表，我们可以得出一个简单的结论:在检索、解析或处理数据方面，数据库总是比 Ruby 快。那么我们应该总是要求数据库做这样的事情吗？当然不是。一如既往，没有灵丹妙药。不朽的声明:“这取决于”在这里也是有效的。

我们能承受长时间锁定数据库，而不是发出一个简单的请求，让 Ruby 运行更复杂的操作吗？当然，Ruby 将花费更长的时间来处理相同的查询，但同时，数据库将可用于执行其他操作。

根据应用的逻辑、应用的架构或硬件能力，上述问题和其他相关问题的答案会有所不同。

我们需要知道的是，ActiveRecord 相当灵活。它基于某些约定为我们做了许多事情，但同时，它允许我们忽略这些默认约定，按照我们想要的方式做事。我们可以真正控制活动记录如何执行其操作。

*测量是在 Ruby 2.5.0 和 Ruby on Rails 5.2.0 上进行的*

*Measurements were made on Ruby 2.5.0 and Ruby on Rails 5.2.0***