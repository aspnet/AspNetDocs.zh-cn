---
title: ASP.NET Core SignalR 入门
author: bradygaster
description: 在本教程中，创建使用 ASP.NET Core SignalR 的聊天应用。
ms.author: bradyg
ms.custom: mvc
ms.date: 11/30/2018
uid: tutorials/signalr
ms.openlocfilehash: 53ec924c2d7b4fac227be0c0bf24d93476528167
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029024"
---
# <a name="tutorial-get-started-with-aspnet-core-signalr"></a><span data-ttu-id="90b2e-103">教程：ASP.NET Core SignalR 入门</span><span class="sxs-lookup"><span data-stu-id="90b2e-103">Tutorial: Get started with ASP.NET Core SignalR</span></span>

<span data-ttu-id="90b2e-104">本教程介绍生成使用 SignalR 的实时应用的基础知识。</span><span class="sxs-lookup"><span data-stu-id="90b2e-104">This tutorial teaches the basics of building a real-time app using SignalR.</span></span> <span data-ttu-id="90b2e-105">您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="90b2e-105">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="90b2e-106">创建 Web 项目。</span><span class="sxs-lookup"><span data-stu-id="90b2e-106">Create a web project.</span></span>
> * <span data-ttu-id="90b2e-107">添加 SignalR 客户端库。</span><span class="sxs-lookup"><span data-stu-id="90b2e-107">Add the SignalR client library.</span></span>
> * <span data-ttu-id="90b2e-108">创建 SignalR 中心。</span><span class="sxs-lookup"><span data-stu-id="90b2e-108">Create a SignalR hub.</span></span>
> * <span data-ttu-id="90b2e-109">配置项目以使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="90b2e-109">Configure the project to use SignalR.</span></span>
> * <span data-ttu-id="90b2e-110">添加可将消息从任何客户端发送到所有连接客户端的代码。</span><span class="sxs-lookup"><span data-stu-id="90b2e-110">Add code that sends messages from any client to all connected clients.</span></span>

<span data-ttu-id="90b2e-111">最终将创建一个正常运行的聊天应用：</span><span class="sxs-lookup"><span data-stu-id="90b2e-111">At the end, you'll have a working chat app:</span></span>

![SignalR 示例应用](signalr/_static/signalr-get-started-finished.png)

