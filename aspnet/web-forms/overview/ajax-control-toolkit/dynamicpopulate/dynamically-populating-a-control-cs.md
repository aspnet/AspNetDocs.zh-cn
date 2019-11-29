---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
title: 动态填充控件（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的通过 dynamicpopulate 控件调用 web 服务（或页面方法），并将生成的值填充到 t 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e1fec43e-1daf-49d2-b0c7-7f1b930455cc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 24f88e44e0f878127314774d4e8846f80133413e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599289"
---
# <a name="dynamically-populating-a-control-c"></a><span data-ttu-id="a0320-103">动态填充控件 (C#)</span><span class="sxs-lookup"><span data-stu-id="a0320-103">Dynamically Populating a Control (C#)</span></span>

<span data-ttu-id="a0320-104">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="a0320-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="a0320-105">[下载代码](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.cs.zip)或[下载 PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="a0320-105">[Download Code](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.cs.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0CS.pdf)</span></span>

> <span data-ttu-id="a0320-106">ASP.NET AJAX 控件工具包中的通过 dynamicpopulate 控件调用 web 服务（或页面方法），并将生成的值填充到页面上的目标控件中，而无需进行页刷新。</span><span class="sxs-lookup"><span data-stu-id="a0320-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span>

## <a name="overview"></a><span data-ttu-id="a0320-107">概述</span><span class="sxs-lookup"><span data-stu-id="a0320-107">Overview</span></span>

<span data-ttu-id="a0320-108">ASP.NET AJAX 控件工具包中的 `DynamicPopulate` 控件将调用 web 服务（或页面方法），并将生成的值填充到页面上的目标控件中，而无需进行页刷新。</span><span class="sxs-lookup"><span data-stu-id="a0320-108">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="a0320-109">本教程演示如何对此进行设置。</span><span class="sxs-lookup"><span data-stu-id="a0320-109">This tutorial shows how to set this up.</span></span>

## <a name="steps"></a><span data-ttu-id="a0320-110">步骤</span><span class="sxs-lookup"><span data-stu-id="a0320-110">Steps</span></span>

<span data-ttu-id="a0320-111">首先，需要一个 ASP.NET Web 服务，该服务实现 `DynamicPopulate`要调用的方法。</span><span class="sxs-lookup"><span data-stu-id="a0320-111">First of all, you need an ASP.NET Web Service which implements the method to be called by `DynamicPopulate`.</span></span> <span data-ttu-id="a0320-112">Web 服务类需要 `Microsoft.Web.Script.Services`中定义的 `ScriptService` 特性;否则，ASP.NET AJAX 无法为 web 服务创建客户端 JavaScript 代理，而 `DynamicPopulate`需要这样做。</span><span class="sxs-lookup"><span data-stu-id="a0320-112">The web service class requires the `ScriptService` attribute which is defined within `Microsoft.Web.Script.Services`; otherwise ASP.NET AJAX cannot create the client-side JavaScript proxy for the web service which in turn is required by `DynamicPopulate`.</span></span>

<span data-ttu-id="a0320-113">Web 方法必须预期一个 string 类型的参数（称为 `contextKey`），因为 `DynamicPopulate` 控件向每个 web 服务调用发送一段上下文信息。</span><span class="sxs-lookup"><span data-stu-id="a0320-113">The web method must expect one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="a0320-114">以下 web 服务以 `contextKey` 参数表示的格式返回当前日期：</span><span class="sxs-lookup"><span data-stu-id="a0320-114">The following web service returns the current date in a format represented by the `contextKey` argument:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample1.aspx)]

<span data-ttu-id="a0320-115">然后，web 服务将另存为 `DynamicPopulate.cs.asmx`。</span><span class="sxs-lookup"><span data-stu-id="a0320-115">The web service is then saved as `DynamicPopulate.cs.asmx`.</span></span> <span data-ttu-id="a0320-116">或者，您可以使用 `DynamicPopulate` 控件将 `getDate()` 方法作为实际 ASP.NET 页中的页方法实现。</span><span class="sxs-lookup"><span data-stu-id="a0320-116">Alternatively, you could implement the `getDate()` method as a page method within the actual ASP.NET page with the `DynamicPopulate` control.</span></span>

<span data-ttu-id="a0320-117">在下一步中，创建一个新的 ASP.NET 文件。</span><span class="sxs-lookup"><span data-stu-id="a0320-117">In the next step, create a new ASP.NET file.</span></span> <span data-ttu-id="a0320-118">与往常一样，第一步是将 `ScriptManager` 包含在当前页面中，以加载 ASP.NET AJAX 库并使控件工具包工作：</span><span class="sxs-lookup"><span data-stu-id="a0320-118">As always, the first step is to include the `ScriptManager` in the current page to load the ASP.NET AJAX library and to make the Control Toolkit work:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample2.aspx)]

