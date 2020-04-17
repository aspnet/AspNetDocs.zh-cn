---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: 配置和检测 |微软文档
author: rick-anderson
description: ASP.NET 2.0 中的配置和检测发生了重大变化。 新的ASP.NET配置 API 允许进行配置更改。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: 30ea2ffd3d055c5373a33615bc19a8f68fb568ab
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543049"
---
# <a name="configuration-and-instrumentation"></a>配置和检测

由[微软](https://github.com/microsoft)

> ASP.NET 2.0 中的配置和检测发生了重大变化。 新的ASP.NET配置 API 允许以编程方式进行配置更改。 此外，存在许多新的配置设置允许新的配置和检测。

ASP.NET 2.0 中的配置和检测发生了重大变化。 新的ASP.NET配置 API 允许以编程方式进行配置更改。 此外，存在许多新的配置设置允许新的配置和检测。

在本模块中，我们将讨论配置 API ASP.NET，因为它与读取和写入ASP.NET配置文件有关，我们还将讨论ASP.NET检测。 我们还将介绍ASP.NET跟踪中提供的新功能。

## <a name="aspnet-configuration-api"></a>ASP.NET 配置 API

ASP.NET配置 API 允许您使用单个编程接口开发、部署和管理应用程序配置数据。 您可以使用配置 API 以编程方式开发和修改完整的ASP.NET配置，而无需直接编辑配置文件中的 XML。 此外，您可以在开发的应用程序和脚本、基于 Web 的管理工具以及 Microsoft 管理控制台 （MMC） 管理单元中使用配置 API。

以下两个配置管理工具使用配置 API，并包含在 .NET 框架版本 2.0 中：

- mMC ASP.NET，它使用配置 API 简化管理任务，提供来自配置层次结构所有级别的本地配置数据的集成视图。
- 网站管理工具，允许您管理本地和远程应用程序的配置设置，包括托管站点。

ASP.NET配置 API 包含一组ASP.NET管理对象，可用于以编程方式配置网站和应用程序。 管理对象作为 .NET 框架类库实现。 配置 API 编程模型通过在编译时强制实施数据类型，有助于确保代码的一致性和可靠性。 为了更轻松地管理应用程序配置，配置 API 允许您将从配置层次结构中的所有点合并的数据视为单个集合，而不是将数据视为来自不同配置文件的单独集合。 此外，配置 API 使您能够操作整个应用程序配置，而无需直接编辑配置文件中的 XML。 最后，API 通过支持管理工具（如网站管理工具）来简化配置任务。 配置 API 通过支持在计算机上创建配置文件并在多台计算机上运行配置脚本来简化部署。

> [!NOTE]
> 配置 API 不支持创建 IIS 应用程序。

## <a name="working-with-local-and-remote-configuration-settings"></a>使用本地和远程配置设置

配置对象表示应用于特定物理实体（如计算机）或逻辑实体（如应用程序或网站）的配置设置的合并视图。 指定的逻辑实体可以存在于本地计算机或远程服务器上。 当指定实体不存在配置文件时，配置对象表示由计算机.config 文件定义的默认配置设置。

通过使用以下类中的一个打开的配置方法，可以获取配置对象：

1. 配置管理器 类（如果您的实体是客户端应用程序）。
2. Web 配置管理器 类（如果您的实体是 Web 应用程序）。

这些方法将返回一个配置对象，该对象反过来提供了处理基础配置文件所需的方法和属性。 您可以访问这些文件进行读取或写入。

### <a name="reading"></a>阅读

您可以使用 GetSection 或 GetSectionGroup 方法读取配置信息。 读取的用户或进程必须对层次结构中的所有配置文件具有读取权限。

> [!NOTE]
> 如果使用采用路径参数的静态 GetSection 方法，则路径参数必须引用运行代码的应用程序。 否则，将忽略该参数，并返回当前正在运行的应用程序的配置信息。

### <a name="writing"></a>写入

您可以使用 Save 方法之一来写入配置信息。 写入的用户或进程必须具有当前配置层次结构级别的配置文件和目录的写入权限，以及层次结构中所有配置文件的读取权限。

要生成表示指定实体继承的配置设置的配置文件，请使用以下保存配置方法之一：

1. 用于创建新配置文件的保存方法。
2. 保存 As 方法用于在另一个位置生成新的配置文件。

## <a name="configuration-classes-and-namespaces"></a>配置类和命名空间

许多配置类和方法彼此相似。 下表描述了最常用的配置类和命名空间。

| **配置类或命名空间** | **说明** |
| --- | --- |
| [系统.配置](https://msdn.microsoft.com/library/system.configuration.aspx)命名空间 | 包含所有 .NET 框架应用程序的主配置类。 节处理程序类用于从 GetSection 和 GetSectionGroup 等方法获取节的配置数据。 这两种方法是非静态的。 |
| 系统.配置.配置类 | 表示计算机、应用程序、Web 目录或其他资源的一组配置数据。 此类包含用于更新配置设置和获取对节和节组的引用的有用方法，如 GetSection 和 GetSectionGroup。 此类用作获取设计时配置数据的方法的返回类型，例如 Web 配置管理器和配置管理器 类的方法。 |
| 系统.Web.配置命名空间 | 包含ASP.NET[配置设置](https://msdn.microsoft.com/library/b5ysx397.aspx)中定义的ASP.NET配置部分的节处理程序类。 节处理程序类用于从 GetSection 和 GetSectionGroup 等方法获取节的配置数据。 |
| 系统.Web.配置.Web配置管理器类 | 提供了获取对运行时和设计时配置设置引用的有用方法。 这些方法使用 System.配置.配置类作为返回类型。 您可以使用此类的静态 GetSection 方法或系统的非静态 GetSection 方法。 对于 Web 应用程序配置，建议使用 System.Web.配置.Web 配置管理器 类而不是系统.配置.配置管理器类。 |
| [系统.配置.提供程序](https://msdn.microsoft.com/library/system.configuration.provider.aspx)命名空间 | 提供了一种自定义和扩展配置提供程序的方法。 这是配置系统中所有提供程序类的基类。 |
| [系统.Web.管理](https://msdn.microsoft.com/library/system.web.management.aspx)命名空间 | 包含用于管理和监视 Web 应用程序运行状况的类和接口。 严格地说，此命名空间不被视为配置 API 的一部分。 例如，跟踪和事件触发由此命名空间中的类完成。 |
| [系统.管理.检测](https://msdn.microsoft.com/library/system.management.instrumentation.aspx)命名空间 | 提供应用程序检测所需的类，以便通过 Windows 管理检测 （WMI） 向潜在使用者公开其管理信息和事件。 ASP.NET运行状况监视使用 WMI 传递事件。 严格地说，此命名空间不被视为配置 API 的一部分。 |

## <a name="reading-from-aspnet-configuration-files"></a>从ASP.NET配置文件读取

WebManagerManager 类是从ASP.NET配置文件读取的核心类。 读取ASP.NET配置文件基本上有三个步骤：

1. 使用 OpenWeb 配置方法获取配置对象。
2. 获取对配置文件中所需部分的引用。
3. 从配置文件中读取所需的信息。

配置对象表示不表示特定的配置文件。 相反，它表示计算机、应用程序或网站的配置的合并视图。 以下代码示例实例化表示名为*ProductInfo*的 Web 应用程序的配置的配置对象。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> 请注意，如果 /ProductInfo 路径不存在，上述代码将返回计算机中指定的默认配置。

获得配置对象后，可以使用 GetSection 或 GetSectionGroup 方法深入了解配置设置。 以下示例获取对上述 ProductInfo 应用程序的模拟设置的引用：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>写入ASP.NET配置文件

与从配置文件读取一样，WebManagerManager 类是写入Asp.NET配置文件的核心。 还有三个步骤要写入ASP.NET配置文件。

1. 使用 OpenWeb 配置方法获取配置对象。
2. 获取对配置文件中所需部分的引用。
3. 使用"保存"或"保存"方法从配置文件中写入所需的信息。

以下代码将编译&lt;&gt;元素的**调试**属性更改为 false：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

执行此代码时&lt;，webApp&gt;应用程序的*Web.config*文件编译元素的**调试**属性将设置为 false。

## <a name="systemwebmanagement-namespace"></a>系统.Web.管理命名空间

System.Web.管理命名空间提供用于管理和监视ASP.NET应用程序的运行状况的类和接口。

日志记录是通过定义将事件与提供程序关联的规则来完成的。 规则定义发送到提供程序的事件类型。 以下基本事件可供您记录：

| **WebBase事件** | 所有事件的基础事件类。 包含所有事件（如事件代码、事件详细信息代码、引发事件的日期和时间、序列号、事件消息和事件详细信息）所需的属性。 |
| --- | --- |
| **网络管理事件** | 管理事件的基本事件类，如应用程序生存期、请求、错误和审核事件。 |
| **网络检测事件** | 应用程序以固定间隔生成的事件，用于捕获有用的运行时状态信息。 |
| **网络审计事件** | 安全审核事件的基类，用于标记授权失败、解密失败*等条件。* |
| **Web请求事件** | 所有信息请求事件的基类。 |
| **WebBase错误事件** | 指示错误条件的所有事件的基类。 |

可用的提供程序类型允许您将事件输出发送到事件查看器、SQL 服务器、Windows 管理检测 （WMI） 和电子邮件。 预配置的提供程序和事件映射减少了记录事件输出所需的工作量。

ASP.NET 2.0 使用事件日志提供程序开箱即用，基于应用程序域启动和停止来记录事件，以及记录任何未处理的异常。 这有助于介绍一些基本方案。 例如，假设您的应用程序引发异常，但用户不保存错误，并且无法重现它。 使用默认事件日志规则，您将能够收集异常和堆栈信息，以便更好地了解发生了哪种错误。 如果应用程序正在失去会话状态，则应用另一个示例。 在这种情况下，您可以在事件日志中查看以确定应用程序域是否正在回收，以及应用程序域最初停止的原因。

此外，健康监测系统是可扩展的。 例如，可以定义自定义 Web 事件，在应用程序中触发这些事件，然后定义一条规则，将事件信息发送到提供程序（如电子邮件）。 这允许您轻松地将检测与运行状况监视提供程序绑定。 作为另一个示例，您可以在每次处理订单时触发事件，并设置将每个事件发送到 SQL Server 数据库的规则。 当用户连续多次无法登录时，还可以触发事件，并将事件设置为使用基于电子邮件的提供程序。

默认提供程序和事件的配置存储在全局 Web.config 文件中。 全局 Web.config 文件将存储在 Machine.config 文件中的所有基于 Web 的设置存储在 ASP.NET 1x 中。 全局 Web.config 文件位于以下目录中：

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

全局&lt;Web.config 文件的运行状况监视&gt;部分提供默认配置设置。 您可以通过在 Web.config 文件中为应用程序实现&lt;运行状况监视&gt;部分来覆盖这些设置或配置您自己的设置。

全局&lt;Web.config 文件的运行状况监视&gt;部分包含以下项：

| **供应商** | 包含为事件查看器、WMI 和 SQL 服务器设置的提供程序。 |
| --- | --- |
| **事件映射** | 包含各种 WebBase 类的映射。 如果生成自己的事件类，则可以扩展此列表。 生成自己的事件类可比向其发送信息的提供程序提供更精细的粒度。 例如，您可以将未处理的异常配置为发送到 SQL Server，同时将您自己的自定义事件发送到电子邮件。 |
| **规则** | 将事件映射链接到提供程序。 |
| **缓冲** | 与 SQL Server 和电子邮件提供程序一起使用，以确定将事件刷新到提供程序的频率。 |

下面是来自全局 Web.config 文件中的代码示例。

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>如何将事件存储到事件查看器

如前所述，在全局 Web.config 文件中为您配置了用于在事件查看器中记录事件提供程序。 默认情况下，记录基于**WebBaseErrorEvent**和**Web 失败审核事件的所有事件**。 您可以添加其他规则以将其他信息记录到事件日志。 例如，如果要记录所有事件（*即*基于**WebBaseEvent**的每个事件），可以向 Web.config 文件添加以下规则：

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

此规则会将 **"所有事件事件**"映射链接到事件日志提供程序。 事件映射和提供程序都包含在全局 Web.config 文件中。

## <a name="how-to-store-events-to-sql-server"></a>如何将事件存储到 SQL 服务器

此方法使用**ASPNETDB**数据库，该数据库由 Aspnet\_regsql.exe 工具生成。 默认提供程序使用 LocalSqlServer 连接字符串，该字符串使用应用\_数据文件夹中的基于文件的数据库或 SQL Server 的本地 SQLExpress 实例。 本地SqlServer连接字符串和 SqlProvider 都在全局 Web.config 文件中配置。

全局 Web.config 文件中的 LocalSqlServer 连接字符串如下所示：

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

如果要使用另一个 SQL Server 实例，则需要使用 Aspnet\_regsql.exe 工具，该工具可在 %windir%_Microsoft.Net_Framework_v2.0 中找到。\*文件夹。 使用 Aspnet\_regsql.exe 工具在 SQL Server 实例上生成自定义**ASPNETDB**数据库，然后将连接字符串添加到应用程序配置文件，然后使用新的连接字符串添加提供程序。 创建**ASPNETDB**数据库后，需要设置规则以将事件映射链接到 sqlProvider。

无论是使用默认 SqlProvider 还是配置自己的提供程序，都需要添加一条规则，将提供程序与事件映射链接。 以下规则将上面创建的新提供程序链接到 **"所有事件"** 事件映射。 此规则将基于**WebBaseEvent**记录所有事件，并将它们发送到将使用 MYASPNETDB 连接字符串的 MySqlWebEvent 提供程序。 以下代码添加了一条规则，用于将提供程序与事件映射链接：

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

如果只想向 SQL Server 发送错误，可以添加以下规则：

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>如何将事件转发到 WMI

您还可以将事件转发到 WMI。 默认情况下，WMI 提供程序在全局 Web.config 文件中为您配置。

以下代码示例添加一条规则以将事件转发到 WMI：

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

您需要添加一个规则来将事件映射关联到提供程序，以及一个 WMI 侦听器应用程序来侦听事件。 以下代码示例添加一条规则，将 WMI 提供程序链接到 **"所有事件"** 事件映射：

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>如何将事件转发到电子邮件

您还可以将事件转发给电子邮件。 请注意您映射到电子邮件提供商的事件规则，因为您可能会无意中向自己发送大量可能更适合 SQL Server 或事件日志的信息。 有两个电子邮件提供商;简单邮件Web事件提供商和模板邮件Web事件提供商。 每个属性具有相同的配置属性，但"模板"和"详细模板错误"属性除外，这两个属性仅在模板IdmailWebEvent提供程序上可用。

> [!NOTE]
> 这些电子邮件提供程序均未为您配置。 您需要将它们添加到 Web.config 文件中。

这两个电子邮件提供商之间的主要区别是 SimpleMailWebEventProvider 在无法修改的通用模板中发送电子邮件。 示例 Web.config 文件使用以下规则将此电子邮件提供程序添加到已配置提供程序列表中：

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

还会添加以下规则以将电子邮件提供程序绑定到 **"所有事件"** 事件映射：

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 跟踪

在 2.0 ASP.NET中，跟踪有三个主要增强功能。

1. 集成跟踪功能
2. 对跟踪消息的编程访问
3. 改进的应用程序级跟踪

## <a name="integrated-tracing-functionality"></a>集成跟踪功能

现在，您可以将 System.Diagnostics.Trace 类发出的消息路由到ASP.NET跟踪输出，并将ASP.NET跟踪发送的消息路由到 System.诊断.Trace。 您还可以将ASP.NET检测事件转发到 System.诊断.Trace。 此功能由&lt;跟踪&gt;元素的新**writeTo诊断跟踪**属性提供。 当此布尔值为 true 时，ASP.NET跟踪消息将转发到 System.诊断跟踪基础结构，供注册以显示 Trace 消息的任何侦听器使用。

## <a name="programmatic-access-to-trace-messages"></a>对跟踪消息的编程访问

ASP.NET 2.0 允许通过**TraceContextRecord**类和**跟踪记录**集合对所有跟踪消息进行编程访问。 访问跟踪消息的最有效方法是注册**TraceContextEventHandler**委托（ASP.NET 2.0 中也是新的）来处理新的**跟踪完成**事件。 然后，您可以根据需要循环访问跟踪消息。

以下代码示例说明了这一点：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

在上面的示例中，我循环浏览跟踪记录集合，然后将每条消息写入响应流。

## <a name="improved-application-level-tracing"></a>改进的应用程序级跟踪

通过引入&lt;跟踪&gt;元素的新**最新**属性，应用程序级跟踪得到了改进。 此属性指定是否显示最新的应用程序级跟踪输出，是否丢弃超出请求Limit 指示限制的较旧跟踪数据。 如果为 false，则在达到请求Limit 属性之前，将显示请求的跟踪数据。

## <a name="aspnet-command-line-tools"></a>ASP.NET命令行工具

有几个命令行工具可以帮助配置ASP.NET。 ASP.NET开发人员应该熟悉 aspnet\_regiis.exe 工具。 ASP.NET 2.0 提供了另外三个命令行工具，以帮助配置。

以下命令行工具可用：

| **工具** | **使用** |
| --- | --- |
| **阿斯普内\_雷吉斯.exe** | 允许在 IIS 注册ASP.NET。 此工具有两个版本附带 ASP.NET 2.0，一个用于 32 位系统（在 Framework 文件夹中），另一个用于 64 位系统（在 Framework64 文件夹中）。64 位版本将不会安装在 32 位操作系统上。 |
| **阿斯普内\_雷格斯** | ASP.NET SQL Server 注册工具用于创建 Microsoft SQL Server 数据库，供 ASP.NET 中的 SQL Server 提供程序使用，或从现有数据库中添加或删除选项。 Aspnet\_regsql.exe 文件位于 Web 服务器上的 [驱动器：]WINDOWS_Microsoft.NET_Framework_versionNumber 文件夹中。 |
| **阿斯普内\_注册浏览器.exe** | ASP.NET浏览器注册工具将所有系统范围的浏览器定义解析和编译到程序集中，并将程序集安装到全局程序集缓存中。 该工具使用浏览器定义文件 （。BROWSER 文件）来自 .NET 框架浏览器子目录。 该工具可以在 %SystemRoot%\Microsoft.NET_Framework_version_目录中找到。 |
| **阿斯普内\_编译器.exe** | ASP.NET编译工具使您能够编译ASP.NET Web 应用程序，无论是就位还是部署到目标位置（如生产服务器）。 就地编译有助于应用程序性能，因为最终用户在编译应用程序时不会遇到对应用程序的第一个请求的延迟。 |

由于 aspnet\_regiis.exe 工具对于 ASP.NET 2.0 并不新鲜，因此我们不会在此处讨论它。

## <a name="aspnet-sql-server-registration-tool---aspnet_regsqlexe"></a>ASP.NET SQL 服务器注册工具 -\_aspnet regsql.exe

您可以使用ASP.NET SQL 服务器注册工具设置多种类型的选项。 可以指定 SQL 连接，指定哪些ASP.NET应用程序服务使用 SQL Server 来管理信息，指示哪个数据库或表用于 SQL 缓存依赖项，以及添加或删除对使用 SQL Server 存储过程和会话状态的支持。

多个ASP.NET应用程序服务依赖于提供程序来管理从数据源存储和检索数据。 每个提供程序都特定于数据源。 ASP.NET包括用于以下ASP.NET功能的 SQL Server 提供程序：

- 成员资格[（Sqlsasprovider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)类）。
- 角色管理[（SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)类）。
- 配置文件[（SqlProfileProvider](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx)类）。
- Web 部件个性化[（Sql个性化提供程序](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx)类）。
- Web 事件[（SqlWebEvent 提供程序](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx)类）。

安装ASP.NET时，服务器的 Machine.config 文件包括配置元素，这些元素为依赖于提供程序的每个ASP.NET功能指定 SQL Server 提供程序。 默认情况下，这些提供程序配置为连接到 SQL Server Express 2005 的本地用户实例。 如果更改提供程序使用的默认连接字符串，则在使用计算机配置中配置的任何ASP.NET功能之前，必须使用 Aspnet\_regsql.exe 安装 SQL Server 数据库和所选功能的数据库元素。 如果使用 SQL 注册工具指定的数据库不存在（如果在命令行上未指定数据库，则 aspnetdb 将是默认数据库），则当前用户必须有权在 SQL Server 中创建数据库以及在数据库中创建架构元素。

### <a name="sql-cache-dependency"></a>SQL 缓存依赖项

ASP.NET输出缓存的高级功能是 SQL 缓存依赖项。 SQL 缓存依赖项支持两种不同的操作模式：一种是使用表轮询ASP.NET实现，另一种模式使用 SQL Server 2005 的查询通知功能。 SQL 注册工具可用于配置表轮询操作模式。

### <a name="session-state"></a>会话状态

默认情况下，会话状态值和信息存储在ASP.NET进程中的内存中。 或者，您可以将会话数据存储在 SQL Server 数据库中，其中会话数据可以由多个 Web 服务器共享。 如果使用 SQL 注册工具为会话状态指定的数据库不存在，则当前用户必须有权在 SQL Server 中创建数据库以及在数据库中创建架构元素。 如果数据库确实存在，则当前用户必须有权在现有数据库中创建架构元素。

要在 SQL Server 上安装会话状态数据库，请运行\_Aspnet regsql.exe 工具，并随命令提供以下信息：

- 使用 **-S**选项的 SQL Server 实例的名称。
- 具有在运行 SQL Server 的计算机上创建数据库的权限的帐户的登录凭据。 使用 **-E**选项使用当前登录的用户，或使用 **-U**选项指定用户 ID 以及 **-P**选项来指定密码。
- **-ssadd**命令行选项用于添加会话状态数据库。

默认情况下，不能使用 Aspnet\_regsql.exe 工具在运行 SQL Server 2005 Express 版的计算机上安装会话状态数据库。

### <a name="the-aspnet-browser-registration-tool---aspnet_regbrowsersexe"></a>ASP.NET浏览器注册工具 - 阿斯网\_注册浏览器.exe

在ASP.NET版本 1.1 中，Machine.config 文件包含&lt;一个&gt;称为浏览器Cap 的部分。 本节包含一系列 XML 条目，这些条目根据正则表达式定义了各种浏览器的配置。 对于ASP.NET版本 2.0，一个新的 。BROWSER 文件使用 XML 条目定义特定浏览器的参数。 通过添加新 的 浏览器，可以添加新 浏览器上的信息。BROWSER 文件到位于系统上 %SystemRoot%_Microsoft.NET_Framework_conFIG_浏览器的文件夹。

由于应用程序每次需要浏览器信息时都未读取 .config 文件，因此您可以创建新的 。BROWSER 文件和运行 Aspnet\_注册浏览器.exe 以向程序集添加所需的更改。 这允许服务器立即访问新的浏览器信息，因此您不必关闭任何应用程序来获取信息。 应用程序可以通过当前 HttpRequest 的浏览器属性访问浏览器功能。

运行 aspnet\_regbrowser.exe 时，以下选项可用：

| **选项** | **说明** |
| --- | --- |
| **-?** | 在命令窗口中显示\_Aspnet regb 浏览器.exe 帮助文本。 |
| **-i** | 创建运行时浏览器功能程序集并将其安装到全局程序集缓存中。 |
| **-u** | 从全局程序集缓存卸载运行时浏览器功能程序集。 |

## <a name="the-aspnet-compilation-tool---aspnet_compilerexe"></a>ASP.NET编译工具 - 阿斯普\_内编译器.exe

ASP.NET编译工具可通过两种常规方式使用：用于就地编译和编译以进行部署，其中指定了目标输出目录。

### <a name="compiling-an-application-in-place"></a>[编译就地的应用程序](https://msdn.microsoft.com/library/ms229863.aspx)

ASP.NET编译工具可以就地编译应用程序，即模仿对应用程序发出多个请求的行为，从而导致定期编译。 预编译网站的用户不会因为在第一次请求时编译页面而遇到延迟。

在就位预编译网站时，应用以下项：

- 该网站保留其文件和目录结构。
- 您必须具有服务器上站点使用的所有编程语言的编译器。
- 如果任何文件编译失败，则整个站点将失败编译。

在向应用程序添加新源文件后，还可以重新编译应用程序。 该工具仅编译新的或更改的文件，除非您包含 **-c**选项。

> [!NOTE]
> 包含嵌套应用程序的应用程序的编译不会编译嵌套应用程序。 嵌套应用程序必须单独编译。

### <a name="compiling-an-application-for-deployment"></a>[编译应用程序进行部署](https://msdn.microsoft.com/library/ms229863.aspx)

通过指定目标Dir参数，编译用于部署的应用程序（编译到目标位置）。 目标 Dir 可以是 Web 应用程序的最终位置，也可以进一步部署编译的应用程序。 使用 **-u**选项编译应用程序的方式，您可以更改编译应用程序中的某些文件，而无需重新编译它。 Aspnet\_编译器.exe 区分静态和动态文件类型，并在创建生成的应用程序时以不同的方式处理它们。

- 静态文件类型是那些没有关联的编译器或生成提供程序的文件，例如其命名具有扩展名的文件，如 .css、.gif、.htm、.html、.jpg、.js 等。 这些文件只是复制到目标位置，并保留其在目录结构中的相对位置。
- 动态文件类型是具有关联编译器或生成提供程序的文件，包括具有ASP.NET特定文件名扩展名的文件，如 .asax、.ascx、.ashx、.aspx、.browser、.master 等。 ASP.NET编译工具从这些文件生成程序集。 如果省略 **-u**选项，该工具还会创建文件名扩展名的文件。将原始源文件映射到其程序集的 COMPILE。 为了确保保留应用程序源的目录结构，该工具会在目标应用程序中的相应位置生成占位符文件。

您必须使用 **-u**选项来指示可以修改已编译应用程序的内容。 否则，后续修改将被忽略或导致运行时错误。

下表描述了在包含 **-u**选项时，ASP.NET编译工具如何处理不同的文件类型。

| **文件类型** | **编译器操作** |
| --- | --- |
| .ascx， .aspx， .master | 这些文件被拆分为标记和源代码，其中包括代码背后的文件和包含在脚本 runat_"server"&lt;&gt;元素中的任何代码。 源代码被编译成程序集，名称派生自哈希算法，并且程序集放置在 Bin 目录中。 任何内联代码，即包含在 括号**&lt;** 和**%** 括号之间的代码，都包含在标记中，并且未编译。 创建与源文件同名的新文件以包含标记并放置在相应的输出目录中。 |
| .ashx， .asmx | 这些文件不会编译，并且会移动到输出目录，以现在和未编译。 如果希望编译处理程序代码，请将代码放入 App\_Code 目录中的源代码文件中。 |
| .cs， .vb， .jsl， .cpp （不包括前面列出的文件类型的代码后文件） | 这些文件被编译并作为引用它们的程序集中的资源包含在其中。 源文件不会复制到输出目录。 如果未引用代码文件，则不编译它。 |
| 自定义文件类型 | 这些文件未编译。 这些文件将复制到相应的输出目录。 |
| 应用\_代码子目录中的源代码文件 | 这些文件被编译成程序集并放置在 Bin 目录中。 |
| .resx 和 .资源文件在\_应用全局资源子目录中 | 这些文件被编译成程序集并放置在 Bin 目录中。 在主\_输出目录下不创建应用全局资源子目录，并且源目录中的 .resx 或 .resource 文件不会复制到输出目录。 |
| .resx 和 .资源文件在\_应用本地资源子目录中 | 这些文件不会编译，并复制到相应的输出目录。 |
| 应用\_主题子目录中的 .skin 文件 | .skin 文件和静态主题文件不会编译，并复制到相应的输出目录。 |
| .browser Web.config 静态文件类型 程序集已存在于 Bin 目录中 | 这些文件将像一样复制到输出目录。 |

下表描述了在省略 **-u**选项时，ASP.NET编译工具如何处理不同的文件类型。

| **文件类型** | **编译器操作** |
| --- | --- |
| .aspx， .asmx， .ashx， .master | 这些文件被拆分为标记和源代码，其中包括代码背后的文件和包含在脚本 runat_"server"&lt;&gt;元素中的任何代码。 源代码被编译成程序集，名称派生自哈希算法。 生成的程序集放置在 Bin 目录中。 任何内联代码，即包含在 括号**&lt;** 和**%** 括号之间的代码，都包含在标记中，并且未编译。 编译器创建新文件以包含与源文件同名的标记。 这些生成的文件放置在 Bin 目录中。 编译器还创建与源文件同名但具有扩展名的文件。包含映射信息的 COMPILED。 .COMPILED 文件放置在与源文件的原始位置对应的输出目录中。 |
| .ascx | 这些文件被拆分为标记和源代码。 源代码被编译成程序集并放置在 Bin 目录中，名称派生自哈希算法。 不生成标记文件。 |
| .cs， .vb， .jsl， .cpp （不包括前面列出的文件类型的代码后文件） | 由 .ascx、.ashx 或 .aspx 文件生成的程序集引用的源代码被编译到程序集中并放置在 Bin 目录中。 不会复制任何源文件。 |
| 自定义文件类型 | 这些文件像动态文件一样编译。 根据它们所基于的文件类型，编译器可以将映射文件放置在输出目录中。 |
| 应用\_代码子目录中的文件 | 此子目录中的源代码文件被编译到程序集中并放置在 Bin 目录中。 |
| 应用\_全局资源子目录中的文件 | 这些文件被编译成程序集并放置在 Bin 目录中。 在主\_输出目录下不创建应用全局资源子目录。 如果配置文件指定应用于"全部"，则 .resx 和 .resources 文件将复制到输出目录。 如果[生成提供程序](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx)引用它们，则不复制它们。 |
| .resx 和 .资源文件在\_应用本地资源子目录中 | 这些文件被编译到具有唯一名称的程序集中，并放置在 Bin 目录中。 没有 .resx 或 .resource 文件复制到输出目录。 |
| 应用\_主题子目录中的 .skin 文件 | 主题被编译到程序集中并放置在 Bin 目录中。 为 .skin 文件创建存根文件，并放置在相应的输出目录中。 静态文件（如 .css）将复制到输出目录。 |
| .browser Web.config 静态文件类型 程序集已存在于 Bin 目录中 | 这些文件将照样复制到输出目录。 |

### <a name="fixed-assembly-names"></a>[固定程序集名称](https://msdn.microsoft.com/library/ms229863.aspx##)

某些方案（如使用 MSI Windows 安装程序部署 Web 应用程序）需要使用一致的文件名和内容，以及一致的目录结构来标识更新的程序集或配置设置。 在这些情况下，可以使用 **-固定名称**选项指定ASP.NET编译工具应为每个源文件编译程序集，而不是使用将多个页面编译到程序集中的位置。 这可能导致大量程序集，因此，如果您担心可伸缩性，则应谨慎使用此选项。

### <a name="strong-name-compilation"></a>[强名称编译](https://msdn.microsoft.com/library/ms229863.aspx##)

\_提供 -aptca、-delaysign、-**键容器**和 **-键文件**选项，以便您可以使用 Aspnet 编译器.exe 创建强命名程序集，而无需单独使用[强名称工具 （Sn.exe）。](https://msdn.microsoft.com/library/k5b5tt23.aspx) **-aptca** **-delaysign** 这些选项分别对应于**允许部分受信任的调用方属性**、**程序集延迟属性**、**程序集 KeyName 属性**和**程序集密钥文件属性**。

讨论这些属性超出了本课程的范围。

## <a name="labs"></a>实验室

以下每个实验室都基于以前的实验室。 你需要按顺序做它们。

## <a name="lab-1-using-the-configuration-api"></a>实验 1：使用配置 API

1. 创建一个名为*mod9lab*的新网站。
2. 向站点添加新的 Web 配置文件。
3. 将以下内容添加到 Web.config 文件：

[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

这将确保您具有保存对 Web.config 文件更改的权限。

1. 将新的 Label 控件添加到 Default.aspx 并将 ID 更改为**lblDebugStatus。**
2. 将新的按钮控件添加到 Default.aspx。
3. 将按钮控件的 ID 更改为**btnToggleDebug**和"文本"以**切换调试状态**。
4. 打开 Default.aspx 的代码背后文件的代码视图，并为**System.Web.配置**添加**using**语句，如下所示：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. 向类添加两个私有变量和一个\_Page Init 方法，如下所示：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. 将以下代码添加到页面\_加载：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. 保存和浏览默认值.aspx。 请注意，"标签"控件显示当前调试状态。
2. 双击设计器中的"按钮"控件，并将以下代码添加到 Button 控件的 Click 事件：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. 保存并浏览默认.aspx，然后单击该按钮。
2. 单击每个按钮后打开 Web.config 文件，并**debug**观察&lt;编译&gt;部分中的调试属性。

## <a name="lab-2-logging-application-restarts"></a>实验 2：记录应用程序重新启动

在本实验中，您将创建代码，以允许您在事件查看器中切换应用程序关闭、启动和重新编译的日志记录。

1. 将下拉列表添加到默认.aspx，并将 ID 更改为 ddlLogApp事件。
2. 将下拉列表的**自动 PostBack**属性设置为**true**。
3. 将三个项目添加到下拉列表的"项目"集合中。 使第一个项目**的文本***选择值*和值 -1。 使第二个项目**的文本**和**值**为**true，** 并使第三项**的文本**和**值****为 false**。
4. 将新标签添加到默认.aspx。 将 ID 更改为**lblLogApp事件**。
5. 打开 default.aspx 的代码后面视图，并为类型为 Health 监视节的变量添加新声明，如下所示：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. 将以下代码添加到页\_Init 中的现有代码：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. 双击下拉列表，并将以下代码添加到"选定索引更改"事件：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. 浏览默认值.aspx。
2. 将下拉设置为**False**。
3. 清除事件查看器中的应用程序日志。
4. 单击该按钮可更改应用程序的调试属性。
5. 刷新事件查看器中的应用程序日志。 

    1. 是否有任何事件被记录？
    2. 为什么或为什么不？
6. 将下拉列表设置为 **"True"。**
7. 单击该按钮可切换应用程序的调试属性。
8. 刷新应用程序登录事件查看器。 

    1. 是否有任何事件被记录？
    2. 应用关闭的原因是什么？
9. 尝试打开和关闭日志记录，并查看对 Web.config 文件所做的更改。

## <a name="more-information"></a>详细信息：

ASP.NET 2.0 的提供程序模型允许您不仅为应用程序检测创建自己的提供程序，还可用于许多其他用途，如成员资格、配置文件等。有关编写自定义提供程序将应用程序事件记录到文本文件的详细信息，请访问[此链接](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp)。
