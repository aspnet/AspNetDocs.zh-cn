---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
title: 数据存储选项 （使用 Azure 构建实际云应用） |Microsoft Docs
author: MikeWasson
description: 构建真实世界云应用与 Azure 的电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践可以他...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: e51fcecb-cb33-4f9e-8428-6d2b3d0fe1bf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/data-storage-options
msc.type: authoredcontent
ms.openlocfilehash: 8656f4a4211c2e97d71d76dd2f799412539896ca
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65118851"
---
# <a name="data-storage-options-building-real-world-cloud-apps-with-azure"></a>数据存储选项 （使用 Azure 构建实际云应用）

通过[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)

[下载修复此错误项目](http://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](http://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **构建真实世界云应用，使用 Azure**电子书基于由 Scott Guthrie 开发的演示文稿。 它还说明了 13 模式和实践，从而帮助您获得成功开发适用于在云中的 web 应用。 有关电子书的信息，请参阅[的第一章](introduction.md)。

大多数人习惯于关系数据库，并忽略其他数据存储选项，当它们设计云应用程序时，他们往往。 结果可以为性能不佳，高开支，甚至更糟糕，因为[NoSQL](http://en.wikipedia.org/wiki/NoSQL) （非关系） 的数据库可以比关系数据库更有效地处理某些任务。 如果客户向我们寻求帮助解决关键数据存储问题，通常是因为它们具有关系数据库，NoSQL 选项之一会起作用更好地。 在这些情况下客户会做得更好关闭如果这些应用部署到生产环境之前实现了 NoSQL 解决方案。

但是，它也是错误地假定是 NoSQL 数据库，可以执行任何操作，良好，甚至还不够。 所有数据存储任务; 没有单一最佳数据管理选项针对不同的任务，不同的数据管理解决方案进行了优化。 大多数实际云应用程序具有各种数据存储要求和通常提供最佳的多个数据存储解决方案的组合。

本章旨在让你更广泛可用的数据存储选项为云应用程序，以及有关如何选择适合你的方案的一些基本指导。 最好的选项供你了解并考虑其优势和劣势之前开发的应用程序。 更改生产应用中的数据存储选项可能会极其困难，如无需更改 jet 引擎，而在平面处于飞行状态。

## <a name="data-storage-options-on-azure"></a>在 Azure 上的数据存储选项

在云中，使相对容易地使用各种关系和 NoSQL 数据存储。 以下是一些可以在 Azure 中使用的数据存储平台。

![](data-storage-options/_static/image1.png)

表显示了四种类型的 NoSQL 数据库：

- [键/值数据库](https://msdn.microsoft.com/library/dn313285.aspx#sec7)存储每个键值的单个序列化的对象。 它们适用于存储大量数据的你想要为给定键值获取一个项，并且不具有基于项的其他属性的查询。

    [Azure Blob 存储](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/)是功能类似于文件存储在云中的键值的对应于文件夹和文件名称的键/值数据库。 检索由其文件夹和文件名称，而不是搜索文件内容中的值的文件。

    [Azure 表存储](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/)也是键/值数据库。 每个值被称为*实体*（类似于一个行，由分区键和行键标识） 和包含多个*属性*(类似于的列，但需要共享同一个表中的不是所有实体列）。 对非键列的查询是极其低效的应当避免。 例如，你可以使用一个分区将存储有关单个用户的信息存储用户配置文件数据。 在单独的一个实体的属性或在同一个分区中的不同实体可以存储数据，例如用户名、 密码哈希、 出生日期等。 你不想要查询具有给定的出生日期范围的所有用户，但不能配置文件表与另一个表之间执行联接都查询。 表存储是更具可伸缩性、 成本更低比关系数据库中，但它并不启用复杂的查询或联接。
- [Documentdatabases](https://msdn.microsoft.com/library/dn313285.aspx#sec8)的值是在其中的键/值数据库*文档*。 "文档"下面未使用 Word 或 Excel 文档的意义上说，但意味着命名的字段和值，其中的任何一可能是子文档的集合。 例如，订单历史记录表中可能有订单文档，订单号、 订单日期和客户字段中;和客户字段可能具有名称和地址字段。 数据库对的格式如 XML、 YAML、 JSON 或 BSON; 中的字段数据进行编码也可以使用纯文本。 设置键/值数据库除了文档数据库的一个功能是能够查询对非键字段并定义辅助索引来提高查询效率。 此功能会使文档数据库更适用于需要检索基于比文档键的值更复杂的条件的数据的应用程序。 例如，销售订单历史记录文档数据库中您可以查询等产品 ID、 客户 ID、 客户名称等各种字段。 [MongoDB](http://www.mongodb.org/)是流行的文档数据库。
- [列系列数据库](https://msdn.microsoft.com/library/dn313285.aspx#sec9)是键/值数据存储，使您将结构数据存储到名为列系列的相关列的集合。 例如，人口普查数据库可能有一组列用于人员的姓名 （名字、 中间名，最后一次），有一个组，此人的地址和有关联系人的配置文件信息 (DOB，性别，等等) 的一个组。 数据库可以然后存储每个列系列中一个单独的分区同时保持所有人与相同的密钥相关的数据。 然后可以读取所有配置文件信息，而无需通读所有名称和地址信息。 [Cassandra](http://cassandra.apache.org/)是一个流行的列系列数据库。
- [图形数据库](https://msdn.microsoft.com/library/dn313285.aspx#sec10)信息存储为对象和关系的集合。 图形数据库旨在使应用程序能够有效执行需遍历它们之间的网络的对象和关系查询。 例如，对象可以是员工在人力资源数据库中，并且你可能想以简化查询如"查找所有直接或间接地工作的员工 Scott 的"。 [Neo4j](http://www.neo4j.org/)是常用的图形数据库。

与关系数据库相比，大得多的可伸缩性和成本效益的存储和分析非结构化数据提供 NoSQL 选项。 弊端是，它们不提供的丰富 queryability 和关系数据库的功能强大的数据完整性功能。 NoSQL 将适用于 IIS 日志数据，这涉及到大量而无需联接查询。 NoSQL 将无法成功得很好，银行事务，它需要绝对数据完整性并涉及与其他帐户相关的数据的多个关系。

此外，还有名为数据库平台的较新类别[NewSQL](http://en.wikipedia.org/wiki/NewSQL) queryability 和关系数据库的事务完整性使用结合 NoSQL 数据库的可伸缩性。 NewSQL 数据库专为分布式的存储和查询处理，通常很难实现"OldSQL"数据库中。 [NuoDB](http://www.nuodb.com/)是可以在 Azure 使用 NewSQL 数据库的示例。

<a id="hadoop"></a>
## <a name="hadoop-and-mapreduce"></a>Hadoop 和 MapReduce

可以在 NoSQL 数据库中存储的数据的大量可能很难及时有效地分析。 为此，可以使用之类的框架[Hadoop](http://hadoop.apache.org/)可实现[MapReduce](http://en.wikipedia.org/wiki/MapReduce)功能。 实质上是 MapReduce 进程的作用是以下情况：

- 需要通过选择从数据处理的数据量仅你实际上需要分析将数据存储的限制。 例如，你想要知道用户的出生年份群的构成，因此从您用户配置文件数据存储选择仅出生年份。
- 细分为部分数据，并将其发送到不同的计算机以进行处理。 计算机 A 计算 1950年 1959年日期的人数，计算机 B 执行 1960年 1969，等等。这组计算机称为*Hadoop 群集*。
- 将每个部分结果的部件处理完成后到一起。 此时的每个出生年份的人员数量相对较短列表，并且在此列表中总体的百分比计算的任务是可管理的。

在 Azure 上， [HDInsight](https://azure.microsoft.com/services/hdinsight/)使您能够处理和分析，并使用 Hadoop 的强大功能进行大数据从中获取新信息。 例如，您可以使用它来分析 web 服务器日志：

- 启用 web 服务器日志记录到存储帐户。 此设置 Azure 将日志写入将 Blob 服务用于你的应用程序对每个 HTTP 请求。 Blob 服务基本上是云文件存储，以及它与 HDInsight 可以很好地集成。

    ![日志以 Blob 存储](data-storage-options/_static/image2.png)
- 当应用程序获取流量，web 服务器 IIS 日志将写入 Blob 存储。

    ![Web 服务器日志](data-storage-options/_static/image3.png)
- 在门户中，单击**新建** - **Data Services** - **HDInsight** - **快速创建**，并指定 HDInsight 群集名称、 群集大小 （HDInsight 群集数据节点数），以及用户名和密码为 HDInsight 群集。

    ![HDInsight](data-storage-options/_static/image4.png)

现在可以设置 MapReduce 作业来分析日志并获取问题的答案，如：

- 一天中的什么时间我的应用程序获取最高或最低流量？
- 哪些国家/地区是我从传入的流量？
- 什么是来自我的流量的区域的平均邻居收入。 （没有公用数据集，可提供邻近区域收入按 IP 地址，并且可以针对 web 服务器日志中的 IP 地址匹配的）。
- 邻居收入如何关联到特定页面或站点中的产品？

然后可以使用这些目标广告根据客户感兴趣的可能性或可能购买特定产品到问题的答案。

中所述[使一切自动化章](automate-everything.md)，可以在门户中执行大多数函数可以自动进行，并包含设置和 HDInsight 分析作业执行。 典型的 HDInsight 脚本可能包含以下步骤：

- 预配 HDInsight 群集，并将其链接到 Blob 存储输入的存储帐户。
- 将 MapReduce 作业可执行文件 （.jar 或.exe 文件） 上传到 HDInsight 群集。
- 提交 MapReduce 存储到 Blob 存储输出数据。
- 等待作业完成。
- 删除 HDInsight 群集。
- 访问 Blob 存储的输出。

通过运行脚本实现这一切，最小化预配 HDInsight 群集，这样就会减少你的成本的时间量。

<a id="paasiaas"></a>
## <a name="platform-as-a-service-paas-versus-infrastructure-as-a-service-iaas"></a>平台即服务 (PaaS) 与基础结构即服务 (IaaS)

前面列出的数据存储选项包括平台-作为-服务 (PaaS) 和基础结构-一种即服务 (IaaS) 解决方案。 PaaS 意味着我们管理的硬件和软件基础结构，只需使用该服务。 SQL 数据库是 Azure PaaS 功能。 要求提供数据库，也在后台 Azure 将设置和配置 Vm 并设置其上的数据库。 您不能直接访问 Vm，无需对其进行管理。IaaS 意味着设置、 配置和管理在我们数据中心基础结构中运行的 Vm 和您随意设置它们。 我们提供预配置的 VM 映像的库的常见 VM 配置。 例如，可以为 Windows Server 2008、 Windows Server 2012 中，BizTalk Server、 Oracle WebLogic Server、 Oracle 数据库等安装预配置的 VM 映像。

Azure 提供的 PaaS 数据解决方案包括：

- Azure SQL 数据库 （以前称为 SQL Azure）。 基于 SQL Server 上的云关系数据库。
- Azure 表存储。 键/值的 NoSQL 数据库。
- Azure Blob 存储。 文件存储在云中。

对于 IaaS，可以运行任何内容加载到一个 VM，例如：

- 例如，SQL Server、 Oracle、 MySQL、 SQL Compact、 SQLite 或 Postgres 的关系数据库。
- 例如 Memcached、 Redis、 Cassandra 和 Riak 键/值数据存储。
- 列数据存储，如 HBase。
- 文档数据库，如 MongoDB、 RavenDB 和 CouchDB。
- 例如，Neo4j 的图形数据库。

![在 Azure 上的数据存储选项](data-storage-options/_static/image5.png)

IaaS 选项可提供几乎无限制的数据存储选项，以及其中有多少已尤其是易于使用，因为您可以创建使用预配置的映像的 Vm。 例如，在管理门户，转到**虚拟机**，单击**映像**选项卡，然后单击**浏览 VM 仓库**。

![浏览 VM 仓库](data-storage-options/_static/image6.png)

然后，您看到一系列[数百个预配置的 VM 映像](http://www.hanselman.com/blog/Over400VirtualMachineImagesOfOpenSourceSoftwareStacksInTheVMDepotAzureGallery.aspx)，并从已预安装的数据库管理系统的映像，例如 MongoDB、 Neo4J、 Redis、 Cassandra 或 CouchDB，可以创建 VM:

![VM 仓库 MongoDB](data-storage-options/_static/image7.png)

Azure 使 IaaS 数据存储选项一样易于使用，但 PaaS 产品/服务有很多优点，使它们更经济高效且适合许多方案：

- 无需创建 Vm，你只需使用门户或脚本来设置数据存储区。 如果你想 200 terabyte 数据存储区，可以只需单击一个按钮或运行命令，并在数秒内就可以供你使用。
- 无需管理或修补虚拟机使用的服务;Microsoft 会为你自动。-无需担心如何设置缩放或高可用性; 基础结构Microsoft 为你处理所有这些。
- 无需购买许可证;许可费用包含在服务费用。
- 只需为所用内容付费。

在 Azure 中的 PaaS 数据存储选项包括受第三方提供商的产品/服务。 例如，可以选择[MongoLab 外接程序](https://azure.microsoft.com/documentation/articles/store-mongolab-web-sites-dotnet-store-data-mongodb/)从 Azure 应用商店来预配 MongoDB 数据库即服务。

## <a name="choosing-a-data-storage-option"></a>选择一个数据存储选项

没有一种方法是适用于所有方案。 如果任何人都认为这项技术是答案，第一件事就是"是什么问题？"，因为不同的解决方案进行了优化用于执行不同操作。 好处很多到关系模型;这就是为什么它已经推出因此长时间。 但也向下-SQL 与 NoSQL 解决方案可以解决的方面。

通常我们看到的内容最佳工作便是组合的方法，可以使用 SQL 和 NoSQL 单个解决方案中。 甚至当人说他们要接纳 NoSQL，是否您深入了解自己在做什么您通常查找它们都使用多个不同的 NoSQL 框架： 他们使用[CouchDB](http://wiki.apache.org/couchdb/Introduction)，并[Redis](http://redis.io/)，和[Riak](http://basho.com/riak/)用于执行不同操作。 甚至 Facebook，大量使用 NoSQL，该服务的不同部分使用不同的 NoSQL 框架。 灵活地混合和匹配数据的存储方法是因为这样可以轻松使用多个数据解决方案，并将其集成在单个应用的云的好处的项目之一。

下面是要考虑当您选择一种方法的一些问题：

| 语义数据 | -什么是核心数据存储和数据访问语义 （您存储关系或非结构化数据）？ 在 blob 存储时，最适合非结构化的数据，例如媒体文件相关数据，例如产品、 清单、 供应商、 客户订单等一系列适合在关系数据库中。 |
| --- | --- |
| 查询支持 | -如何轻松是它来查询数据？ -什么类型的问题可以有效地要求？ 键/值数据存储是很好地获取给定键的值的单个行，但对于复杂的查询不那么理想。 用户配置文件数据存储都能得到一个特定用户的数据，键/值数据存储可能工作正常;要获取基于各种产品属性的不同分组的产品目录的关系数据库可能更好地工作。 NoSQL 数据库可以高效地存储数据量很大，但必须围绕如何应用查询的数据，数据库的结构和这会使即席查询很难执行。 使用关系数据库中，您可以构建几乎任何类型的查询。 |
| 功能投影 | -可以问题、 聚合，等等，在执行的服务器端？ 如果我运行 SELECT COUNT (\*) 从 SQL 中的表，它将非常高效地执行在服务器上的所有工作并返回的数字我在寻找。 如果我想从一个 NoSQL 数据存储，不支持聚合相同的计算，这是一个效率低下的"未绑定的查询"，可能会超时。即使成功执行查询我需要向客户端从服务器检索的所有数据和客户端上的行进行计数。 -可以使用何种语言或表达式的类型？ 与关系数据库中，我可以使用 SQL。 使用某些 NoSQL 数据库，如 Azure 表存储，我将使用[OData](http://www.odata.org/)，和我可以做的就是对主键进行筛选，然后获取的投影 （选择可用的字段的子集）。 |
| 容易伸缩 | -如何通常和如何太多将数据需要进行缩放？ -在平台本机实现向外扩展？ -如何轻松将它添加/删除容量 （大小和吞吐量）？ 关系数据库和表不会自动分区以使其可缩放，因此它们难以扩展超过一定的限制。 如 Azure 表存储的 NoSQL 数据存储本质上是分区的所有内容，并添加分区几乎没有任何限制。 你可以轻松缩放表存储，最多 200 兆兆字节，但 Azure SQL 数据库的最大数据库大小为 500 千兆字节为单位。 可以通过将划分到多个数据库，来缩放关系数据，但设置应用程序以支持该模型包含大量的编程工作。 |
| 检测和可管理性 | -如何轻松是能够检测、 监视和管理平台？ 将需要以随时了解有关的运行状况和性能的数据存储区，因此需要提前知道一个平台，免费提供的指标，必须开发自己。 |
| 操作 | -如何轻松是平台来部署和在 Azure 上运行？ PaaS？ IaaS？ Linux？ 表存储和 SQL 数据库非常轻松地在 Azure 上设置了。 不是内置的 Azure PaaS 解决方案的平台需要更多工作。 |
| API 支持 | -是可轻松地使用平台的 API？ 对于 Azure 表服务不存在与支持.NET 4.5 的异步编程模型的.NET API 的 SDK。 如果您正在编写一个.NET 应用程序，它将更轻松地编写和测试代码到另一个键/值列的数据存储区平台具有任何 API 或一个不太全面比较 Azure 表服务。 |
| 事务的完整性和数据一致性 | -是关键平台支持的事务以保证数据的一致性？ 用于跟踪批量电子邮件发送，性能和低数据存储成本可能比自动支持事务或数据平台中的引用完整性更重要使 Azure 表服务的一个不错选择。 用于跟踪银行帐户余额或采购订单的一个关系数据库平台，提供强事务保证会更好的选择。 |
| 业务连续性 | -如何轻松是备份、 还原和灾难恢复？ 生产数据还是迟早会遭到损坏，你将需要撤消的功能。 关系数据库通常具有更多的细粒度的还原能力，例如能够还原到的时间点。 了解你正在考虑每个平台中提供的还原功能的是要考虑的一个重要因素。 |
| 成本 | -如果多个平台可支持你的数据的工作负荷，两者有何差别的成本？ 例如，如果您使用 ASP.NET 标识，您可以在 Azure 表服务或 Azure SQL 数据库中存储用户配置文件数据。 如果你不需要的丰富的查询的 SQL 数据库功能，则可以选择 Azure 表部分因为花费很多较少的给定存储量。 |

什么我们通常建议就是选择你的数据存储解决方案之前了解每个类别中的问题的答案。

此外，你的工作负荷可能具有某些平台可以比其他更好地支持的特定要求。 例如：

- 不会应用程序需要审核功能？
- 你的数据的使用寿命要求是什么--是否需要自动存档或清除功能？
- 你是否有专门的安全需求？ 例如，数据包括 PII （个人身份信息），但必须要能够确保，查询结果中排除 PII。
- 如果有不能出于法规或技术原因而在云中存储一些数据，可能需要一个云数据存储平台，便于使用的本地存储集成。

## <a name="demo--using-sql-database-in-azure"></a>演示 – 在 Azure 中使用 SQL 数据库

Fix It 应用程序使用关系数据库来存储任务。 中所示的环境创建 Windows PowerShell 脚本[使一切自动化章](automate-everything.md)创建两个 SQL 数据库实例。 您可以看到这些门户中通过单击**SQL 数据库**选项卡。

![在门户中的 SQL 数据库](data-storage-options/_static/image8.png)

它也很容易通过使用门户来创建数据库。

单击**新建-数据服务** -- **SQL 数据库** -- **快速创建**，输入数据库名称，选择你的帐户中已有的服务器或创建一个新的活动，然后单击**创建 SQL 数据库**。

![新建 SQL 数据库](data-storage-options/_static/image9.png)

请等待几秒钟，并随时可以使用 Azure 中有一个数据库。

![新创建的 SQL 数据库](data-storage-options/_static/image10.png)

使 Azure does 在几秒内容可能需要在一天或每周或更长时间才能在本地环境中完成。 并且由于可以轻松地创建的数据库会自动在脚本中或通过使用管理 API，可以动态横向扩展通过你的数据分散到多个数据库，只要被编程为此，你的应用程序。

这是我们的平台即服务模型的示例。 无需管理的服务器，我们执行此操作。 无需担心如何备份，我们执行此操作。 在高可用性-运行自动在三个服务器之间复制数据库中的数据。 如果一台计算机出现故障，我们自动故障转移，并且会丢失任何数据。 定期修补服务器，无需担心的。

单击一个按钮，就需要可以立即开始使用新的数据库的确切的连接字符串。

![连接字符串](data-storage-options/_static/image11.png)

仪表板显示连接历史记录和使用的存储量。

![SQL Database 仪表板](data-storage-options/_static/image12.png)

您可以管理门户中的数据库，或通过使用 SQL Server 工具您已经熟悉，包括 SQL Server Management Studio (SSMS) 和 SQL Server 对象资源管理器 (SSOX) 和服务器资源管理器的 Visual Studio 工具。

![SSOX](data-storage-options/_static/image13.png)

另一个优势是定价模型。 可以使用免费的 20 MB 数据库，开始开发和生产数据库启动时大约为每月 5 美元。 仅对于实际存储在数据库中，不的最大容量的数据量付费。 您无需购买许可证。

SQL 数据库是轻松地扩展规模。 对于 Fix It 应用，我们在我们的自动化脚本中创建的数据库上限为 1 千兆。 如果你想要将其扩展到 150 千兆，只是可以转到门户并更改该设置，或执行 REST API 命令，并在数秒内有 150 千兆数据库可部署到的数据。

![SQL 数据库版本和大小](data-storage-options/_static/image14.png)

这就是云来快速轻松地构建基础结构并立即开始使用它的强大功能。

Fix It 应用程序使用两个 SQL 数据库，一个用于成员资格 （身份验证和授权），一个用于数据，而这是您只需对它进行设置并将其扩展。 您以前看到过如何预配数据库通过 Windows PowerShell 脚本，现在还看到将为在门户中是多么容易。

## <a name="entity-framework-versus-direct-database-access-using-adonet"></a>与直接数据库访问使用 ADO.NET 实体框架

Fix It 应用通过使用实体框架来访问这些数据库，Microsoft 建议为.NET 应用程序的 ORM （对象关系映射程序）。 ORM 是一个很好的工具，便于开发人员工作效率，但工作效率的代价是在某些情况下导致性能下降。 在真实世界云应用程序中不会进行一个选择是使用 EF 还是直接使用 ADO.NET--你将同时使用。 大多数情况下当您编写的代码使用数据库，可以获得最大的性能并不重要，并可以充分利用简化的编码和测试，获取使用实体框架。 在 EF 开销导致不可接受的性能的情况下，可以编写和执行查询使用 ADO.NET，理想情况下通过调用存储的过程。

你想要最大程度减少通信频率"尽可能多地用于访问数据库时，任何方法。 换而言之，如果在一个更大的查询结果集而不是几十个还是几百个较小的可以获取所需的所有数据，则通常更可取。 例如，如果需要对列表的学生和中注册的课程，是通常更好，若要获取所有一个联接查询而不是在一个查询中获取学生和执行每个学生的课程的单独查询中的数据。

## <a name="sql-databases-and-the-entity-framework-in-the-fix-it-app"></a>SQL 数据库和修复其应用中的实体框架

修复其应用中`FixItContext`类，该类派生自 Entity Framework`DbContext`类中标识的数据库，并在数据库中指定的表。 上下文指定实体集 （表） 的任务，然后代码将传递中对上下文连接字符串名称。 该名称是指定义 Web.config 文件中的连接字符串。

[!code-csharp[Main](data-storage-options/samples/sample1.cs?highlight=4,8)]

中的连接字符串*Web.config*文件被命名为 appdb （此处指向本地开发数据库）：

[!code-xml[Main](data-storage-options/samples/sample2.xml?highlight=3)]

实体框架将创建*FixItTasks*表中包含的属性上基于`FixItTask`实体类。 这是一个简单的 POCO （普通旧 CLR 对象） 类，这意味着它不会继承自或实体框架存在任何依赖关系。 但是，实体框架知道如何创建基于该表并执行与其 CRUD （创建-读取-更新-删除） 操作。

[!code-csharp[Main](data-storage-options/samples/sample3.cs)]

![FixItTasks 表](data-storage-options/_static/image15.png)

Fix It 应用包含它的 CRUD 操作使用的数据存储区使用一个存储库界面。

[!code-csharp[Main](data-storage-options/samples/sample4.cs)]

请注意，存储库方法是所有异步，因此，可以完全异步的方式完成的所有数据访问。

存储库实现调用 Entity Framework 异步方法来处理数据，包括 LINQ 查询还与插入、 更新和删除操作。 下面是代码的用于查找 Fix It 任务示例。

[!code-csharp[Main](data-storage-options/samples/sample5.cs)]

您会注意到还有一些计时和错误日志记录代码中，我们将看看这个更高版本中[监视和遥测章](monitoring-and-telemetry.md)。

<a id="sqliaas"></a>
## <a name="choosing-sql-database-paas-versus-sql-server-in-a-vm-iaas-in-azure"></a>选择与 Azure 中的 VM (IaaS) 中的 SQL Server 的 SQL 数据库 (PaaS)

好处 SQL Server 和 Azure SQL 数据库是对这两个核心编程模型是完全相同。 可以在这两个环境中使用的大部分相同技能。 您甚至可以使用在开发过程中的 SQL Server 数据库和 SQL 数据库实例在云中，这是修复其应用的设置方式。

或者，您可以相同的 SQL Server 在云中运行在本地运行的 IaaS Vm 上安装此更新。 对于某些旧版应用程序，在 VM 中运行 SQL Server 可能会更好的解决方案。 由于在专用 VM 上运行的 SQL Server 数据库，因此它具有比共享服务器运行的 SQL 数据库数据库向其提供的更多资源。 这意味着 SQL Server 数据库可以更大并且仍具有良好的性能。 一般情况下，越小的数据库大小和表的大小，更好地用例适用于 SQL 数据库 (PaaS)。

以下是一些准则，如何以两个模型之间进行选择。

| Azure SQL 数据库 (PaaS) | 虚拟机 (IaaS) 中的 SQL Server |
| --- | --- |
| **专业人员**-无需创建或管理 Vm、 更新或修补操作系统或 SQL;Azure 会为你。 -内置的高可用性、 数据库级的 sla。 -低总拥有成本 (TCO)，因为您只需支付使用 （不需要许可证）。 -非常适合用于处理大量的小型数据库 (&lt;= 500 GB)。 -轻松地动态创建新的数据库启用横向扩展。 | ***专业人员***-与在本地 SQL Server 功能兼容。 -可以实现 SQL Server[通过 AlwaysOn 高可用性](https://www.microsoft.com/sqlserver/solutions-technologies/mission-critical-operations/high-availability.aspx)2 + Vm，VM 级别的 sla 中。 -你可以完全控制如何管理 SQL。 -可以重复使用已拥有的或按个小时付费的 SQL 许可证。 -非常适合用于处理更少但更大 (1 TB +) 数据库。 |
| **缺点**-某些功能差距相比于在本地 SQL Server (缺少[CLR 集成](https://technet.microsoft.com/library/ms131102.aspx)， [TDE](https://technet.microsoft.com/library/bb934049.aspx)，[压缩支持](https://technet.microsoft.com/library/cc280449.aspx)， [SQL ServerReporting Services](https://technet.microsoft.com/library/ms159106.aspx)等)-包含 500 GB 的数据库大小限制。 | ***缺点***-更新/修补程序 （OS 和 SQL） 由你负责-创建和管理的数据库由你负责-磁盘 IOPS （每秒输入/输出操作数） 限制为大约 8000 （通过 16 个数据驱动器）。 |

如果你想要在 VM 中使用 SQL Server，可以使用你自己的 SQL Server 许可证，或可以为一个按小时付费。 例如，在门户中或通过 REST API 可以创建新的 VM 使用的 SQL Server 映像。

![创建具有 SQL Server VM](data-storage-options/_static/image16.png)

![SQL Server VM 映像的列表](data-storage-options/_static/image17.png)

在创建 VM 具有 SQL Server 映像，费率 SQL Server 许可证成本按小时根据 VM 的使用情况。 如果必须只会运行几个月的项目，则成本按小时付费。 如果您认为您的项目转到最后一年，是更便宜，若要购买的许可证通常情况下进行的方法。

## <a name="summary"></a>总结

云计算变得切实可行来混合和匹配数据存储的方法，以便最好地满足你的应用程序的需求。 如果您正在构建新的应用程序，仔细考虑这样才能选择方法非常适用于你的应用程序的增长将继续在此处列出的问题。 [接下来的章节](data-partitioning-strategies.md)将介绍一些可用来组合多个数据存储方法的分区策略。

## <a name="resources"></a>资源

有关更多信息，请参见以下资源。

选择一个数据库平台：

- [高度可缩放解决方案的数据访问：使用 SQL、 NoSQL 和 Polyglot 持久性](https://aka.ms/dag-doc)。 电子书 Microsoft 模式与实践中的深度中放入不同类型的数据存储适用于云应用程序。
- [Microsoft 模式和做法-Azure 指南](https://msdn.microsoft.com/library/ff898430.aspx)。 请参阅数据一致性入门、 数据复制和同步的指导，索引表模式、 具体化视图模式。
- [基址：备用 Acid](http://queue.acm.org/detail.cfm?id=1394128)。 有关数据的一致性和可伸缩性方面做出权衡的文章。
- [在这七个星期中的七个数据库：现代数据库和 NoSQL 运动指南](https://www.amazon.com/Seven-Databases-Weeks-Modern-Movement/dp/1934356921)。 本书由 Eric 雷德蒙德和 Jim R.Wilson。 强烈建议引入自己的当前可用的数据存储平台范围的。

SQL Server 和 SQL 数据库之间进行选择：

- [高级 SQL Database 预览版指导](https://msdn.microsoft.com/library/windowsazure/dn369873.aspx)。 SQL 数据库高级版，以及有关何时选择而不是 SQL 数据库 Web 和企业版指南简介。
- [指导原则和限制 （Azure SQL 数据库）](https://msdn.microsoft.com/library/windowsazure/ff394102.aspx)。 链接到有关的 SQL 数据库限制的文档的门户页上，其中包括一个重点介绍该 SQL 数据库的 SQL Server 功能不支持。
- [Azure 虚拟机中的 SQL Server](https://msdn.microsoft.com/library/windowsazure/jj823132.aspx)。 链接到有关在 Azure 中运行 SQL Server 的文档的门户页面。
- [Scott Guthrie 介绍 Azure 中的 SQL 数据库](https://azure.microsoft.com/documentation/videos/sql-in-azure-scottgu/)。 由 Scott Guthrie 的 SQL 数据库 6 分钟视频介绍。
- [应用程序模式和 Azure 虚拟机中 SQL Server 的开发策略](https://msdn.microsoft.com/library/windowsazure/dn574746.aspx)。

在 ASP.NET Web 应用中使用实体框架和 SQL 数据库

- [开始使用 EF 6 使用 MVC 5](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 包含 9 个部分组成的系列教程将指导你完成生成的 MVC 应用程序，它使用 EF 并将数据库部署到 Azure 和 SQL 数据库。
- [使用 Visual Studio 的 ASP.NET Web 部署](../../../../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md)。 十二个部分组成的系列教程将进入有关如何将数据库部署通过使用 EF Code First 的更多深入分析。
- [使用成员资格、 OAuth 和 SQL 数据库的安全 ASP.NET MVC 5 应用部署到 Azure 网站](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)。 分步教程将指导你完成创建 web 应用使用身份验证、 成员资格数据库中存储应用程序表，修改数据库架构，并将应用部署到 Azure。
- [ASP.NET 数据访问内容映射](https://go.microsoft.com/fwlink/p/?LinkId=282414)。 如何使用 EF 和 SQL 数据库资源的链接。

在 Azure 上使用 MongoDB:

- [MongoLab-在 Azure 上的 MongoDB](http://msopentech.com/opentech-projects/mongolab-mongodb-on-windows-azure/)。 有关在 Azure 上运行 MongoDB 的文档的门户页。
- [创建 Azure 网站连接到 Azure 中的虚拟机上运行的 MongoDB](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-store-data-mongodb-vm/)。 分步教程演示如何在 ASP.NET web 应用程序中使用 MongoDB 数据库。

HDInsight (Hadoop 在 Azure 上):

- [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)。 门户上的 HDInsight 文档[Azure](https://azure.microsoft.com/)网站。
- [Hadoop 和 HDInsight:在 Azure 中的大数据](https://msdn.microsoft.com/magazine/dn385705.aspx)。 Bruno Terkaly 和 Ricardo Villalobos，引入了 Azure 上的 Hadoop 的 MSDN 杂志 》 一文。
- [Microsoft 模式和做法-Azure 指南](https://msdn.microsoft.com/library/dn568099.aspx)。 请参阅 MapReduce 模式。

> [!div class="step-by-step"]
> [上一页](single-sign-on.md)
> [下一页](data-partitioning-strategies.md)
