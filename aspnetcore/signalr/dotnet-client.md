---
title: ASP.NET Core SignalR.NET 客户端
author: bradygaster
description: 有关 ASP.NET Core SignalR.NET 客户端信息
monikerRange: '>= aspnetcore-2.1'
ms.author: bradyg
ms.custom: mvc
ms.date: 09/10/2018
uid: signalr/dotnet-client
ms.openlocfilehash: 25b618f7a424b217c0fb55417754ea358280b95a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034714"
---
# <a name="aspnet-core-signalr-net-client"></a>ASP.NET Core SignalR.NET 客户端

ASP.NET Core SignalR.NET 客户端库可让你与 SignalR 集线器从.NET 应用程序进行通信。

> [!NOTE]
> Xamarin 有特殊要求 Visual Studio 版本。 有关详细信息，请参阅[在 Xamarin 中的 SignalR 客户端 2.1.1](https://github.com/aspnet/Announcements/issues/305)。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/dotnet-client/sample)（[如何下载](xref:index#how-to-download-a-sample)）

这篇文章中的代码示例是使用 ASP.NET Core SignalR.NET 客户端的 WPF 应用。

## <a name="install-the-signalr-net-client-package"></a>安装 SignalR.NET 客户端包

`Microsoft.AspNetCore.SignalR.Client`包所需的.NET 客户端连接到 SignalR 集线器。 若要安装客户端库，请运行以下命令**程序包管理器控制台**窗口：

```powershell
Install-Package Microsoft.AspNetCore.SignalR.Client
```

## <a name="connect-to-a-hub"></a>连接到中心

若要建立连接，创建`HubConnectionBuilder`，并调用`Build`。 生成一个连接时，可以配置中心 URL、 协议、 传输类型、 日志级别、 标头，和其他选项。 配置任何必需的选项的方法是插入的任何`HubConnectionBuilder`方法转换`Build`。 启动与连接`StartAsync`。

[!code-csharp[Build hub connection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_MainWindowClass&highlight=15-17,39)]

## <a name="handle-lost-connection"></a>已断开连接的句柄

使用<xref:Microsoft.AspNetCore.SignalR.Client.HubConnection.Closed>事件响应丢失连接。 例如，你可能想要自动执行重新连接。

`Closed`事件需要返回的委托`Task`，它允许异步代码运行，而不使用`async void`。 若要满足中的委托签名`Closed`运行以同步方式，返回的事件处理程序`Task.CompletedTask`:

```csharp
connection.Closed += (error) => {
    // Do your close logic.
    return Task.CompletedTask;
};
```

异步支持的主要原因是使您可以重新启动连接。 正在启动的连接是一个异步操作。

在`Closed`处理程序重新启动该连接，请考虑等待某些随机延迟，以防止服务器，重载，如下面的示例中所示：

[!code-csharp[Use Closed event handler to automate reconnection](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ClosedRestart)]

## <a name="call-hub-methods-from-client"></a>从客户端调用集线器方法

`InvokeAsync` 在该中心将调用方法。 将中心方法名称和到中心方法中定义的任何参数传递`InvokeAsync`。 SignalR 是异步的因此请使用`async`和`await`时进行调用。

[!code-csharp[InvokeAsync method](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_InvokeAsync)]

## <a name="call-client-methods-from-hub"></a>从集线器调用客户端方法

定义使用集线器调用的方法`connection.On`之后生成，但之前启动连接。

[!code-csharp[Define client methods](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ConnectionOn)]

在前面的代码`connection.On`运行时服务器端代码将调用它使用`SendAsync`方法。

[!code-csharp[Call client method](dotnet-client/sample/signalrchat/hubs/chathub.cs?name=snippet_SendMessage)]

## <a name="error-handling-and-logging"></a>错误处理和日志记录

处理 try catch 语句的错误。 检查`Exception`对象，以确定要执行后发生错误的适当操作。

[!code-csharp[Logging](dotnet-client/sample/signalrchatclient/MainWindow.xaml.cs?name=snippet_ErrorHandling)]

## <a name="additional-resources"></a>其他资源

* [中心](xref:signalr/hubs)
* [JavaScript 客户端](xref:signalr/javascript-client)
* [发布到 Azure](xref:signalr/publish-to-azure-web-app)
