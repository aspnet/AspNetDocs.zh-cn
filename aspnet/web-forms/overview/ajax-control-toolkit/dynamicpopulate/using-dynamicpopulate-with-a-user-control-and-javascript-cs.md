---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
title: 通过用户控件和 JavaScript (C#) 使用 DynamicPopulate |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页面方法），并将生成的值填充到 t 上的目标控件...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 38ac8250-8854-444c-b9ab-8998faa41c5a
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-cs
msc.type: authoredcontent
ms.openlocfilehash: 0462d8357d83115e751a818d3c9feb4b4274e212
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59402539"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-c"></a><span data-ttu-id="69727-103">通过用户控件和 JavaScript 使用 DynamicPopulate (C#)</span><span class="sxs-lookup"><span data-stu-id="69727-103">Using DynamicPopulate with a User Control And JavaScript (C#)</span></span>

<span data-ttu-id="69727-104">通过[Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="69727-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="69727-105">[下载代码](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.cs.zip)或[下载 PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="69727-105">[Download Code](http://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.cs.zip) or [Download PDF](http://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2CS.pdf)</span></span>

> <span data-ttu-id="69727-106">ASP.NET AJAX 控件工具包中的 DynamicPopulate 控件调用 web 服务 （或页面方法），并将生成的值填充到目标控件在页上，而无需刷新页面。</span><span class="sxs-lookup"><span data-stu-id="69727-106">The DynamicPopulate control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="69727-107">还有可能触发使用自定义客户端的 JavaScript 代码的填充。</span><span class="sxs-lookup"><span data-stu-id="69727-107">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="69727-108">但是特别留意具有扩展器驻留在用户控件时要执行。</span><span class="sxs-lookup"><span data-stu-id="69727-108">However special care has to be taken when the extender resides in a user control.</span></span>


## <a name="overview"></a><span data-ttu-id="69727-109">概述</span><span class="sxs-lookup"><span data-stu-id="69727-109">Overview</span></span>

<span data-ttu-id="69727-110">`DynamicPopulate` ASP.NET AJAX 控件工具包中的控件调用 web 服务 （或页面方法），并将生成的值填充到目标控件在页上，而无需刷新页面。</span><span class="sxs-lookup"><span data-stu-id="69727-110">The `DynamicPopulate` control in the ASP.NET AJAX Control Toolkit calls a web service (or page method) and fills the resulting value into a target control on the page, without a page refresh.</span></span> <span data-ttu-id="69727-111">还有可能触发使用自定义客户端的 JavaScript 代码的填充。</span><span class="sxs-lookup"><span data-stu-id="69727-111">It is also possible to trigger the population using custom client-side JavaScript code.</span></span> <span data-ttu-id="69727-112">但是特别留意具有扩展器驻留在用户控件时要执行。</span><span class="sxs-lookup"><span data-stu-id="69727-112">However special care has to be taken when the extender resides in a user control.</span></span>

## <a name="steps"></a><span data-ttu-id="69727-113">步骤</span><span class="sxs-lookup"><span data-stu-id="69727-113">Steps</span></span>

<span data-ttu-id="69727-114">首先，需要 ASP.NET Web 服务实现的方法调用的`DynamicPopulateExtender`控件。</span><span class="sxs-lookup"><span data-stu-id="69727-114">First of all, you need an ASP.NET Web Service which implements the method to be called by the `DynamicPopulateExtender` control.</span></span> <span data-ttu-id="69727-115">Web 服务实现方法`getDate()`需要一个自变量的类型字符串，调用`contextKey`，因为`DynamicPopulate`控件将发送一条与每个 web 服务调用上下文信息。</span><span class="sxs-lookup"><span data-stu-id="69727-115">The web service implements the method `getDate()` that expects one argument of type string, called `contextKey`, since the `DynamicPopulate` control sends one piece of context information with each web service call.</span></span> <span data-ttu-id="69727-116">下面是代码 (文件`DynamicPopulate.cs.asmx`) 中检索当前日期中三种格式之一：</span><span class="sxs-lookup"><span data-stu-id="69727-116">Here is the code (file `DynamicPopulate.cs.asmx`) which retrieves the current date in one of three formats:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample1.aspx)]

<span data-ttu-id="69727-117">在下一步中创建新的用户控件 (`.ascx`文件)，表示由其第一行中的以下声明：</span><span class="sxs-lookup"><span data-stu-id="69727-117">In the next step, create a new user control (`.ascx` file), denoted by the following declaration in its first line:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample2.aspx)]

<span data-ttu-id="69727-118">一个&lt; `label` &gt;元素将用于显示来自服务器的数据。</span><span class="sxs-lookup"><span data-stu-id="69727-118">A &lt;`label`&gt; element will be used to display the data coming from the server.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample3.aspx)]

<span data-ttu-id="69727-119">此外在用户控件文件中，我们将使用三个单选按钮，每个表示一个 web 服务支持的三个可能的日期格式。</span><span class="sxs-lookup"><span data-stu-id="69727-119">Also in the user control file, we will use three radio buttons, each one representing one of the three possible date formats supported by the web service.</span></span> <span data-ttu-id="69727-120">当用户单击一个单选按钮上时，浏览器将执行 JavaScript 代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="69727-120">When the user clicks on one of the radio buttons, the browser will execute JavaScript code which looks like this:</span></span>

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample4.ps1)]