<span data-ttu-id="a0320-119">然后，添加 "标签" 控件（例如，使用同一名称的 HTML 控件，或 &lt;`asp:Label` /&gt; web 控件中），后者稍后会显示 web 服务调用的结果。</span><span class="sxs-lookup"><span data-stu-id="a0320-119">Then, add a label control (for instance using the HTML control of the same name, or the &lt;`asp:Label` /&gt; web control) which will later show the result of the web service call.</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample3.aspx)]

<span data-ttu-id="a0320-120">HTML 按钮（作为 HTML 控件，因为我们不需要回发到服务器）将用于触发动态填充：</span><span class="sxs-lookup"><span data-stu-id="a0320-120">An HTML button (as an HTML control, since we do not require a postback to the server) will then be used to trigger the dynamic population:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample4.aspx)]

<span data-ttu-id="a0320-121">最后，我们需要 `DynamicPopulateExtender` 控件来连接问题。</span><span class="sxs-lookup"><span data-stu-id="a0320-121">Finally, we need the `DynamicPopulateExtender` control to wire things up.</span></span> <span data-ttu-id="a0320-122">将设置以下属性（`ID` 和 `runat`=`"server"`）：</span><span class="sxs-lookup"><span data-stu-id="a0320-122">The following attributes will be set (apart from the obvious ones, `ID` and `runat`=`"server"`):</span></span>

- <span data-ttu-id="a0320-123">`TargetControlID` 在何处放置 web 服务调用的结果</span><span class="sxs-lookup"><span data-stu-id="a0320-123">`TargetControlID` where to put the result from the web service call</span></span>
- <span data-ttu-id="a0320-124">web 服务的 `ServicePath` 路径（如果要使用 page 方法，则省略）</span><span class="sxs-lookup"><span data-stu-id="a0320-124">`ServicePath` path to the web service (omit if you want to use a page method)</span></span>
- <span data-ttu-id="a0320-125">web 方法或页方法 `ServiceMethod` 名称</span><span class="sxs-lookup"><span data-stu-id="a0320-125">`ServiceMethod` name of the web method or page method</span></span>
- <span data-ttu-id="a0320-126">`ContextKey` 要发送到 web 服务的上下文信息</span><span class="sxs-lookup"><span data-stu-id="a0320-126">`ContextKey` context information to be sent to the web service</span></span>
- <span data-ttu-id="a0320-127">触发 web 服务调用的 `PopulateTriggerControlID` 元素</span><span class="sxs-lookup"><span data-stu-id="a0320-127">`PopulateTriggerControlID` element which triggers the web service call</span></span>
- <span data-ttu-id="a0320-128">`ClearContentsDuringUpdate` 在 web 服务调用期间是否清空目标元素</span><span class="sxs-lookup"><span data-stu-id="a0320-128">`ClearContentsDuringUpdate` whether to empty the target element during the web service call</span></span>

<span data-ttu-id="a0320-129">正如您所看到的那样，控件需要一些信息，但将所有内容放在适当的位置都是非常简单的。</span><span class="sxs-lookup"><span data-stu-id="a0320-129">As you can see, the control requires some information but putting everything into place is quite straight-forward.</span></span> <span data-ttu-id="a0320-130">下面是当前方案中 `DynamicPopulateExtender` 控件的标记：</span><span class="sxs-lookup"><span data-stu-id="a0320-130">Here is the markup for the `DynamicPopulateExtender` control in the current scenario:</span></span>

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample5.aspx)]

<span data-ttu-id="a0320-131">在浏览器中运行 "ASP.NET" 页，然后单击该按钮;您将收到以月/日为年份的当前日期。</span><span class="sxs-lookup"><span data-stu-id="a0320-131">Run the ASP.NET page in the browser and click on the button; you will receive the current date in month-day-year format.</span></span>

<span data-ttu-id="a0320-132">[![单击该按钮将从服务器中检索日期](dynamically-populating-a-control-cs/_static/image2.png)](dynamically-populating-a-control-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a0320-132">[![A click on the button retrieves the date from the server](dynamically-populating-a-control-cs/_static/image2.png)](dynamically-populating-a-control-cs/_static/image1.png)</span></span>

<span data-ttu-id="a0320-133">单击该按钮将从服务器中检索日期（[单击查看完全大小的图像](dynamically-populating-a-control-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="a0320-133">A click on the button retrieves the date from the server ([Click to view full-size image](dynamically-populating-a-control-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a0320-134">下一页</span><span class="sxs-lookup"><span data-stu-id="a0320-134">Next</span></span>](dynamically-populating-a-control-using-javascript-code-cs.md)