<span data-ttu-id="90b2e-113">[查看或下载示例代码](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample)（[如何下载](xref:index#how-to-download-a-sample)）。</span><span class="sxs-lookup"><span data-stu-id="90b2e-113">[View or download sample code](https://github.com/aspnet/Docs/tree/master/aspnetcore/tutorials/signalr/sample) ([how to download](xref:index#how-to-download-a-sample)).</span></span>

[!INCLUDE [|Prerequisites](~/includes/net-core-prereqs-all-2.2.md)]

## <a name="create-a-web-project"></a><span data-ttu-id="90b2e-114">创建 Web 项目</span><span class="sxs-lookup"><span data-stu-id="90b2e-114">Create a web project</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="90b2e-115">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90b2e-115">Visual Studio</span></span>](#tab/visual-studio/)

* <span data-ttu-id="90b2e-116">从菜单中选择“文件”>“新建项目”。</span><span class="sxs-lookup"><span data-stu-id="90b2e-116">From the menu, select **File > New Project**.</span></span>

* <span data-ttu-id="90b2e-117">在“新建项目”对话框中，选择“已安装”>“Visual C#”>“Web”>“ASP.NET Core Web 应用”。</span><span class="sxs-lookup"><span data-stu-id="90b2e-117">In the **New Project** dialog, select **Installed > Visual C# > Web > ASP.NET Core Web Application**.</span></span> <span data-ttu-id="90b2e-118">将项目命名为“SignalRChat”。</span><span class="sxs-lookup"><span data-stu-id="90b2e-118">Name the project *SignalRChat*.</span></span>

  ![Visual Studio 中的“新建项目”对话框](signalr/_static/signalr-new-project-dialog.png)

* <span data-ttu-id="90b2e-120">选择“Web 应用”，以创建使用 Razor Pages 的项目。</span><span class="sxs-lookup"><span data-stu-id="90b2e-120">Select **Web Application** to create a project that uses Razor Pages.</span></span>

* <span data-ttu-id="90b2e-121">选择“.NET Core”目标框架，选择“ASP.NET Core 2.2”，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="90b2e-121">Select a target framework of **.NET Core**, select **ASP.NET Core 2.2**, and click **OK**.</span></span>

  ![Visual Studio 中的“新建项目”对话框](signalr/_static/signalr-new-project-choose-type.png)

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="90b2e-123">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="90b2e-123">Visual Studio Code</span></span>](#tab/visual-studio-code/)

* <span data-ttu-id="90b2e-124">在将要在其中创建新项目文件夹的文件夹中打开[集成终端](https://code.visualstudio.com/docs/editor/integrated-terminal)。</span><span class="sxs-lookup"><span data-stu-id="90b2e-124">Open the [integrated terminal](https://code.visualstudio.com/docs/editor/integrated-terminal) to the folder in which the new project folder will be created.</span></span>

* <span data-ttu-id="90b2e-125">运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="90b2e-125">Run the following commands:</span></span>

   ```console
   dotnet new webapp -o SignalRChat
   code -r SignalRChat
   ```

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="90b2e-126">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="90b2e-126">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="90b2e-127">从菜单中选择“文件”>“新建解决方案”。</span><span class="sxs-lookup"><span data-stu-id="90b2e-127">From the menu, select **File > New Solution**.</span></span>

* <span data-ttu-id="90b2e-128">选择“.NET Core”>“应用”>“ASP.NET Core Web 应用”（请勿选择 ASP.NET Core Web 应用 (MVC)）。</span><span class="sxs-lookup"><span data-stu-id="90b2e-128">Select **.NET Core > App > ASP.NET Core Web App** (Don't select **ASP.NET Core Web App (MVC)**).</span></span>

* <span data-ttu-id="90b2e-129">选择“下一步”。</span><span class="sxs-lookup"><span data-stu-id="90b2e-129">Select **Next**.</span></span>

* <span data-ttu-id="90b2e-130">将项目命名为“SignalRChat”，然后选择“创建”。</span><span class="sxs-lookup"><span data-stu-id="90b2e-130">Name the project *SignalRChat*, and then select **Create**.</span></span>

---

## <a name="add-the-signalr-client-library"></a><span data-ttu-id="90b2e-131">添加 SignalR 客户端库</span><span class="sxs-lookup"><span data-stu-id="90b2e-131">Add the SignalR client library</span></span>

<span data-ttu-id="90b2e-132">`Microsoft.AspNetCore.App` 元包中包括 SignalR 服务器库。</span><span class="sxs-lookup"><span data-stu-id="90b2e-132">The SignalR server library is included in the `Microsoft.AspNetCore.App` metapackage.</span></span> <span data-ttu-id="90b2e-133">JavaScript 客户端库不会自动包含在项目中。</span><span class="sxs-lookup"><span data-stu-id="90b2e-133">The JavaScript client library isn't automatically included in the project.</span></span> <span data-ttu-id="90b2e-134">对于此教程，使用库管理器 (LibMan) 从 unpkg 获取客户端库。</span><span class="sxs-lookup"><span data-stu-id="90b2e-134">For this tutorial, you use Library Manager (LibMan) to get the client library from *unpkg*.</span></span> <span data-ttu-id="90b2e-135">unpkg 是一个内容分发网络 (CDN)，可以分发在 npm（即 Node.js 包管理器）中找到的任何内容。</span><span class="sxs-lookup"><span data-stu-id="90b2e-135">unpkg is a content delivery network (CDN)) that can deliver anything found in npm, the Node.js package manager.</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="90b2e-136">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90b2e-136">Visual Studio</span></span>](#tab/visual-studio/)

* <span data-ttu-id="90b2e-137">在“解决方案资源管理器”中，右键单击项目，然后选择“添加” > “客户端库”。</span><span class="sxs-lookup"><span data-stu-id="90b2e-137">In **Solution Explorer**, right-click the project, and select **Add** > **Client-Side Library**.</span></span>

* <span data-ttu-id="90b2e-138">在“添加客户端库”对话框中，对于“提供程序”，选择“unpkg”。</span><span class="sxs-lookup"><span data-stu-id="90b2e-138">In the **Add Client-Side Library** dialog, for **Provider** select **unpkg**.</span></span> 

* <span data-ttu-id="90b2e-139">对于“库”，输入 `@aspnet/signalr@1`，然后选择不是预览版的最新版本。</span><span class="sxs-lookup"><span data-stu-id="90b2e-139">For **Library**, enter `@aspnet/signalr@1`, and select the latest version that isn't preview.</span></span>

  ![“添加客户端库”对话框 - 选择库](signalr/_static/libman1.png)

* <span data-ttu-id="90b2e-141">选择“选择特定文件”，展开“dist/browser”文件夹，然后选择“signalr.js”和“signalr.min.js”。</span><span class="sxs-lookup"><span data-stu-id="90b2e-141">Select **Choose specific files**, expand the *dist/browser* folder, and select *signalr.js* and *signalr.min.js*.</span></span>

* <span data-ttu-id="90b2e-142">将“目标位置”设置为 wwwroot/lib/signalr/，然后选择“安装”。</span><span class="sxs-lookup"><span data-stu-id="90b2e-142">Set **Target Location** to *wwwroot/lib/signalr/*, and select **Install**.</span></span>

  ![“添加客户端库”对话框 - 选择文件和目标](signalr/_static/libman2.png)

  <span data-ttu-id="90b2e-144">LibMan 创建 wwwroot/lib/signalr 文件夹并将所选文件复制到该文件夹。</span><span class="sxs-lookup"><span data-stu-id="90b2e-144">LibMan creates a *wwwroot/lib/signalr* folder and copies the selected files to it.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="90b2e-145">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="90b2e-145">Visual Studio Code</span></span>](#tab/visual-studio-code/)

* <span data-ttu-id="90b2e-146">在集成终端中，运行以下命令以安装 LibMan。</span><span class="sxs-lookup"><span data-stu-id="90b2e-146">In the integrated terminal, run the following command to install LibMan.</span></span>

  ```console
  dotnet tool install -g Microsoft.Web.LibraryManager.Cli
  ```

* <span data-ttu-id="90b2e-147">使用 LibMan 运行以下命令，以获取 SignalR 客户端库。</span><span class="sxs-lookup"><span data-stu-id="90b2e-147">Run the following command to get the SignalR client library by using LibMan.</span></span> <span data-ttu-id="90b2e-148">可能需要等待几秒钟的时间才能看到输出。</span><span class="sxs-lookup"><span data-stu-id="90b2e-148">You might have to wait a few seconds before seeing output.</span></span>

  ```console
  libman install @aspnet/signalr -p unpkg -d wwwroot/lib/signalr --files dist/browser/signalr.js --files dist/browser/signalr.min.js
  ```

  <span data-ttu-id="90b2e-149">参数指定以下选项：</span><span class="sxs-lookup"><span data-stu-id="90b2e-149">The parameters specify the following options:</span></span>
  * <span data-ttu-id="90b2e-150">使用 unpkg 提供程序。</span><span class="sxs-lookup"><span data-stu-id="90b2e-150">Use the unpkg provider.</span></span>
  * <span data-ttu-id="90b2e-151">将文件复制到 wwwroot/lib/signalr 目标。</span><span class="sxs-lookup"><span data-stu-id="90b2e-151">Copy files to the *wwwroot/lib/signalr* destination.</span></span>
  * <span data-ttu-id="90b2e-152">仅复制指定的文件。</span><span class="sxs-lookup"><span data-stu-id="90b2e-152">Copy only the specified files.</span></span>

  <span data-ttu-id="90b2e-153">输出如下所示：</span><span class="sxs-lookup"><span data-stu-id="90b2e-153">The output looks like the following example:</span></span>

  ```console
  wwwroot/lib/signalr/dist/browser/signalr.js written to disk
  wwwroot/lib/signalr/dist/browser/signalr.min.js written to disk
  Installed library "@aspnet/signalr@1.0.3" to "wwwroot/lib/signalr"
  ```

# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="90b2e-154">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="90b2e-154">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="90b2e-155">在“终端”中，运行以下命令以安装 LibMan。</span><span class="sxs-lookup"><span data-stu-id="90b2e-155">In the **Terminal**, run the following command to install LibMan.</span></span>

  ```console
  dotnet tool install -g Microsoft.Web.LibraryManager.Cli
  ```

* <span data-ttu-id="90b2e-156">导航到项目文件夹（包含 SignalRChat.csproj 文件的文件夹）。</span><span class="sxs-lookup"><span data-stu-id="90b2e-156">Navigate to the project folder (the one that contains the *SignalRChat.csproj* file).</span></span>

* <span data-ttu-id="90b2e-157">使用 LibMan 运行以下命令，以获取 SignalR 客户端库。</span><span class="sxs-lookup"><span data-stu-id="90b2e-157">Run the following command to get the SignalR client library by using LibMan.</span></span>

  ```console
  libman install @aspnet/signalr -p unpkg -d wwwroot/lib/signalr --files dist/browser/signalr.js --files dist/browser/signalr.min.js
  ```

  <span data-ttu-id="90b2e-158">参数指定以下选项：</span><span class="sxs-lookup"><span data-stu-id="90b2e-158">The parameters specify the following options:</span></span>
  * <span data-ttu-id="90b2e-159">使用 unpkg 提供程序。</span><span class="sxs-lookup"><span data-stu-id="90b2e-159">Use the unpkg provider.</span></span>
  * <span data-ttu-id="90b2e-160">将文件复制到 wwwroot/lib/signalr 目标。</span><span class="sxs-lookup"><span data-stu-id="90b2e-160">Copy files to the *wwwroot/lib/signalr* destination.</span></span>
  * <span data-ttu-id="90b2e-161">仅复制指定的文件。</span><span class="sxs-lookup"><span data-stu-id="90b2e-161">Copy only the specified files.</span></span>

  <span data-ttu-id="90b2e-162">输出如下所示：</span><span class="sxs-lookup"><span data-stu-id="90b2e-162">The output looks like the following example:</span></span>

  ```console
  wwwroot/lib/signalr/dist/browser/signalr.js written to disk
  wwwroot/lib/signalr/dist/browser/signalr.min.js written to disk
  Installed library "@aspnet/signalr@1.0.3" to "wwwroot/lib/signalr"
  ```

---

## <a name="create-a-signalr-hub"></a><span data-ttu-id="90b2e-163">创建 SignalR 中心</span><span class="sxs-lookup"><span data-stu-id="90b2e-163">Create a SignalR hub</span></span>

<span data-ttu-id="90b2e-164">*中心*是一个类，用作处理客户端 - 服务器通信的高级管道。</span><span class="sxs-lookup"><span data-stu-id="90b2e-164">A *hub* is a class that serves as a high-level pipeline that handles client-server communication.</span></span>

* <span data-ttu-id="90b2e-165">在 SignalRChat 项目文件夹中，创建 Hubs 文件夹。</span><span class="sxs-lookup"><span data-stu-id="90b2e-165">In the SignalRChat project folder, create a *Hubs* folder.</span></span>

* <span data-ttu-id="90b2e-166">在 Hubs 文件夹中，使用以下代码创建 ChatHub.cs 文件：</span><span class="sxs-lookup"><span data-stu-id="90b2e-166">In the *Hubs* folder, create a *ChatHub.cs* file with the following code:</span></span>

  [!code-csharp[Startup](signalr/sample/Hubs/ChatHub.cs)]

  <span data-ttu-id="90b2e-167">`ChatHub` 类继承自 SignalR `Hub` 类。</span><span class="sxs-lookup"><span data-stu-id="90b2e-167">The `ChatHub` class inherits from the SignalR `Hub` class.</span></span> <span data-ttu-id="90b2e-168">`Hub` 类管理连接、组和消息。</span><span class="sxs-lookup"><span data-stu-id="90b2e-168">The `Hub` class manages connections, groups, and messaging.</span></span>

  <span data-ttu-id="90b2e-169">可通过已连接客户端调用 `SendMessage`，以向所有客户端发送消息。</span><span class="sxs-lookup"><span data-stu-id="90b2e-169">The `SendMessage` method can be called by a connected client to send a message to all clients.</span></span> <span data-ttu-id="90b2e-170">本教程后面部分将显示调用该方法的 JavaScript 客户端代码。</span><span class="sxs-lookup"><span data-stu-id="90b2e-170">JavaScript client code that calls the method is shown later in the tutorial.</span></span> <span data-ttu-id="90b2e-171">SignalR 代码是异步模式，可提供最大的可伸缩性。</span><span class="sxs-lookup"><span data-stu-id="90b2e-171">SignalR code is asynchronous to provide maximum scalability.</span></span>

## <a name="configure-signalr"></a><span data-ttu-id="90b2e-172">配置 SignalR</span><span class="sxs-lookup"><span data-stu-id="90b2e-172">Configure SignalR</span></span>

<span data-ttu-id="90b2e-173">必须配置 SignalR 服务器，以将 SignalR 请求传递到 SignalR。</span><span class="sxs-lookup"><span data-stu-id="90b2e-173">The SignalR server must be configured to pass SignalR requests to SignalR.</span></span>

* <span data-ttu-id="90b2e-174">将以下突出显示的代码添加到 Startup.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="90b2e-174">Add the following highlighted code to the *Startup.cs* file.</span></span>

  [!code-csharp[Startup](signalr/sample/Startup.cs?highlight=7,33,52-55)]

  <span data-ttu-id="90b2e-175">这些更改将 SignalR 添加到 ASP.NET Core 依赖关系注入系统和中间件管道。</span><span class="sxs-lookup"><span data-stu-id="90b2e-175">These changes add SignalR to the ASP.NET Core dependency injection system and the middleware pipeline.</span></span>

## <a name="add-signalr-client-code"></a><span data-ttu-id="90b2e-176">添加 SignalR 客户端代码</span><span class="sxs-lookup"><span data-stu-id="90b2e-176">Add SignalR client code</span></span>

* <span data-ttu-id="90b2e-177">使用以下代码替换 Pages\Index.cshtml 中的内容：</span><span class="sxs-lookup"><span data-stu-id="90b2e-177">Replace the content in *Pages\Index.cshtml* with the following code:</span></span>

  [!code-cshtml[Index](signalr/sample/Pages/Index.cshtml)]

  <span data-ttu-id="90b2e-178">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="90b2e-178">The preceding code:</span></span>

  * <span data-ttu-id="90b2e-179">创建名称以及消息文本的文本框和“提交”按钮。</span><span class="sxs-lookup"><span data-stu-id="90b2e-179">Creates text boxes for name and message text, and a submit button.</span></span>
  * <span data-ttu-id="90b2e-180">使用 `id="messagesList"` 创建一个列表，用于显示从 SignalR 中心接收的消息。</span><span class="sxs-lookup"><span data-stu-id="90b2e-180">Creates a list with `id="messagesList"` for displaying messages that are received from the SignalR hub.</span></span>
  * <span data-ttu-id="90b2e-181">包含对 SignalR 的脚本引用以及在下一步中创建的 chat.js 应用程序代码。</span><span class="sxs-lookup"><span data-stu-id="90b2e-181">Includes script references to SignalR and the *chat.js* application code that you create in the next step.</span></span>

* <span data-ttu-id="90b2e-182">在 wwwroot/js 文件夹中，使用以下代码创建 chat.js 文件：</span><span class="sxs-lookup"><span data-stu-id="90b2e-182">In the *wwwroot/js* folder, create a *chat.js* file with the following code:</span></span>

  [!code-javascript[Index](signalr/sample/wwwroot/js/chat.js)]

  <span data-ttu-id="90b2e-183">前面的代码：</span><span class="sxs-lookup"><span data-stu-id="90b2e-183">The preceding code:</span></span>

  * <span data-ttu-id="90b2e-184">创建并启动连接。</span><span class="sxs-lookup"><span data-stu-id="90b2e-184">Creates and starts a connection.</span></span>
  * <span data-ttu-id="90b2e-185">向“提交”按钮添加一个用于向中心发送消息的处理程序。</span><span class="sxs-lookup"><span data-stu-id="90b2e-185">Adds to the submit button a handler that sends messages to the hub.</span></span>
  * <span data-ttu-id="90b2e-186">向连接对象添加一个用于从中心接收消息并将其添加到列表的处理程序。</span><span class="sxs-lookup"><span data-stu-id="90b2e-186">Adds to the connection object a handler that receives messages from the hub and adds them to the list.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="90b2e-187">运行应用</span><span class="sxs-lookup"><span data-stu-id="90b2e-187">Run the app</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="90b2e-188">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90b2e-188">Visual Studio</span></span>](#tab/visual-studio)

* <span data-ttu-id="90b2e-189">按 Ctrl+F5 可运行应用而不进行调试。</span><span class="sxs-lookup"><span data-stu-id="90b2e-189">Press **CTRL+F5** to run the app without debugging.</span></span>

# <a name="visual-studio-codetabvisual-studio-code"></a>[<span data-ttu-id="90b2e-190">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="90b2e-190">Visual Studio Code</span></span>](#tab/visual-studio-code)

* <span data-ttu-id="90b2e-191">在集成终端中，运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="90b2e-191">In the integrated terminal, run the following command:</span></span>

  ```console
  dotnet run -p SignalRChat.csproj
  ```
  
# <a name="visual-studio-for-mactabvisual-studio-mac"></a>[<span data-ttu-id="90b2e-192">Visual Studio for Mac</span><span class="sxs-lookup"><span data-stu-id="90b2e-192">Visual Studio for Mac</span></span>](#tab/visual-studio-mac)

* <span data-ttu-id="90b2e-193">从菜单中选择“运行”>“开始执行(不调试)”。</span><span class="sxs-lookup"><span data-stu-id="90b2e-193">From the menu, select **Run > Start Without Debugging**.</span></span>

---

* <span data-ttu-id="90b2e-194">从地址栏复制 URL，打开另一个浏览器实例或选项卡，并在地址栏中粘贴该 URL。</span><span class="sxs-lookup"><span data-stu-id="90b2e-194">Copy the URL from the address bar, open another browser instance or tab, and paste the URL in the address bar.</span></span>

* <span data-ttu-id="90b2e-195">选择任一浏览器，输入名称和消息，然后选择“发送消息”按钮。</span><span class="sxs-lookup"><span data-stu-id="90b2e-195">Choose either browser, enter a name and message, and select the **Send Message** button.</span></span>

  <span data-ttu-id="90b2e-196">两个页面上立即显示名称和消息。</span><span class="sxs-lookup"><span data-stu-id="90b2e-196">The name and message are displayed on both pages instantly.</span></span>

  ![SignalR 示例应用](signalr/_static/signalr-get-started-finished.png)

> [!TIP]
> <span data-ttu-id="90b2e-198">如果应用不起作用，请打开浏览器开发人员工具 (F12) 并转到控制台。</span><span class="sxs-lookup"><span data-stu-id="90b2e-198">If the app doesn't work, open your browser developer tools (F12) and go to the console.</span></span> <span data-ttu-id="90b2e-199">可能会看到与 HTML 和 JavaScript 代码相关的错误。</span><span class="sxs-lookup"><span data-stu-id="90b2e-199">You might see errors related to your HTML and JavaScript code.</span></span> <span data-ttu-id="90b2e-200">例如，假设将 signalr.js 放在不同于系统指示的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="90b2e-200">For example, suppose you put *signalr.js* in a different folder than directed.</span></span> <span data-ttu-id="90b2e-201">在这种情况下，对该文件的引用将不起作用，并且你将在控制台中看到 404 错误。</span><span class="sxs-lookup"><span data-stu-id="90b2e-201">In that case the reference to that file won't work and you'll see a 404 error in the console.</span></span>
> <span data-ttu-id="90b2e-202">![未找到 signalr.js 错误](signalr/_static/f12-console.png)</span><span class="sxs-lookup"><span data-stu-id="90b2e-202">![signalr.js not found error](signalr/_static/f12-console.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="90b2e-203">后续步骤</span><span class="sxs-lookup"><span data-stu-id="90b2e-203">Next steps</span></span>

<span data-ttu-id="90b2e-204">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="90b2e-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="90b2e-205">创建 Web 应用项目。</span><span class="sxs-lookup"><span data-stu-id="90b2e-205">Create a web app project.</span></span>
> * <span data-ttu-id="90b2e-206">添加 SignalR 客户端库。</span><span class="sxs-lookup"><span data-stu-id="90b2e-206">Add the SignalR client library.</span></span>
> * <span data-ttu-id="90b2e-207">创建 SignalR 中心。</span><span class="sxs-lookup"><span data-stu-id="90b2e-207">Create a SignalR hub.</span></span>
> * <span data-ttu-id="90b2e-208">配置项目以使用 SignalR。</span><span class="sxs-lookup"><span data-stu-id="90b2e-208">Configure the project to use SignalR.</span></span>
> * <span data-ttu-id="90b2e-209">添加代码，以便使用此中心将消息从任何客户端发送到所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="90b2e-209">Add code that uses the hub to send messages from any client to all connected clients.</span></span>

<span data-ttu-id="90b2e-210">若要详细了解 SignalR，请参阅简介：</span><span class="sxs-lookup"><span data-stu-id="90b2e-210">To learn more about SignalR, see the introduction:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="90b2e-211">ASP.NET Core SignalR 简介</span><span class="sxs-lookup"><span data-stu-id="90b2e-211">Introduction to ASP.NET Core SignalR</span></span>](xref:signalr/introduction)
