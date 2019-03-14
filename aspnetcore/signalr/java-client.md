---
title: ASP.NET Core SignalR Java 客户端
author: mikaelm12
description: 了解如何使用 ASP.NET Core SignalR Java 客户端。
monikerRange: '>= aspnetcore-2.2'
ms.author: mimengis
ms.custom: mvc
ms.date: 11/07/2018
uid: signalr/java-client
ms.openlocfilehash: d0eff38c1f622b896ed1dc3002238aec7b6bfd38
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57030064"
---
# <a name="aspnet-core-signalr-java-client"></a>ASP.NET Core SignalR Java 客户端

通过[Mikael Mengistu](https://twitter.com/MikaelM_12)

Java 客户端，包括 Android 应用程序的 Java 代码中连接到 ASP.NET Core SignalR 服务器。 像[JavaScript 客户端](xref:signalr/javascript-client)并[.NET 客户端](xref:signalr/dotnet-client)，Java 客户端，可接收并将消息发送到实时的中心。 Java 客户端是可在 ASP.NET Core 2.2 及更高版本。

在这篇文章中引用示例 Java 控制台应用程序使用 SignalR Java 客户端。

[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/signalr/java-client/sample)（[如何下载](xref:index#how-to-download-a-sample)）

## <a name="install-the-signalr-java-client-package"></a>SignalR Java 客户端程序包安装

*Signalr 1.0.0* JAR 文件允许客户端连接到 SignalR 集线器。 若要查找最新的 JAR 文件版本号，请参阅[Maven 搜索结果](https://search.maven.org/search?q=g:com.microsoft.signalr%20AND%20a:signalr)。

如果使用 Gradle，添加下面的代码行`dependencies`一部分您*build.gradle*文件：

```gradle
implementation 'com.microsoft.signalr:signalr:1.0.0'
```

如果使用 Maven，添加以下行`<dependencies>`的元素在*pom.xml*文件：

[!code-xml[pom.xml dependency element](java-client/sample/pom.xml?name=snippet_dependencyElement)]

## <a name="connect-to-a-hub"></a>连接到中心

若要建立`HubConnection`，则`HubConnectionBuilder`应使用。 生成连接时，可以配置中心 URL 和日志级别。 配置任何必需的选项，方法是调用的任何`HubConnectionBuilder`方法之前`build`。 启动与连接`start`。

[!code-java[Build hub connection](java-client/sample/src/main/java/Chat.java?range=16-17)]

## <a name="call-hub-methods-from-client"></a>从客户端调用集线器方法

调用`send`调用集线器方法。 将中心方法名称和到中心方法中定义的任何参数传递`send`。

[!code-java[send method](java-client/sample/src/main/java/Chat.java?range=28)]

## <a name="call-client-methods-from-hub"></a>从集线器调用客户端方法

使用`hubConnection.on`可以调用该集线器的客户端上定义的方法。 构建之后启动连接之前定义的方法。

[!code-java[Define client methods](java-client/sample/src/main/java/Chat.java?range=19-21)]

## <a name="add-logging"></a>添加日志记录

SignalR Java 客户端使用[SLF4J](https://www.slf4j.org/)用于日志记录库。 它是库的一个高级日志记录 API，允许通过将特定的日志记录依赖项中选择其自己特定的日志记录实现的用户。 下面的代码段演示如何使用`java.util.logging`的 SignalR Java 客户端。

```gradle
implementation 'org.slf4j:slf4j-jdk14:1.7.25'
```

如果没有配置依赖项中的日志记录，SLF4J 加载具有以下警告消息的默认无操作记录器：

```
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
```

这可以安全地忽略。

## <a name="android-development-notes"></a>Android 开发说明

与 SignalR 客户端功能的 Android SDK 兼容性时，请考虑以下各项指定你的目标 Android SDK 版本：

* SignalR Java 客户端将运行 Android API 级别 16 和更高版本。
* 通过 Azure SignalR 服务连接将需要 20 及更高版本的 Android API 级别因为[Azure SignalR 服务](/azure/azure-signalr/signalr-overview)需要 TLS 1.2，并且不支持基于 SHA-1 的密码套件。 Android[添加支持 SHA-256 （和更高版本） 的密码套件](https://developer.android.com/reference/javax/net/ssl/SSLSocket)API 20 级中。

## <a name="configure-bearer-token-authentication"></a>配置持有者令牌身份验证

在 SignalR Java 客户端，可配置的持有者令牌，用于通过提供"访问令牌工厂"进行身份验证，向[HttpHubConnectionBuilder](/java/api/com.microsoft.signalr._http_hub_connection_builder?view=aspnet-signalr-java)。 使用[withAccessTokenFactory](/java/api/com.microsoft.signalr._http_hub_connection_builder.withaccesstokenprovider?view=aspnet-signalr-java#com_microsoft_signalr__http_hub_connection_builder_withAccessTokenProvider_Single_String__)提供[RxJava](https://github.com/ReactiveX/RxJava) [单一<String>](http://reactivex.io/documentation/single.html)。 通过调用[Single.defer](http://reactivex.io/RxJava/javadoc/io/reactivex/Single.html#defer-java.util.concurrent.Callable-)，可以编写逻辑来为您的客户端生成访问令牌。

```java
HubConnection hubConnection = HubConnectionBuilder.create("YOUR HUB URL HERE")
    .withAccessTokenProvider(Single.defer(() -> {
        // Your logic here.
        return Single.just("An Access Token");
    })).build();
```

## <a name="known-limitations"></a>已知限制

* 支持仅 JSON 协议。
* 支持仅 Websocket 传输。
* 流式处理尚不支持。

## <a name="additional-resources"></a>其他资源

* [Java API 参考](/java/api/com.microsoft.signalr?view=aspnet-signalr-java)
* <xref:signalr/hubs>
* <xref:signalr/javascript-client>
* <xref:signalr/publish-to-azure-web-app>
