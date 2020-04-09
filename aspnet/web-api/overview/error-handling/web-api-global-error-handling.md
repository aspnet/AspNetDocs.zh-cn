---
uid: web-api/overview/error-handling/web-api-global-error-handling
title: ASP.NET Web API 2 中的全局错误处理 - ASP.NET 4.x
author: davidmatson
description: ASP.NET 4.x ASP.NET Web API 2 中的全局错误处理概述。
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: bffd7863-f63b-4b23-a13c-372b5492e9fb
msc.legacyurl: /web-api/overview/error-handling/web-api-global-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 5ff54d2e4ed881ce927d0a401fb79d9b8bc5b8a1
ms.sourcegitcommit: ce28244209db8615bc9bdd576a2e2c88174d318d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80675419"
---
# <a name="global-error-handling-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的全局错误处理

由[大卫·马特森](https://github.com/davidmatson)，[里克·安德森](https://twitter.com/RickAndMSFT)

本主题概述了ASP.NET web API 2 中针对ASP.NET 4.x 的全局错误处理。 如今，Web API 中没有简单的方法来全局记录或处理错误。 某些未处理的异常可以通过[异常筛选器](exception-handling.md)进行处理，但有许多异常筛选器无法处理的情况。 例如：

1. 从控制器构造函数引发的异常。
2. 从消息处理程序引发的异常。
3. 在路由过程中引发的异常。
4. 在响应内容序列化期间引发的异常。

我们希望提供一种简单、一致的方式来记录和处理这些异常（如果可能）。 

处理异常有两个主要情况，即我们能够发送错误响应的情况，以及我们所能做的就是记录异常的情况。 后一种情况的一个示例是在流式响应内容中间引发异常时;在流式响应内容中引发异常时，则为后一种情况。在这种情况下，发送新的响应消息为时已晚，因为状态代码、标头和部分内容已经通过导线，因此我们只需中止连接即可。 即使无法处理异常以生成新的响应消息，我们仍支持记录异常。 在可以检测到错误的情况下，我们可以返回适当的错误响应，如下所示：

[!code-csharp[Main](web-api-global-error-handling/samples/sample1.cs?highlight=6)]

### <a name="existing-options"></a>现有选项

除了[异常筛选器](exception-handling.md)之外，[消息处理程序](../advanced/http-message-handlers.md)今天还可用于观察所有 500 级响应，但对这些响应进行操作很困难，因为它们缺少有关原始错误的上下文。 消息处理程序也有一些与异常筛选器相同的限制，涉及它们可以处理的情况。 虽然 Web API 确实具有捕获错误条件的跟踪基础结构，但跟踪基础结构用于诊断目的，并且不适合在生产环境中运行。 全局异常处理和日志记录应该是可在生产期间运行并插入现有监视解决方案（例如[ELMAH）](https://code.google.com/p/elmah/)的服务。

### <a name="solution-overview"></a>解决方案概述

 我们提供两种新的用户可替换服务[，IexceptionLogger](../releases/whats-new-in-aspnet-web-api-21.md)和 IexceptionHandler，用于记录和处理未处理的异常。 服务非常相似，主要有两个区别：

1. 我们支持注册多个异常记录器，但仅支持单个异常处理程序。
2. 异常记录器总是被调用，即使我们即将中止连接。 只有在我们仍可以选择要发送的响应消息时，才会调用异常处理程序。

这两个服务都提供从检测到异常点包含相关信息的异常上下文的访问，特别是[HttpRequestMessage、HttpRequestContext、](https://msdn.microsoft.com/library/system.web.http.controllers.httprequestcontext(v=vs.118).aspx)引发异常和异常源（详情见下文）。 [HttpRequestMessage](https://msdn.microsoft.com/library/system.net.http.httprequestmessage(v=vs.110).aspx)

### <a name="design-principles"></a>设计原理

1. **无重大更改**由于此功能是在次要版本中添加的，因此影响解决方案的一个重要约束是，对于类型协定或行为，没有重大更改。 此约束排除了我们希望在现有 catch 块方面进行的一些清理，将异常转换为 500 个响应。 对于后续的主要版本，我们可以考虑此附加清理。 如果这对你很重要，请[ASP.NETWeb API用户语音](http://aspnet.uservoice.com/forums/147201-asp-net-web-api/suggestions/5451321-add-flag-to-enable-iexceptionlogger-and-iexception)投。
2. **与 Web API 构造保持一致性**Web API 的筛选器管道是处理跨领域问题的绝佳方法，它可灵活地将逻辑应用于特定于操作、特定于控制器或全局的范围。 筛选器（包括异常筛选器）始终具有操作和控制器上下文，即使在全局作用域中注册也是如此。 该协定对筛选器有意义，但它意味着异常筛选器（即使是全局范围筛选器）不适合某些异常处理情况，例如消息处理程序的异常，其中不存在操作或控制器上下文。 如果我们想要使用筛选器提供的灵活范围来处理异常处理，我们仍然需要异常筛选器。 但是，如果需要在控制器上下文之外处理异常，我们还需要一个单独的构造来进行完整的全局错误处理（没有控制器上下文和操作上下文约束）。

### <a name="when-to-use"></a>何时使用

- 异常记录器是查看 Web API 捕获的所有未处理异常的解决方案。
- 异常处理程序是自定义 Web API 捕获的未处理异常的所有可能响应的解决方案。
- 异常筛选器是处理与特定操作或控制器相关的子集未处理异常的最简单解决方案。

### <a name="service-details"></a>服务详细信息

 异常记录器和处理程序服务接口是采用相应上下文的简单异步方法： 

[!code-csharp[Main](web-api-global-error-handling/samples/sample2.cs)]

 我们还为这两个接口提供基类。 重写核心（同步或异步）方法是在建议的时间记录或处理所需的全部方法。 对于日志记录，`ExceptionLogger`基类将确保每个异常只调用一次核心日志记录方法（即使它稍后在调用堆栈上传播并进一步传播并再次捕获）。 基`ExceptionHandler`类将仅针对调用堆栈顶部的异常调用核心处理方法，而忽略旧嵌套 catch 块。 （这些基类的简化版本见下面的附录。和`IExceptionLogger``IExceptionHandler`都通过 接收有关异常的信息`ExceptionContext`。

[!code-csharp[Main](web-api-global-error-handling/samples/sample3.cs)]

当框架调用异常记录器或异常处理程序时，它将始终提供 和`Exception`。 `Request` 除了单元测试外，它还会始终提供 。 `RequestContext` 它很少提供 和`ControllerContext``ActionContext`（仅在从异常筛选器的 catch 块调用时）。 它很少提供 （`Response`仅在某些 IIS 情况下，当尝试编写响应时）。 请注意，由于其中一些属性可能`null`由使用者在访问异常类的成员`null`之前进行检查。`CatchBlock` 是指示哪个 catch 块看到异常的字符串。 catch 块字符串如下所示：

- HttpServer（发送同步方法）
- HttpController调度程序（发送同步方法）
- HttpBatchhandler（发送同步方法）
- IExceptionFilter（ApiController 在 ExecuteAsync 中处理异常筛选器管道）
- OWIN 主机：

    - HttpMessageHandlerAdapter.缓冲区响应内容同步（用于缓冲输出）
    - HttpMessageHandlerAdapter.复制响应内容同步（用于流式处理输出）
- 网络主机：

    - HttpControllerHandler.写入缓冲响应内容同步（用于缓冲输出）
    - HttpControllerHandler.写入流式响应内容同步（用于流式处理输出）
    - HttpControllerHandler.写入错误响应内容同步（对于缓冲输出模式下错误恢复失败）

catch 块字符串的列表也可通过静态只读属性提供。 （核心 catch 块字符串位于静态异常捕获块上;其余字符串出现在一个静态类中，每个静态类用于 OWIN 和 Web 主机）。`IsTopLevelCatchBlock` 有助于遵循仅在调用堆栈顶部处理异常的建议模式。 异常处理程序可以允许异常传播到主机即将看到之前，而不是将异常转换为 500 个响应。

除了 ，`ExceptionContext`记录器通过完整`ExceptionLoggerContext`获取了一条信息：

[!code-csharp[Main](web-api-global-error-handling/samples/sample4.cs)]

第二个属性`CanBeHandled`允许记录器标识无法处理的异常。 当连接即将中止，并且无法发送新的响应消息时，将调用记录器，但不会调用处理程序，并且记录器可以从此属性标识此方案***not***。

在 除`ExceptionContext`中，处理程序还可以获取一个可以设置在 full`ExceptionHandlerContext`上处理异常的属性：

[!code-csharp[Main](web-api-global-error-handling/samples/sample5.cs)]

`Result`异常处理程序通过将属性设置为操作结果（例如，[异常结果](https://msdn.microsoft.com/library/system.web.http.results.exceptionresult(v=vs.118).aspx)、[内部服务器错误结果](https://msdn.microsoft.com/library/system.web.http.results.internalservererrorresult(v=vs.118).aspx)、[状态代码结果](https://msdn.microsoft.com/library/system.web.http.results.statuscoderesult(v=vs.118).aspx)或自定义结果）来指示它已处理异常。 如果`Result`属性为 null，则异常将未处理，并且将重新引发原始异常。

对于调用堆栈顶部的异常，我们采取了额外的步骤，以确保响应适合 API 调用方。 如果异常传播到主机，调用方将看到死亡黄色屏幕或其他一些主机提供的响应，这些响应通常是 HTML，通常不是适当的 API 错误响应。 在这些情况下，结果开始为非空，只有当自定义异常处理程序显式将其设置回`null`（未处理）时，异常才会传播到主机。 在这种情况下`Result`，`null`设置为 可用于以下两种情况：

1. OWIN 托管 Web API，具有在 Web API 之前/外部注册的自定义异常处理中间件。
2. 通过浏览器进行本地调试，其中死亡黄色屏幕实际上是对未处理异常的有用响应。

对于异常记录器和异常处理程序，如果记录器或处理程序本身引发异常，则不执行任何恢复操作。 （除了让异常传播外，如果您有更好的方法，请将反馈保留在此页面的底部。异常记录器和处理程序的协定是，它们不应让异常传播到其调用方;否则，异常将只传播到主机，导致 HTML 错误（如 ASP）。NET 的黄色屏幕）被发送回客户端（对于希望 JSON 或 XML 的 API 调用方来说，这通常不是首选选项）。

## <a name="examples"></a>示例

### <a name="tracing-exception-logger"></a>跟踪异常记录器

下面的异常记录器将异常数据发送到配置的跟踪源（包括 Visual Studio 中的调试输出窗口）。

[!code-csharp[Main](web-api-global-error-handling/samples/sample6.cs)]

### <a name="custom-error-message-exception-handler"></a>自定义错误消息异常处理程序

下面的异常处理程序生成对客户端的自定义错误响应，包括用于联系支持的电子邮件地址。

[!code-csharp[Main](web-api-global-error-handling/samples/sample7.cs)]

## <a name="registering-exception-filters"></a>注册异常筛选器

如果使用"ASP.NET MVC 4 Web 应用程序"项目模板创建项目，请将 Web API 配置代码`WebApiConfig`放入类中，放入*App_Start*文件夹中：

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

## <a name="appendix-base-class-details"></a>附录：基本课程详细信息

[!code-csharp[Main](web-api-global-error-handling/samples/sample8.cs)]