<span data-ttu-id="69727-121">此代码访问`DynamicPopulateExtender`（不用再担心如何奇怪 ID 尚不，这将稍后介绍），并触发数据动态填充。</span><span class="sxs-lookup"><span data-stu-id="69727-121">This code accesses the `DynamicPopulateExtender` (do not worry about the strange ID yet, this will be covered later on) and triggers the dynamic population with data.</span></span> <span data-ttu-id="69727-122">中的当前单选按钮，上下文`this.value`其值即是指`format1`，`format2`或`format3`完全什么 web 方法的要求。</span><span class="sxs-lookup"><span data-stu-id="69727-122">In the context of the current radio button, `this.value` refers to its value which is `format1`, `format2` or `format3` exactly what the web method expects.</span></span>

<span data-ttu-id="69727-123">唯一尚未缺少用户控件中是`DynamicPopulateExtender`可链接到 web 服务的单选按钮控件。</span><span class="sxs-lookup"><span data-stu-id="69727-123">The only thing missing in the user control yet is the `DynamicPopulateExtender` control which links the radio buttons to the web service.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample5.aspx)]

<span data-ttu-id="69727-124">再一次可能会注意该控件中使用的奇怪 ID:`mcd1$myDate`而不是`myDate`。</span><span class="sxs-lookup"><span data-stu-id="69727-124">Again you may note the strange ID used in the control: `mcd1$myDate` instead of `myDate`.</span></span> <span data-ttu-id="69727-125">以前，使用的 JavaScript 代码`mcd1_dpe1`访问`DynamicPopulateExtender`而不是`dpe1`。此命名策略是一个特殊的要求时使用`DynamicPopulateExtender`用户控件内。</span><span class="sxs-lookup"><span data-stu-id="69727-125">Previously, the JavaScript code used `mcd1_dpe1` to access the `DynamicPopulateExtender` instead of `dpe1`.This naming strategy is a special requirement when using `DynamicPopulateExtender` within a user control.</span></span> <span data-ttu-id="69727-126">此外，您必须在特定的方式，以使其工作中嵌入用户控件。</span><span class="sxs-lookup"><span data-stu-id="69727-126">Furthermore, you have to embed the user control in a specific way to make it all work.</span></span> <span data-ttu-id="69727-127">创建一个新的 ASP.NET 页面并注册你只需实现的用户控件标记前缀：</span><span class="sxs-lookup"><span data-stu-id="69727-127">Create a new ASP.NET page and register a tag prefix for the user control you have just implemented:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample6.aspx)]

<span data-ttu-id="69727-128">然后，包括 ASP.NET AJAX`ScriptManager`新页上的控件：</span><span class="sxs-lookup"><span data-stu-id="69727-128">Then, include the ASP.NET AJAX `ScriptManager` control on the new page:</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample7.aspx)]

<span data-ttu-id="69727-129">最后，将用户控件添加到页面。</span><span class="sxs-lookup"><span data-stu-id="69727-129">Finally, add the user control to the page.</span></span> <span data-ttu-id="69727-130">只需设置其`ID`属性 (和`runat="server"`，当然)，但您还必须将其设置为一个特定的名称：`mcd1`由于这是用户控件内用于使用 JavaScript 访问它的前缀。</span><span class="sxs-lookup"><span data-stu-id="69727-130">You only have to set its `ID` attribute (and `runat="server"`, of course), but you also have to set it to a specific name: `mcd1` since this is the prefix used within the user control to access it using JavaScript.</span></span>

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-cs/samples/sample8.aspx)]

<span data-ttu-id="69727-131">就是这么简单！</span><span class="sxs-lookup"><span data-stu-id="69727-131">And that's it!</span></span> <span data-ttu-id="69727-132">页面的行为都按预期方式：用户单击其中一个单选按钮，该工具包中的控件调用 web 服务，并以所需的格式显示当前日期。</span><span class="sxs-lookup"><span data-stu-id="69727-132">The page behaves as expected: A user clicks on one of the radio buttons, the control in the Toolkit calls the web service and displays the current date in the desired format.</span></span>


<span data-ttu-id="69727-133">[![单选按钮位于用户控件](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="69727-133">[![The radio buttons reside in a user control](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image1.png)</span></span>

<span data-ttu-id="69727-134">单选按钮位于用户控件 ([单击此项可查看原尺寸图像](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="69727-134">The radio buttons reside in a user control ([Click to view full-size image](using-dynamicpopulate-with-a-user-control-and-javascript-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="69727-135">[上一页](dynamically-populating-a-control-using-javascript-code-cs.md)
> [下一页](dynamically-populating-a-control-vb.md)</span><span class="sxs-lookup"><span data-stu-id="69727-135">[Previous](dynamically-populating-a-control-using-javascript-code-cs.md)
[Next](dynamically-populating-a-control-vb.md)</span></span>
