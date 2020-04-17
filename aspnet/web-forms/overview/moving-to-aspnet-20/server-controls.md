---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 服务器控制 |微软文档
author: rick-anderson
description: ASP.NET 2.0 在许多方面增强了服务器控件。 在本模块中，我们将介绍ASP.NET 2.0 和 Visual Studio 200 的方式的一些体系结构更改。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: 7109f10e87abfadf1e7e08795cf9d3d6bf5df122
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543738"
---
# <a name="server-controls"></a><span data-ttu-id="2cdca-104">服务器控件</span><span class="sxs-lookup"><span data-stu-id="2cdca-104">Server Controls</span></span>

<span data-ttu-id="2cdca-105">由[微软](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="2cdca-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="2cdca-106">ASP.NET 2.0 在许多方面增强了服务器控件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-106">ASP.NET 2.0 enhances server controls in many ways.</span></span> <span data-ttu-id="2cdca-107">在本模块中，我们将介绍ASP.NET 2.0 和 Visual Studio 2005 处理服务器控件的方式的一些体系结构更改。</span><span class="sxs-lookup"><span data-stu-id="2cdca-107">In this module, we'll cover some of the architectural changes to the way ASP.NET 2.0 and Visual Studio 2005 deals with server controls.</span></span>

<span data-ttu-id="2cdca-108">ASP.NET 2.0 在许多方面增强了服务器控件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-108">ASP.NET 2.0 enhances server controls in many ways.</span></span> <span data-ttu-id="2cdca-109">在本模块中，我们将介绍ASP.NET 2.0 和 Visual Studio 2005 处理服务器控件的方式的一些体系结构更改。</span><span class="sxs-lookup"><span data-stu-id="2cdca-109">In this module, we'll cover some of the architectural changes to the way ASP.NET 2.0 and Visual Studio 2005 deals with server controls.</span></span>

## <a name="view-state"></a><span data-ttu-id="2cdca-110">查看状态</span><span class="sxs-lookup"><span data-stu-id="2cdca-110">View state</span></span>

<span data-ttu-id="2cdca-111">ASP.NET 2.0 中视图状态的主要变化是大小显著减小。</span><span class="sxs-lookup"><span data-stu-id="2cdca-111">The primary change in view state in ASP.NET 2.0 is a dramatic reduction in size.</span></span> <span data-ttu-id="2cdca-112">考虑一个只有"日历"控件的页面。</span><span class="sxs-lookup"><span data-stu-id="2cdca-112">Consider a page with only a Calendar control on it.</span></span> <span data-ttu-id="2cdca-113">下面是ASP.NET 1.1 中的视图状态。</span><span class="sxs-lookup"><span data-stu-id="2cdca-113">Here is the view state in ASP.NET 1.1.</span></span>

[!code-css[Main](server-controls/samples/sample1.css)]

<span data-ttu-id="2cdca-114">现在，下面是ASP.NET 2.0 中相同页面上的视图状态。</span><span class="sxs-lookup"><span data-stu-id="2cdca-114">Now here's the view state on an identical page in ASP.NET 2.0.</span></span>

[!code-css[Main](server-controls/samples/sample2.css)]

<span data-ttu-id="2cdca-115">这是一个相当重大的变化，考虑到视图状态在线上来回移动，此更改可以显著提高开发人员的性能。</span><span class="sxs-lookup"><span data-stu-id="2cdca-115">That's a pretty significant change, and considering that view state is carried back and forth over the wire, this change can give developers a significant performance increase.</span></span> <span data-ttu-id="2cdca-116">视图状态大小的减小主要是由于我们在内部处理它的方式。</span><span class="sxs-lookup"><span data-stu-id="2cdca-116">The reduction in size of view state is largely due to the way that we handle it internally.</span></span> <span data-ttu-id="2cdca-117">请记住，视图状态是 Base64 编码字符串。</span><span class="sxs-lookup"><span data-stu-id="2cdca-117">Remember that view state is a Base64 encoded string.</span></span> <span data-ttu-id="2cdca-118">为了更好地了解 ASP.NET 2.0 中视图状态的变化，让我们从上面的示例中查看解码的值。</span><span class="sxs-lookup"><span data-stu-id="2cdca-118">To better understand the change in view state in ASP.NET 2.0, let's have a look at the decoded values from the examples above.</span></span>

<span data-ttu-id="2cdca-119">下面是已解码的 1.1 视图状态：</span><span class="sxs-lookup"><span data-stu-id="2cdca-119">Here is the 1.1 view state decoded:</span></span>

[!code-css[Main](server-controls/samples/sample3.css)]

<span data-ttu-id="2cdca-120">这可能看起来有点胡言乱语，但这里有一个模式。</span><span class="sxs-lookup"><span data-stu-id="2cdca-120">This may look a bit like gibberish, but there is a pattern here.</span></span> <span data-ttu-id="2cdca-121">在ASP.NET 1.x 中，我们使用单个字符来标识&lt;&gt;数据类型并使用字符分隔值。</span><span class="sxs-lookup"><span data-stu-id="2cdca-121">In ASP.NET 1.x, we used single characters to identify data-types and delimited values using the &lt;&gt; characters.</span></span> <span data-ttu-id="2cdca-122">上面的视图状态示例中的"t"表示三重。</span><span class="sxs-lookup"><span data-stu-id="2cdca-122">The "t" in the view state sample above represents a Triplet.</span></span> <span data-ttu-id="2cdca-123">三重列表包含一对数组列表（"l"表示数组列表）。其中一个数组列表包含一个 Int32 （"i"），其值为 1，另一个包含另一个 Triplet。</span><span class="sxs-lookup"><span data-stu-id="2cdca-123">The Triplet contains a pair of ArrayLists (the "l" represents an ArrayList.) One of those ArrayLists contains an Int32 ("i") with a value of 1 and the other contains another Triplet.</span></span> <span data-ttu-id="2cdca-124">三重包含一对数组列表等。需要记住的重要的事情是，我们使用包含对的三脚架，我们通过字母识别数据类型，并使用 和&lt;&gt;字符作为分隔符。</span><span class="sxs-lookup"><span data-stu-id="2cdca-124">The Triplet contains a pair of ArrayLists, etc. The important thing to remember is that we use Triplets that contain pairs, we identify the data-types via a letter, and we use the &lt; and &gt; characters as delimiters.</span></span>

<span data-ttu-id="2cdca-125">在ASP.NET 2.0 中，解码的视图状态看起来有点不同。</span><span class="sxs-lookup"><span data-stu-id="2cdca-125">In ASP.NET 2.0, the decoded view state looks a bit different.</span></span>

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

<span data-ttu-id="2cdca-126">您应该注意到解码视图状态的外观发生巨大变化。</span><span class="sxs-lookup"><span data-stu-id="2cdca-126">You should notice a huge change in the appearance of the decoded view state.</span></span> <span data-ttu-id="2cdca-127">此更改具有多个体系结构基础。</span><span class="sxs-lookup"><span data-stu-id="2cdca-127">This change has several architectural underpinnings.</span></span> <span data-ttu-id="2cdca-128">ASP.NET 1.x 中的视图状态使用 LosFormatter 对数据进行序列化。</span><span class="sxs-lookup"><span data-stu-id="2cdca-128">View state in ASP.NET 1.x used the LosFormatter to serialize data.</span></span> <span data-ttu-id="2cdca-129">在 2.0 中，我们使用新的 ObjectStateFormatter 类。</span><span class="sxs-lookup"><span data-stu-id="2cdca-129">In 2.0, we use the new ObjectStateFormatter class.</span></span> <span data-ttu-id="2cdca-130">此类是专门为帮助视图状态和控制状态的序列化和反序列化而设计的。</span><span class="sxs-lookup"><span data-stu-id="2cdca-130">This class was specifically designed to aid in the serialization and deserialization of view state and control state.</span></span> <span data-ttu-id="2cdca-131">（下一节将介绍控制状态。通过改变序列化和反序列化的方法，可以带来许多好处。</span><span class="sxs-lookup"><span data-stu-id="2cdca-131">(Control state will be covered in the next section.) There are many benefits gained by changing the method by which serialization and deserialization take place.</span></span> <span data-ttu-id="2cdca-132">其中最戏剧性的是，与使用文本Writer的LosFormatter不同，ObjectStateFormatter使用二进制写入器。</span><span class="sxs-lookup"><span data-stu-id="2cdca-132">One of the most dramatic is the fact that unlike the LosFormatter which uses a TextWriter, the ObjectStateFormatter uses a BinaryWriter.</span></span> <span data-ttu-id="2cdca-133">这允许ASP.NET 2.0 存储一系列字节而不是字符串的视图状态。</span><span class="sxs-lookup"><span data-stu-id="2cdca-133">This allows ASP.NET 2.0 to store view state a series of bytes instead of strings.</span></span> <span data-ttu-id="2cdca-134">以整数为例。</span><span class="sxs-lookup"><span data-stu-id="2cdca-134">Take, for example, an integer.</span></span> <span data-ttu-id="2cdca-135">在ASP.NET 1.1 中，整数需要 4 个字节的视图状态。</span><span class="sxs-lookup"><span data-stu-id="2cdca-135">In ASP.NET 1.1, an integer required 4 bytes of view state.</span></span> <span data-ttu-id="2cdca-136">在ASP.NET 2.0 中，相同的整数只需要 1 个字节。</span><span class="sxs-lookup"><span data-stu-id="2cdca-136">In ASP.NET 2.0, that same integer only requires 1 byte.</span></span> <span data-ttu-id="2cdca-137">进行了其他增强，以减少存储的视图状态量。</span><span class="sxs-lookup"><span data-stu-id="2cdca-137">Other enhancements were made to decrease the amount of view state that is stored.</span></span> <span data-ttu-id="2cdca-138">例如，DateTime 值现在使用 TickCount 而不是字符串进行存储。</span><span class="sxs-lookup"><span data-stu-id="2cdca-138">DateTime values, for example, are now stored using a TickCount instead of a string.</span></span>

<span data-ttu-id="2cdca-139">似乎所有这一切还不够，特别注意的是，在 1.x 中，视图状态的最大使用者之一是 DataGrid 和类似的控件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-139">As if all of that weren't enough, special attention was paid to the fact that one of the greatest consumers of view state in 1.x was the DataGrid and similar controls.</span></span> <span data-ttu-id="2cdca-140">控件（如视图状态所在的 DataGrid）的一个主要缺点是，它通常包含大量重复的信息。</span><span class="sxs-lookup"><span data-stu-id="2cdca-140">A major drawback of controls such as the DataGrid where view state is concerned is that it often contains large amounts of repeated information.</span></span> <span data-ttu-id="2cdca-141">在ASP.NET 1.x 中，重复的信息只是一遍又一遍地存储，导致视图状态膨胀。</span><span class="sxs-lookup"><span data-stu-id="2cdca-141">In ASP.NET 1.x, that repeated information was simply stored over and over again resulting in a bloated view state.</span></span> <span data-ttu-id="2cdca-142">在 ASP.NET 2.0 中，我们使用新的 IndexedString 类来存储此类数据。</span><span class="sxs-lookup"><span data-stu-id="2cdca-142">In ASP.NET 2.0, we use the new IndexedString class to store such data.</span></span> <span data-ttu-id="2cdca-143">如果字符串重复，我们只需将索引String 和索引的令牌存储在索引String 对象的运行表中。</span><span class="sxs-lookup"><span data-stu-id="2cdca-143">If a string repeats, we just store the token for the IndexedString and the index within a running table of IndexedString objects.</span></span>

## <a name="control-state"></a><span data-ttu-id="2cdca-144">控制状态</span><span class="sxs-lookup"><span data-stu-id="2cdca-144">Control State</span></span>

<span data-ttu-id="2cdca-145">开发人员对视图状态的主要抱怨之一是它添加到 HTTP 负载的大小。</span><span class="sxs-lookup"><span data-stu-id="2cdca-145">One of the major gripes that developers had with view state was the size that it added to the HTTP payload.</span></span> <span data-ttu-id="2cdca-146">如前所述，视图状态的最大使用者之一是 DataGrid 控件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-146">As previously mentioned, one of the greatest consumers of view state is the DataGrid control.</span></span> <span data-ttu-id="2cdca-147">为了避免 DataGrid 生成的大量视图状态，许多开发人员只是禁用该控件的视图状态。</span><span class="sxs-lookup"><span data-stu-id="2cdca-147">To avoid the huge amounts of view state generated by a DataGrid, many developers simply disabled view state for that control.</span></span> <span data-ttu-id="2cdca-148">不幸的是，这个解决方案并不总是一个好的。</span><span class="sxs-lookup"><span data-stu-id="2cdca-148">Unfortunately, that solution wasn't always a good one.</span></span> <span data-ttu-id="2cdca-149">ASP.NET 1.x 中的视图状态不仅包含控件正确功能所需的数据。</span><span class="sxs-lookup"><span data-stu-id="2cdca-149">View state in ASP.NET 1.x contains not only data necessary for the correct functionality of the control.</span></span> <span data-ttu-id="2cdca-150">它还包含有关控件 UI 的状态的信息。</span><span class="sxs-lookup"><span data-stu-id="2cdca-150">It also contains information concerning the state of the control's UI.</span></span> <span data-ttu-id="2cdca-151">这意味着，如果要允许在 DataGrid 上进行分页，则必须启用视图状态，即使您不需要视图状态包含的所有 UI 信息也是如此。</span><span class="sxs-lookup"><span data-stu-id="2cdca-151">This means that if you want to allow for pagination on a DataGrid, you must enable view state even if you don't need all of the UI information that view state contains.</span></span> <span data-ttu-id="2cdca-152">这是一个全有或全无的情况。</span><span class="sxs-lookup"><span data-stu-id="2cdca-152">It's an all-or-nothing scenario.</span></span>

<span data-ttu-id="2cdca-153">在ASP.NET 2.0 中，控制状态通过引入控制状态很好地解决了该问题。</span><span class="sxs-lookup"><span data-stu-id="2cdca-153">In ASP.NET 2.0, control state solves that problem nicely via the introduction of control state.</span></span> <span data-ttu-id="2cdca-154">控件状态包含控件正确功能绝对必要的数据。</span><span class="sxs-lookup"><span data-stu-id="2cdca-154">Control state contains the data that is absolutely necessary for the proper functionality of a control.</span></span> <span data-ttu-id="2cdca-155">与视图状态不同，无法禁用控件状态。</span><span class="sxs-lookup"><span data-stu-id="2cdca-155">Unlike view state, control state cannot be disabled.</span></span> <span data-ttu-id="2cdca-156">因此，必须严格控制存储在受控状态的数据。</span><span class="sxs-lookup"><span data-stu-id="2cdca-156">Therefore, it is important that the data being stored in control state is carefully controlled.</span></span>

> [!NOTE]
> <span data-ttu-id="2cdca-157">控件状态与\_\_"视图状态隐藏窗体"字段中的视图状态一起保留。</span><span class="sxs-lookup"><span data-stu-id="2cdca-157">Control state is persisted along with the view state in the \_\_VIEWSTATE hidden form field.</span></span>

<span data-ttu-id="2cdca-158">此视频是视图状态和控制状态的演练。</span><span class="sxs-lookup"><span data-stu-id="2cdca-158">This video is a walkthrough of view state and control state.</span></span>

![](server-controls/_static/image1.png)

[<span data-ttu-id="2cdca-159">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="2cdca-159">Open Full-Screen Video</span></span>](server-controls/_static/state1.wmv)

<span data-ttu-id="2cdca-160">为了使服务器控件读取和写入以控制状态，必须执行三个步骤。</span><span class="sxs-lookup"><span data-stu-id="2cdca-160">In order for a server control to read and write to control state, you must take three steps.</span></span>

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a><span data-ttu-id="2cdca-161">第 1 步：调用寄存器需求控制状态方法</span><span class="sxs-lookup"><span data-stu-id="2cdca-161">Step 1: Call the RegisterRequiresControlState Method</span></span>

<span data-ttu-id="2cdca-162">注册需求控制状态方法ASP.NET通知控件需要保持控制状态。</span><span class="sxs-lookup"><span data-stu-id="2cdca-162">The RegisterRequiresControlState method informs ASP.NET that a control needs to persist control state.</span></span> <span data-ttu-id="2cdca-163">它采用类型控制（即正在注册的控件）的一个参数。</span><span class="sxs-lookup"><span data-stu-id="2cdca-163">It takes one argument of type Control which is the control that is being registered.</span></span>

<span data-ttu-id="2cdca-164">请务必注意，注册不会从请求持续到请求。</span><span class="sxs-lookup"><span data-stu-id="2cdca-164">It is important to note that registration does not persist from request to request.</span></span> <span data-ttu-id="2cdca-165">因此，如果控件要保留控制状态，则必须在每个请求上调用此方法。</span><span class="sxs-lookup"><span data-stu-id="2cdca-165">Therefore, this method must be called on every request if a control is to persist control state.</span></span> <span data-ttu-id="2cdca-166">建议在 OnInit 中调用该方法。</span><span class="sxs-lookup"><span data-stu-id="2cdca-166">It is recommended that the method be called in OnInit.</span></span>

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a><span data-ttu-id="2cdca-167">第 2 步：重写保存控制状态</span><span class="sxs-lookup"><span data-stu-id="2cdca-167">Step 2: Override SaveControlState</span></span>

<span data-ttu-id="2cdca-168">自上次回帖以来，SaveControlState 方法保存控件的控制状态更改。</span><span class="sxs-lookup"><span data-stu-id="2cdca-168">The SaveControlState method saves control state changes for a control since the last post back.</span></span> <span data-ttu-id="2cdca-169">它返回表示控件状态的对象。</span><span class="sxs-lookup"><span data-stu-id="2cdca-169">It returns an object representing the control's state.</span></span>

## <a name="step-3-override-loadcontrolstate"></a><span data-ttu-id="2cdca-170">步骤 3：覆盖负载控制状态</span><span class="sxs-lookup"><span data-stu-id="2cdca-170">Step 3: Override LoadControlState</span></span>

<span data-ttu-id="2cdca-171">LoadControlState 方法将保存的状态加载到控件中。</span><span class="sxs-lookup"><span data-stu-id="2cdca-171">The LoadControlState method loads saved state into a control.</span></span> <span data-ttu-id="2cdca-172">该方法采用一种类型 Object 的参数，该参数保存控件的保存状态。</span><span class="sxs-lookup"><span data-stu-id="2cdca-172">The method takes one argument of type Object which holds the saved state for the control.</span></span>

## <a name="full-xhtml-compliance"></a><span data-ttu-id="2cdca-173">完全 XHTML 合规性</span><span class="sxs-lookup"><span data-stu-id="2cdca-173">Full XHTML Compliance</span></span>

<span data-ttu-id="2cdca-174">任何 Web 开发人员都知道标准在 Web 应用程序中的重要性。</span><span class="sxs-lookup"><span data-stu-id="2cdca-174">Any Web developer knows the importance of standards in Web applications.</span></span> <span data-ttu-id="2cdca-175">为了维护基于标准的开发环境，ASP.NET 2.0 完全符合 XHTML 标准。</span><span class="sxs-lookup"><span data-stu-id="2cdca-175">In order to maintain a standards-based development environment, ASP.NET 2.0 is fully XHTML compliant.</span></span> <span data-ttu-id="2cdca-176">因此，所有标记都根据支持 HTML 4.0 或更高程度的浏览器中的 XHTML 标准进行呈现。</span><span class="sxs-lookup"><span data-stu-id="2cdca-176">Therefore, all tags are rendered according to XHTML standards in browsers that support HTML 4.0 or greater.</span></span>

<span data-ttu-id="2cdca-177">ASP.NET 1.1 中的 DOCTYPE 定义如下：</span><span class="sxs-lookup"><span data-stu-id="2cdca-177">The DOCTYPE definition in ASP.NET 1.1 was as follows:</span></span>

[!code-html[Main](server-controls/samples/sample6.html)]

<span data-ttu-id="2cdca-178">在 ASP.NET 2.0 中，默认的 DOCTYPE 定义如下所示：</span><span class="sxs-lookup"><span data-stu-id="2cdca-178">In ASP.NET 2.0, the default DOCTYPE definition is as follows:</span></span>

[!code-html[Main](server-controls/samples/sample7.html)]

<span data-ttu-id="2cdca-179">如果选择，您可以通过配置文件中的 xhtml 一致性节点更改默认 XHTML 合规性。</span><span class="sxs-lookup"><span data-stu-id="2cdca-179">If you choose, you can alter the default XHTML compliance via the xhtmlConformance node in the configuration file.</span></span> <span data-ttu-id="2cdca-180">例如，Web.config 文件中的以下节点将 XHTML 符合性更改为 XHTML 1.0 严格：</span><span class="sxs-lookup"><span data-stu-id="2cdca-180">For example, the following node in the web.config file will change XHTML compliance to XHTML 1.0 Strict:</span></span>

[!code-xml[Main](server-controls/samples/sample8.xml)]

<span data-ttu-id="2cdca-181">如果选择，还可以配置ASP.NET以使用 ASP.NET 1.x 中使用的旧配置，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2cdca-181">If you choose, you can also configure ASP.NET to use the legacy configuration used in ASP.NET 1.x as follows:</span></span>

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a><span data-ttu-id="2cdca-182">使用适配器进行自适应渲染</span><span class="sxs-lookup"><span data-stu-id="2cdca-182">Adaptive Rendering Using Adapters</span></span>

<span data-ttu-id="2cdca-183">在 ASP.NET 1.x 中，配置文件&lt;包含填充&gt;HttpBrowser 功能对象的浏览器Cap 节。</span><span class="sxs-lookup"><span data-stu-id="2cdca-183">In ASP.NET 1.x, the configuration file contained a &lt;browserCaps&gt; section that populated a HttpBrowserCapabilities object.</span></span> <span data-ttu-id="2cdca-184">此对象允许开发人员确定正在发出特定请求的设备并适当地呈现代码。</span><span class="sxs-lookup"><span data-stu-id="2cdca-184">This object allowed a developer to determine what device is making a particular request and render code appropriately.</span></span> <span data-ttu-id="2cdca-185">在 ASP.NET 2.0 中，模型已改进，现在使用新的 ControlAdapter 类。</span><span class="sxs-lookup"><span data-stu-id="2cdca-185">In ASP.NET 2.0, the model has improved and now uses the new ControlAdapter class.</span></span> <span data-ttu-id="2cdca-186">ControlAdapter 类覆盖控件生命周期中的事件，并控制基于用户代理功能的控件的呈现。</span><span class="sxs-lookup"><span data-stu-id="2cdca-186">The ControlAdapter class overrides events in the control's lifecycle and controls the rendering of controls based upon the user agent's capabilities.</span></span> <span data-ttu-id="2cdca-187">特定用户代理的功能由存储在 c：_windows_microsoft.net_framework_v2.0 中的浏览器定义文件（具有 .browser 文件扩展名的文件）定义。\* \* \*[CONFIG]浏览器\*文件夹。</span><span class="sxs-lookup"><span data-stu-id="2cdca-187">The capabilities of a specific user agent are defined by a browser definition file (a file with a .browser file extension) stored in the c:\windows\microsoft.net\framework\v2.0.\*\*\*\*\CONFIG\Browsers folder.</span></span>

> [!NOTE]
> <span data-ttu-id="2cdca-188">ControlAdapter 类是一个抽象类。</span><span class="sxs-lookup"><span data-stu-id="2cdca-188">The ControlAdapter class is an abstract class.</span></span>

<span data-ttu-id="2cdca-189">与 1.x 中的&lt;浏览器Cap&gt;节类似，浏览器定义文件使用正则表达式来分析用户代理字符串以标识请求的浏览器。</span><span class="sxs-lookup"><span data-stu-id="2cdca-189">Much like the &lt;browserCaps&gt; section in 1.x, the browser definition file uses a Regular Expression to parse the user agent string in order to identify the requesting browser.</span></span> <span data-ttu-id="2cdca-190">它们定义该用户代理的特定功能。</span><span class="sxs-lookup"><span data-stu-id="2cdca-190">It them defines particular capabilities for that user agent.</span></span> <span data-ttu-id="2cdca-191">控件适配器通过渲染方法呈现控件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-191">The ControlAdapter renders the control via the Render method.</span></span> <span data-ttu-id="2cdca-192">因此，如果重写 Render 方法，则不应在基类上调用 Render。</span><span class="sxs-lookup"><span data-stu-id="2cdca-192">Therefore, if you override the Render method, you should not call Render on the base class.</span></span> <span data-ttu-id="2cdca-193">这样做可能会导致渲染发生两次，一次用于适配器，一次用于控件本身。</span><span class="sxs-lookup"><span data-stu-id="2cdca-193">Doing so may cause rendering to occur twice, once for the adapter and once for the control itself.</span></span>

## <a name="developing-a-custom-adapter"></a><span data-ttu-id="2cdca-194">开发自定义适配器</span><span class="sxs-lookup"><span data-stu-id="2cdca-194">Developing a Custom Adapter</span></span>

<span data-ttu-id="2cdca-195">您可以通过从 ControlAdapter 继承来开发自己的自定义适配器。</span><span class="sxs-lookup"><span data-stu-id="2cdca-195">You can develop your own custom adapter by inheriting from ControlAdapter.</span></span> <span data-ttu-id="2cdca-196">此外，在页面需要适配器的情况下，可以从抽象类 PageAdapter 继承。</span><span class="sxs-lookup"><span data-stu-id="2cdca-196">Additionally, you can inherit from the abstract class PageAdapter in cases where an adapter is needed for a page.</span></span> <span data-ttu-id="2cdca-197">控件映射到自定义适配器是通过浏览器定义文件中的&lt;控件适配器&gt;元素完成的。</span><span class="sxs-lookup"><span data-stu-id="2cdca-197">Mapping of controls to your custom adapter is accomplished via the &lt;controlAdapters&gt; element in the browser definition file.</span></span> <span data-ttu-id="2cdca-198">例如，浏览器定义文件中的以下 XML 将菜单控件映射到 MenuAdapter 类：</span><span class="sxs-lookup"><span data-stu-id="2cdca-198">For example, the following XML from a browser definition file maps the Menu control to the MenuAdapter class:</span></span>

[!code-html[Main](server-controls/samples/sample10.html)]

<span data-ttu-id="2cdca-199">使用此模型，控件开发人员很容易定位特定设备或浏览器。</span><span class="sxs-lookup"><span data-stu-id="2cdca-199">Using this model, it becomes quite easy for a control developer to target a particular device or browser.</span></span> <span data-ttu-id="2cdca-200">对于开发人员来说，完全控制每个设备上的页面呈现方式也非常简单。</span><span class="sxs-lookup"><span data-stu-id="2cdca-200">It's also quite simple for a developer to have complete control over how pages render on every device.</span></span>

## <a name="per-device-rendering"></a><span data-ttu-id="2cdca-201">每设备渲染</span><span class="sxs-lookup"><span data-stu-id="2cdca-201">Per-Device Rendering</span></span>

<span data-ttu-id="2cdca-202">ASP.NET 2.0 中的服务器控件属性可以使用特定于浏览器的前缀按设备指定。</span><span class="sxs-lookup"><span data-stu-id="2cdca-202">Server control properties in ASP.NET 2.0 can be specified per-device using a browser-specific prefix.</span></span> <span data-ttu-id="2cdca-203">例如，下面的代码将更改标签的文本，具体取决于用于浏览页面的设备。</span><span class="sxs-lookup"><span data-stu-id="2cdca-203">For example, the code below will change the Text of a label depending upon which device is being used to browse the page.</span></span>

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

<span data-ttu-id="2cdca-204">当包含此标签的页面从 Internet Explorer 浏览时，标签将显示文本，上面写着"您正在从 Internet 资源管理器浏览"。</span><span class="sxs-lookup"><span data-stu-id="2cdca-204">When the page containing this label is browsed from Internet Explorer, the label will display text saying "You are browsing from Internet Explorer."</span></span> <span data-ttu-id="2cdca-205">当从 Firefox 浏览页面时，标签将显示文本"您正在从 Firefox 浏览"。</span><span class="sxs-lookup"><span data-stu-id="2cdca-205">When the page is browsed from Firefox, the label will display the text "You are browsing from Firefox."</span></span> <span data-ttu-id="2cdca-206">从任何其他设备浏览页面时，将显示"您正在从未知设备浏览"。</span><span class="sxs-lookup"><span data-stu-id="2cdca-206">When the page is browsed from any other device, it will display "You are browsing from an unknown device."</span></span> <span data-ttu-id="2cdca-207">可以使用此特殊语法指定任何属性。</span><span class="sxs-lookup"><span data-stu-id="2cdca-207">Any property can be specified using this special syntax.</span></span>

## <a name="setting-focus"></a><span data-ttu-id="2cdca-208">设置焦点</span><span class="sxs-lookup"><span data-stu-id="2cdca-208">Setting Focus</span></span>

<span data-ttu-id="2cdca-209">ASP.NET 1.x 开发人员经常询问如何将初始焦点放在特定控件上。</span><span class="sxs-lookup"><span data-stu-id="2cdca-209">ASP.NET 1.x developers frequently asked about how to set initial focus on a particular control.</span></span> <span data-ttu-id="2cdca-210">例如，在登录页上，让用户 ID 文本框在页面首次加载时获取焦点非常有用。</span><span class="sxs-lookup"><span data-stu-id="2cdca-210">For example, on a login page, it's useful to have the User ID textbox get the focus when the page first loads.</span></span> <span data-ttu-id="2cdca-211">在ASP.NET 1.x 中，执行此操作需要编写一些客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="2cdca-211">In ASP.NET 1.x, doing this required writing some client-side script.</span></span> <span data-ttu-id="2cdca-212">尽管此类脚本是一项琐碎的任务，但由于 SetFocus 方法，ASP.NET 2.0 中不再需要它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-212">Even though such a script is a trivial task, it's no longer necessary in ASP.NET 2.0 thanks to the SetFocus method.</span></span> <span data-ttu-id="2cdca-213">SetFocus 方法采用一个参数，指示应接收焦点的控件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-213">The SetFocus method takes one argument indicating the control that should receive focus.</span></span> <span data-ttu-id="2cdca-214">此参数可以是控件的客户端 ID 作为字符串，也可以是 Server 控件的名称作为控件对象。</span><span class="sxs-lookup"><span data-stu-id="2cdca-214">This argument can either be the client ID of the control as a string or the name of the Server control as a Control object.</span></span> <span data-ttu-id="2cdca-215">例如，要将初始焦点设置为页面首次加载时称为 txtUserID 的 TextBox 控件，请向页面\_加载添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="2cdca-215">For example, to set the initial focus to a TextBox control called txtUserID when the page first loads, add the following code to Page\_Load:</span></span>

[!code-csharp[Main](server-controls/samples/sample12.cs)]

<span data-ttu-id="2cdca-216">- 或</span><span class="sxs-lookup"><span data-stu-id="2cdca-216">-- or</span></span>

[!code-csharp[Main](server-controls/samples/sample13.cs)]

<span data-ttu-id="2cdca-217">ASP.NET 2.0 使用 Webresource.axd 处理程序（前面讨论）来呈现设置焦点的客户端函数。</span><span class="sxs-lookup"><span data-stu-id="2cdca-217">ASP.NET 2.0 uses the Webresource.axd handler (discussed previously) to render a client-side function that sets the focus.</span></span> <span data-ttu-id="2cdca-218">客户端函数的名称是 WebForm\_自动焦点，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2cdca-218">The name of the client-side function is WebForm\_AutoFocus as shown here:</span></span>

[!code-html[Main](server-controls/samples/sample14.html)]

<span data-ttu-id="2cdca-219">或者，可以使用控件的 Focus 方法将初始焦点设置为该控件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-219">Alternatively, you can use the Focus method for a control to set the initial focus to that control.</span></span> <span data-ttu-id="2cdca-220">Focus 方法派生自 Control 类，可用于所有ASP.NET 2.0 控件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-220">The Focus method derives from the Control class and is available to all ASP.NET 2.0 controls.</span></span> <span data-ttu-id="2cdca-221">当发生验证错误时，还可以将焦点设置为特定控件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-221">It is also possible to set focus to a particular control when a validation error occurs.</span></span> <span data-ttu-id="2cdca-222">稍后将介绍这一点。</span><span class="sxs-lookup"><span data-stu-id="2cdca-222">That will be covered in a later module.</span></span>

## <a name="new-server-controls-in-aspnet-20"></a><span data-ttu-id="2cdca-223">ASP.NET 2.0 中的新服务器控件</span><span class="sxs-lookup"><span data-stu-id="2cdca-223">New Server Controls in ASP.NET 2.0</span></span>

<span data-ttu-id="2cdca-224">以下是 ASP.NET 2.0 中的新服务器控件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-224">The following are new server controls in ASP.NET 2.0.</span></span> <span data-ttu-id="2cdca-225">我们将在后面的模块中更详细地介绍其中一些内容。</span><span class="sxs-lookup"><span data-stu-id="2cdca-225">We will go into more detail on some of them in later modules.</span></span>

## <a name="imagemap-control"></a><span data-ttu-id="2cdca-226">图像映射控件</span><span class="sxs-lookup"><span data-stu-id="2cdca-226">ImageMap Control</span></span>

<span data-ttu-id="2cdca-227">ImageMap 控件允许您向图像添加热点，该图像可以启动帖子或导航到 URL。</span><span class="sxs-lookup"><span data-stu-id="2cdca-227">The ImageMap control allows you to add hotspots to an image that can initiate a post back or navigate to a URL.</span></span> <span data-ttu-id="2cdca-228">有三种类型的热点可用;圆热点、矩形热点和多边形热点。</span><span class="sxs-lookup"><span data-stu-id="2cdca-228">There are three types of hotspots available; CircleHotSpot, RectangleHotSpot, and PolygonHotSpot.</span></span> <span data-ttu-id="2cdca-229">热点通过 Visual Studio 中的集合编辑器添加，或在代码中以编程方式添加。</span><span class="sxs-lookup"><span data-stu-id="2cdca-229">Hotspots are added via a collection editor in Visual Studio or programmatically in code.</span></span> <span data-ttu-id="2cdca-230">没有可用于在图像上绘制热点的用户界面。</span><span class="sxs-lookup"><span data-stu-id="2cdca-230">There is no user-interface available for drawing hotspots on an image.</span></span> <span data-ttu-id="2cdca-231">必须声明性地指定热点的坐标、大小或半径。</span><span class="sxs-lookup"><span data-stu-id="2cdca-231">The coordinates and size or radius of the hotspot must be specified declaratively.</span></span> <span data-ttu-id="2cdca-232">设计器中也没有热点的可视表示形式。</span><span class="sxs-lookup"><span data-stu-id="2cdca-232">There is also no visual representation of a hotspot in the designer.</span></span> <span data-ttu-id="2cdca-233">如果热点配置为导航到 URL，则 URL 将通过热点的 NavigateUrl 属性指定。</span><span class="sxs-lookup"><span data-stu-id="2cdca-233">If a hotspot is configured to navigate to a URL, the URL is specified via the NavigateUrl property of the hotspot.</span></span> <span data-ttu-id="2cdca-234">在后回热点的情况下，PostBackValue 属性允许您传递后回的字符串，该字符串可以在服务器端代码中检索。</span><span class="sxs-lookup"><span data-stu-id="2cdca-234">In the case of a post back hotspot, the PostBackValue property allows you to pass a string in the post back that can be retrieved in server-side code.</span></span>

![可视化工作室中的热点集合编辑器](server-controls/_static/image1.jpg)

<span data-ttu-id="2cdca-236">**图 1**： 可视化工作室中的热点集合编辑器</span><span class="sxs-lookup"><span data-stu-id="2cdca-236">**Figure 1**: HotSpot Collection Editor in Visual Studio</span></span>

## <a name="bulletedlist-control"></a><span data-ttu-id="2cdca-237">项目符号列表控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-237">BulletedList Control</span></span>

<span data-ttu-id="2cdca-238">"项目符号列表"控件是一个项目符号列表，可以轻松绑定数据。</span><span class="sxs-lookup"><span data-stu-id="2cdca-238">The BulletedList control is a bulleted list that can easily be data bound.</span></span> <span data-ttu-id="2cdca-239">列表可以通过"项目符号样式"属性排序（编号）或无序排序。</span><span class="sxs-lookup"><span data-stu-id="2cdca-239">The list can be ordered (numbered) or unordered via the BulletStyle property.</span></span> <span data-ttu-id="2cdca-240">列表中的每个项都由 ListItem 对象表示。</span><span class="sxs-lookup"><span data-stu-id="2cdca-240">Each item in the list is represented by a ListItem object.</span></span>

![可视化工作室中的项目符号列表控制](server-controls/_static/image1.gif)

<span data-ttu-id="2cdca-242">**图 2**： 可视化工作室中的项目列表控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-242">**Figure 2**: BulletedList Control in Visual Studio</span></span>

## <a name="hiddenfield-control"></a><span data-ttu-id="2cdca-243">隐藏字段控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-243">HiddenField Control</span></span>

<span data-ttu-id="2cdca-244">HiddenField 控件向页面添加隐藏表单字段，其值在服务器端代码中可用。</span><span class="sxs-lookup"><span data-stu-id="2cdca-244">The HiddenField control adds a hidden form field to your page, the value of which is available in server-side code.</span></span> <span data-ttu-id="2cdca-245">隐藏窗体字段的值通常预计在后背之间保持不变。</span><span class="sxs-lookup"><span data-stu-id="2cdca-245">The value of a hidden form field is generally expected to remain unchanged between post backs.</span></span> <span data-ttu-id="2cdca-246">但是，恶意用户可能会在回发布之前更改该值。</span><span class="sxs-lookup"><span data-stu-id="2cdca-246">However, it is possible for a malicious user to change the value prior to post back.</span></span> <span data-ttu-id="2cdca-247">如果发生这种情况，"隐藏字段"控件将引发"值更改"事件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-247">If this happens, the HiddenField control will raise the ValueChanged event.</span></span> <span data-ttu-id="2cdca-248">如果在 HiddenField 控件中具有敏感信息，并且希望确保信息保持不变，则应在代码中处理 Value"更改"事件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-248">If you have sensitive information in the HiddenField control and you want to ensure that it remains unchanged, you should handle the ValueChanged event in your code.</span></span>

## <a name="fileupload-control"></a><span data-ttu-id="2cdca-249">文件上传控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-249">FileUpload Control</span></span>

<span data-ttu-id="2cdca-250">ASP.NET 2.0 中的 FileUpload 控件使得可以通过ASP.NET页面将文件上载到 Web 服务器成为可能。</span><span class="sxs-lookup"><span data-stu-id="2cdca-250">The FileUpload control in ASP.NET 2.0 makes it possible to upload files to a Web server via an ASP.NET page.</span></span> <span data-ttu-id="2cdca-251">此控件与 ASP.NET 1.x HtmlInputFile 类非常相似，但有一些例外。</span><span class="sxs-lookup"><span data-stu-id="2cdca-251">This control is quite similar to the ASP.NET 1.x HtmlInputFile class with a few exceptions.</span></span> <span data-ttu-id="2cdca-252">在 ASP.NET 1.x 中，建议将"已发布文件"属性检查为 null，以确定您是否具有良好的文件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-252">In ASP.NET 1.x, it was recommended that the PostedFile property be checked for null in order to determine if you had a good file.</span></span> <span data-ttu-id="2cdca-253">ASP.NET 2.0 中的 FileUpload 控件添加了一个新的 HasFile 属性，您可以将其用于同一目的，并且效率更高一些。</span><span class="sxs-lookup"><span data-stu-id="2cdca-253">The FileUpload control in ASP.NET 2.0 adds a new HasFile property that you can use for the same purpose and it's a bit more efficient.</span></span>

<span data-ttu-id="2cdca-254">已发布文件属性仍可用于访问 HttpPostedFile 对象，但 HttpPostedFile 的某些功能现在可通过 FileUpload 控件在本质上可用。</span><span class="sxs-lookup"><span data-stu-id="2cdca-254">The PostedFile property is still available for access to an HttpPostedFile object, but some of the functionality of the HttpPostedFile is now available intrinsically with the FileUpload control.</span></span> <span data-ttu-id="2cdca-255">例如，要将上载的文件保存在 ASP.NET 1.x 中，请调用 HttpPostedFile 对象上的 SaveAs 方法。</span><span class="sxs-lookup"><span data-stu-id="2cdca-255">For example, to save an uploaded file in ASP.NET 1.x, you call the SaveAs method on the HttpPostedFile object.</span></span> <span data-ttu-id="2cdca-256">使用 ASP.NET 2.0 中的 FileUpload 控件，您将在 FileUpload 控件本身上调用 SaveAs 方法。</span><span class="sxs-lookup"><span data-stu-id="2cdca-256">Using the FileUpload control in ASP.NET 2.0, you would call the SaveAs method on the FileUpload control itself.</span></span>

<span data-ttu-id="2cdca-257">2.0 行为（可能是最重要的更改）的另一个重要变化是，在保存整个上载的文件之前，不再需要将整个上载的文件加载到内存中。</span><span class="sxs-lookup"><span data-stu-id="2cdca-257">Another significant change in the 2.0 behavior (and likely the most significant change) is that it is no longer necessary to load an entire uploaded file into memory before saving it.</span></span> <span data-ttu-id="2cdca-258">在 1.x 中，上载的任何文件在写入磁盘之前都完全保存到内存中。</span><span class="sxs-lookup"><span data-stu-id="2cdca-258">In 1.x, any file that was uploaded is saved entirely into memory prior to being written to disk.</span></span> <span data-ttu-id="2cdca-259">此体系结构可防止上载大型文件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-259">This architecture prevents the upload of large files.</span></span>

<span data-ttu-id="2cdca-260">在 ASP.NET 2.0 中，httpRuntime 元素的请求长度磁盘阈值属性允许您配置在写入磁盘之前在内存中存储缓冲区中的数量。</span><span class="sxs-lookup"><span data-stu-id="2cdca-260">In ASP.NET 2.0, the requestLengthDiskThreshold attribute of the httpRuntime element allows you to configure how many Kilobytes are held in a buffer in memory prior to being written to disk.</span></span>

<span data-ttu-id="2cdca-261">**重要提示**：MSDN 文档（和其他地方的文档）指定此值以字节为单位（不是千字节），默认值为 256。</span><span class="sxs-lookup"><span data-stu-id="2cdca-261">**IMPORTANT**: MSDN documentation (and documentation elsewhere) specifies that this value is in bytes (not Kilobytes) and that the default is 256.</span></span> <span data-ttu-id="2cdca-262">该值实际上以千字节为单位指定，默认值为 80。</span><span class="sxs-lookup"><span data-stu-id="2cdca-262">The value is actually specified in Kilobytes and the default value is 80.</span></span> <span data-ttu-id="2cdca-263">通过默认值 80K，我们确保缓冲区不会最终位于大型对象堆上。</span><span class="sxs-lookup"><span data-stu-id="2cdca-263">By having a default value of 80K, we ensure that the buffer does not end up on the large object heap.</span></span>

## <a name="wizard-control"></a><span data-ttu-id="2cdca-264">向导控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-264">Wizard Control</span></span>

<span data-ttu-id="2cdca-265">遇到ASP.NET开发人员在尝试使用面板在一系列"页面"中收集信息或从一个页面传输到一个页面时遇到这样的常见情况。</span><span class="sxs-lookup"><span data-stu-id="2cdca-265">It is fairly common to encounter ASP.NET developers struggling with attempting to gather information in a series of "pages" using panels or by transferring from page to page.</span></span> <span data-ttu-id="2cdca-266">很多时候，这种努力是令人沮丧的，而且非常耗时。</span><span class="sxs-lookup"><span data-stu-id="2cdca-266">More often than not, the endeavor is a frustrating one and is time consuming.</span></span> <span data-ttu-id="2cdca-267">新的向导控件通过在用户熟悉的向导界面中允许线性和非线性步骤来解决问题。</span><span class="sxs-lookup"><span data-stu-id="2cdca-267">The new Wizard control solves the problems by allowing for linear and non-linear steps in a wizard interface that users are familiar with.</span></span> <span data-ttu-id="2cdca-268">向导控件以一系列步骤显示输入窗体。</span><span class="sxs-lookup"><span data-stu-id="2cdca-268">The Wizard control presents input forms in a series of steps.</span></span> <span data-ttu-id="2cdca-269">每个步骤都是控件的 StepType 属性指定的特定类型。</span><span class="sxs-lookup"><span data-stu-id="2cdca-269">Each step is of a particular type specified by the StepType property of the control.</span></span> <span data-ttu-id="2cdca-270">可用的步骤类型如下：</span><span class="sxs-lookup"><span data-stu-id="2cdca-270">The available step types are as follows:</span></span>

| <span data-ttu-id="2cdca-271">**步长类型**</span><span class="sxs-lookup"><span data-stu-id="2cdca-271">**Step Type**</span></span> | <span data-ttu-id="2cdca-272">**说明**</span><span class="sxs-lookup"><span data-stu-id="2cdca-272">**Explanation**</span></span> |
| --- | --- |
| <span data-ttu-id="2cdca-273">自动</span><span class="sxs-lookup"><span data-stu-id="2cdca-273">Auto</span></span> | <span data-ttu-id="2cdca-274">向导根据步骤层次结构中的位置自动确定步骤的类型。</span><span class="sxs-lookup"><span data-stu-id="2cdca-274">The wizard automatically determines the type of step based upon its position within the step hierarchy.</span></span> |
| <span data-ttu-id="2cdca-275">开始</span><span class="sxs-lookup"><span data-stu-id="2cdca-275">Start</span></span> | <span data-ttu-id="2cdca-276">第一步，通常用于提出介绍性陈述。</span><span class="sxs-lookup"><span data-stu-id="2cdca-276">The first step, often used to present an introductory statement.</span></span> |
| <span data-ttu-id="2cdca-277">步骤</span><span class="sxs-lookup"><span data-stu-id="2cdca-277">Step</span></span> | <span data-ttu-id="2cdca-278">正常步骤。</span><span class="sxs-lookup"><span data-stu-id="2cdca-278">A normal step.</span></span> |
| <span data-ttu-id="2cdca-279">完成</span><span class="sxs-lookup"><span data-stu-id="2cdca-279">Finish</span></span> | <span data-ttu-id="2cdca-280">最后一步，通常用于显示一个按钮来完成向导。</span><span class="sxs-lookup"><span data-stu-id="2cdca-280">The final step, usually used to present a button to finish the wizard.</span></span> |
| <span data-ttu-id="2cdca-281">完成</span><span class="sxs-lookup"><span data-stu-id="2cdca-281">Complete</span></span> | <span data-ttu-id="2cdca-282">显示传达成功或失败的信息。</span><span class="sxs-lookup"><span data-stu-id="2cdca-282">Presents a message communicating success or failure.</span></span> |

> [!NOTE]
> <span data-ttu-id="2cdca-283">向导控件使用ASP.NET控制状态跟踪其状态。</span><span class="sxs-lookup"><span data-stu-id="2cdca-283">The Wizard control keeps track of its state using ASP.NET control state.</span></span> <span data-ttu-id="2cdca-284">因此，启用视图状态属性可以设置为 false，而不会造成任何损害。</span><span class="sxs-lookup"><span data-stu-id="2cdca-284">Therefore, the EnableViewState property can be set to false without any detriment.</span></span>

<span data-ttu-id="2cdca-285">此视频是向导控件的演练。</span><span class="sxs-lookup"><span data-stu-id="2cdca-285">This video is a walkthrough of the Wizard control.</span></span>

![](server-controls/_static/image2.png)

[<span data-ttu-id="2cdca-286">打开全屏视频</span><span class="sxs-lookup"><span data-stu-id="2cdca-286">Open Full-Screen Video</span></span>](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a><span data-ttu-id="2cdca-287">本地化控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-287">Localize Control</span></span>

<span data-ttu-id="2cdca-288">本地化控件类似于文本控件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-288">The Localize control is similar to a Literal control.</span></span> <span data-ttu-id="2cdca-289">但是，本地化控件具有一个**Mode**属性，用于控制如何向其添加标记。</span><span class="sxs-lookup"><span data-stu-id="2cdca-289">However, the Localize control has a **Mode** property that controls how markup that is added to it is rendered.</span></span> <span data-ttu-id="2cdca-290">Mode 属性支持以下值：</span><span class="sxs-lookup"><span data-stu-id="2cdca-290">The Mode property supports the following values:</span></span>

| <span data-ttu-id="2cdca-291">**模式**</span><span class="sxs-lookup"><span data-stu-id="2cdca-291">**Mode**</span></span> | <span data-ttu-id="2cdca-292">**说明**</span><span class="sxs-lookup"><span data-stu-id="2cdca-292">**Explanation**</span></span> |
| --- | --- |
| <span data-ttu-id="2cdca-293">转换</span><span class="sxs-lookup"><span data-stu-id="2cdca-293">Transform</span></span> | <span data-ttu-id="2cdca-294">标记根据发出请求的浏览器的协议进行转换。</span><span class="sxs-lookup"><span data-stu-id="2cdca-294">Markup is transformed according to the protocol of the browser making the request.</span></span> |
| <span data-ttu-id="2cdca-295">直通</span><span class="sxs-lookup"><span data-stu-id="2cdca-295">PassThrough</span></span> | <span data-ttu-id="2cdca-296">标记将呈现为"正样"。</span><span class="sxs-lookup"><span data-stu-id="2cdca-296">Markup is rendered as-is.</span></span> |
| <span data-ttu-id="2cdca-297">编码</span><span class="sxs-lookup"><span data-stu-id="2cdca-297">Encode</span></span> | <span data-ttu-id="2cdca-298">添加到控件的标记使用 HtmlEncode 进行编码。</span><span class="sxs-lookup"><span data-stu-id="2cdca-298">Markup that is added to the control is encoded using HtmlEncode.</span></span> |

## <a name="multiview-and-view-controls"></a><span data-ttu-id="2cdca-299">多视图和视图控件</span><span class="sxs-lookup"><span data-stu-id="2cdca-299">MultiView and View Controls</span></span>

<span data-ttu-id="2cdca-300">MultiView 控件充当视图控件的容器，视图控件充当其他控件的容器（与面板控件类似）。</span><span class="sxs-lookup"><span data-stu-id="2cdca-300">The MultiView control acts as a container for View controls, and the View control acts as a container (much like a Panel control) for other controls.</span></span> <span data-ttu-id="2cdca-301">MultiView 控件中的每个视图都由单个视图控件表示。</span><span class="sxs-lookup"><span data-stu-id="2cdca-301">Each view in a MultiView control is represented by a single View control.</span></span> <span data-ttu-id="2cdca-302">MultiView 中的第一个视图控件是视图 0，第二个视图 1 等。您可以通过指定 MultiView 控件的 ActiveViewIndex 来切换视图。</span><span class="sxs-lookup"><span data-stu-id="2cdca-302">The first View control in the MultiView is view 0, the second is view 1, etc. You can switch views by specifying the ActiveViewIndex of the MultiView control.</span></span>

## <a name="substitution-control"></a><span data-ttu-id="2cdca-303">替代控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-303">Substitution Control</span></span>

<span data-ttu-id="2cdca-304">替换控件与ASP.NET缓存一起使用。</span><span class="sxs-lookup"><span data-stu-id="2cdca-304">The Substitution control is used in conjunction with ASP.NET caching.</span></span> <span data-ttu-id="2cdca-305">如果要利用缓存，但具有必须在每个请求上更新页面的某些部分（换句话说，免除缓存的页面部分），则替换组件提供了一个很好的解决方案。</span><span class="sxs-lookup"><span data-stu-id="2cdca-305">In cases where you want to take advantage of caching, but you have portions of a page that must be updated on each request (in other words, portions of a page that are exempt from caching), the Substitution component provides a great solution.</span></span> <span data-ttu-id="2cdca-306">控件实际上不会自行呈现任何输出。</span><span class="sxs-lookup"><span data-stu-id="2cdca-306">The control doesn't actually render any output on its own.</span></span> <span data-ttu-id="2cdca-307">相反，它绑定到服务器端代码中的方法。</span><span class="sxs-lookup"><span data-stu-id="2cdca-307">Instead, it is bound to a method in server-side code.</span></span> <span data-ttu-id="2cdca-308">请求页面时，将调用该方法，并呈现返回的标记来代替替换控件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-308">When the page is requested, the method is called and the returned markup is rendered in place of the substitution control.</span></span>

<span data-ttu-id="2cdca-309">通过**MethodName**属性指定替换控件绑定到的方法。</span><span class="sxs-lookup"><span data-stu-id="2cdca-309">The method to which the Substitution control is bound is specified via the **MethodName** property.</span></span> <span data-ttu-id="2cdca-310">该方法必须满足以下条件：</span><span class="sxs-lookup"><span data-stu-id="2cdca-310">That method must meet the following criteria:</span></span>

- <span data-ttu-id="2cdca-311">它必须是静态（在 VB 中共享）方法。</span><span class="sxs-lookup"><span data-stu-id="2cdca-311">It must be a static (shared in VB) method.</span></span>
- <span data-ttu-id="2cdca-312">它接受 HttpContext 类型的一个参数。</span><span class="sxs-lookup"><span data-stu-id="2cdca-312">It accepts one parameter of type HttpContext.</span></span>
- <span data-ttu-id="2cdca-313">它返回一个字符串，表示应替换页面上的控件的标记。</span><span class="sxs-lookup"><span data-stu-id="2cdca-313">It returns a string representing the markup that should replace the control on the page.</span></span>

<span data-ttu-id="2cdca-314">替换控件无法修改页面上的任何其他控件，但它确实可以通过其参数访问当前 HttpContext。</span><span class="sxs-lookup"><span data-stu-id="2cdca-314">The Substitution control does not have the ability to modify any other control on the page, but it does have access to the current HttpContext via its parameter.</span></span>

## <a name="gridview-control"></a><span data-ttu-id="2cdca-315">网格视图控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-315">GridView Control</span></span>

<span data-ttu-id="2cdca-316">GridView 控件是 DataGrid 控件的替换。</span><span class="sxs-lookup"><span data-stu-id="2cdca-316">The GridView control is the replacement for the DataGrid control.</span></span> <span data-ttu-id="2cdca-317">此控件将在后面的模块中更详细地介绍。</span><span class="sxs-lookup"><span data-stu-id="2cdca-317">This control will be covered in more detail in a later module.</span></span>

## <a name="detailsview-control"></a><span data-ttu-id="2cdca-318">详细信息查看控件</span><span class="sxs-lookup"><span data-stu-id="2cdca-318">DetailsView Control</span></span>

<span data-ttu-id="2cdca-319">"详细信息视图"控件允许您从数据源显示单个记录，并对其进行编辑或删除。</span><span class="sxs-lookup"><span data-stu-id="2cdca-319">The DetailsView control allows you to display a single record from a data source and to edit or delete it.</span></span> <span data-ttu-id="2cdca-320">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-320">It is covered in more detail in a later module.</span></span>

## <a name="formview-control"></a><span data-ttu-id="2cdca-321">窗体视图控件</span><span class="sxs-lookup"><span data-stu-id="2cdca-321">FormView Control</span></span>

<span data-ttu-id="2cdca-322">FormView 控件用于在可配置的界面中显示来自数据源的单个记录。</span><span class="sxs-lookup"><span data-stu-id="2cdca-322">The FormView control is used to display a single record from a datasource in a configurable interface.</span></span> <span data-ttu-id="2cdca-323">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-323">It is covered in more detail in a later module.</span></span>

## <a name="accessdatasource-control"></a><span data-ttu-id="2cdca-324">访问数据源控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-324">AccessDataSource Control</span></span>

<span data-ttu-id="2cdca-325">AccessDataSource 控件用于数据绑定 Access 数据库。</span><span class="sxs-lookup"><span data-stu-id="2cdca-325">The AccessDataSource control is used to data bind an Access database.</span></span> <span data-ttu-id="2cdca-326">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-326">It is covered in more detail in a later module.</span></span>

## <a name="objectdatasource-control"></a><span data-ttu-id="2cdca-327">对象数据源控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-327">ObjectDataSource Control</span></span>

<span data-ttu-id="2cdca-328">ObjectDataSource 控件用于支持三层体系结构，以便控件可以将数据绑定到中间层业务对象，而不是控件直接绑定到数据源的双层模型。</span><span class="sxs-lookup"><span data-stu-id="2cdca-328">The ObjectDataSource control is used to support a three-tier architecture so that controls can be data-bound to a middle-tier business object as opposed to a two-tiered model where controls are bound directly to the data source.</span></span> <span data-ttu-id="2cdca-329">稍后将在后面的模块中更详细地讨论它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-329">It will be discussed in more detail in a later module.</span></span>

## <a name="xmldatasource-control"></a><span data-ttu-id="2cdca-330">XmlDataSource 控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-330">XmlDataSource Control</span></span>

<span data-ttu-id="2cdca-331">XmlDataSource 控件用于绑定到 XML 数据源的数据。</span><span class="sxs-lookup"><span data-stu-id="2cdca-331">The XmlDataSource control is used to data bind to an XML data source.</span></span> <span data-ttu-id="2cdca-332">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-332">It is covered in more detail in a later module.</span></span>

## <a name="sitemapdatasource-control"></a><span data-ttu-id="2cdca-333">站点映射数据源控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-333">SiteMapDataSource Control</span></span>

<span data-ttu-id="2cdca-334">SiteMapDataSource 控件基于站点地图为站点导航控件提供数据绑定。</span><span class="sxs-lookup"><span data-stu-id="2cdca-334">The SiteMapDataSource control provides data binding for site navigation controls based on a site map.</span></span> <span data-ttu-id="2cdca-335">稍后将在后面的模块中更详细地讨论它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-335">It will be discussed in more detail in a later module.</span></span>

## <a name="sitemappath-control"></a><span data-ttu-id="2cdca-336">站点地图路径控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-336">SiteMapPath Control</span></span>

<span data-ttu-id="2cdca-337">SiteMapPath 控件显示一系列导航链接，通常称为痕迹。</span><span class="sxs-lookup"><span data-stu-id="2cdca-337">The SiteMapPath control displays a series of navigation links commonly referred to as breadcrumbs.</span></span> <span data-ttu-id="2cdca-338">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-338">It is covered in more detail in a later module.</span></span>

## <a name="menu-control"></a><span data-ttu-id="2cdca-339">Menu 控件</span><span class="sxs-lookup"><span data-stu-id="2cdca-339">Menu Control</span></span>

<span data-ttu-id="2cdca-340">"菜单"控件使用 DHTML 显示动态菜单。</span><span class="sxs-lookup"><span data-stu-id="2cdca-340">The Menu control displays dynamic menus using DHTML.</span></span> <span data-ttu-id="2cdca-341">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-341">It is covered in more detail in a later module.</span></span>

## <a name="treeview-control"></a><span data-ttu-id="2cdca-342">TreeView 控件</span><span class="sxs-lookup"><span data-stu-id="2cdca-342">TreeView Control</span></span>

<span data-ttu-id="2cdca-343">TreeView 控件用于显示数据的分层树视图。</span><span class="sxs-lookup"><span data-stu-id="2cdca-343">The TreeView control is used to display a hierarchical tree view of data.</span></span> <span data-ttu-id="2cdca-344">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-344">It is covered in more detail in a later module.</span></span>

## <a name="login-control"></a><span data-ttu-id="2cdca-345">登录控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-345">Login Control</span></span>

<span data-ttu-id="2cdca-346">登录控件提供了登录到网站的机制。</span><span class="sxs-lookup"><span data-stu-id="2cdca-346">The Login control provides for a mechanism to log into a Web site.</span></span> <span data-ttu-id="2cdca-347">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-347">It is covered in more detail in a later module.</span></span>

## <a name="loginview-control"></a><span data-ttu-id="2cdca-348">LoginView 控件</span><span class="sxs-lookup"><span data-stu-id="2cdca-348">LoginView Control</span></span>

<span data-ttu-id="2cdca-349">登录视图控件允许根据用户的登录状态显示不同的模板。</span><span class="sxs-lookup"><span data-stu-id="2cdca-349">The LoginView control allows for the display of different templates based upon a user's login status.</span></span> <span data-ttu-id="2cdca-350">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-350">It is covered in more detail in a later module.</span></span>

## <a name="passwordrecovery-control"></a><span data-ttu-id="2cdca-351">密码恢复控制</span><span class="sxs-lookup"><span data-stu-id="2cdca-351">PasswordRecovery Control</span></span>

<span data-ttu-id="2cdca-352">密码恢复控件用于检索ASP.NET应用程序的用户忘记的密码。</span><span class="sxs-lookup"><span data-stu-id="2cdca-352">The PasswordRecovery control is used to retrieve forgotten passwords by users of an ASP.NET application.</span></span> <span data-ttu-id="2cdca-353">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-353">It is covered in more detail in a later module.</span></span>

## <a name="loginstatus"></a><span data-ttu-id="2cdca-354">LoginStatus</span><span class="sxs-lookup"><span data-stu-id="2cdca-354">LoginStatus</span></span>

<span data-ttu-id="2cdca-355">登录状态控件显示用户的登录状态。</span><span class="sxs-lookup"><span data-stu-id="2cdca-355">The LoginStatus control displays a user's login status.</span></span> <span data-ttu-id="2cdca-356">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-356">It is covered in more detail in a later module.</span></span>

## <a name="loginname"></a><span data-ttu-id="2cdca-357">LoginName</span><span class="sxs-lookup"><span data-stu-id="2cdca-357">LoginName</span></span>

<span data-ttu-id="2cdca-358">登录名称控件在登录到ASP.NET应用程序后显示用户的用户名。</span><span class="sxs-lookup"><span data-stu-id="2cdca-358">The LoginName control displays a user's username after being logged into an ASP.NET application.</span></span> <span data-ttu-id="2cdca-359">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-359">It is covered in more detail in a later module.</span></span>

## <a name="createuserwizard"></a><span data-ttu-id="2cdca-360">创建用户向导</span><span class="sxs-lookup"><span data-stu-id="2cdca-360">CreateUserWizard</span></span>

<span data-ttu-id="2cdca-361">CreateUserWizard 是一个可配置的向导，它使用户能够创建ASP.NET成员资格帐户，供ASP.NET应用程序使用。</span><span class="sxs-lookup"><span data-stu-id="2cdca-361">The CreateUserWizard is a configurable wizard which gives users the ability to create an ASP.NET Membership account for use in an ASP.NET application.</span></span> <span data-ttu-id="2cdca-362">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-362">It is covered in more detail in a later module.</span></span>

## <a name="changepassword"></a><span data-ttu-id="2cdca-363">ChangePassword</span><span class="sxs-lookup"><span data-stu-id="2cdca-363">ChangePassword</span></span>

<span data-ttu-id="2cdca-364">更改密码控件允许用户更改其ASP.NET应用程序的密码。</span><span class="sxs-lookup"><span data-stu-id="2cdca-364">The ChangePassword control allows users to change their password for an ASP.NET application.</span></span> <span data-ttu-id="2cdca-365">在后面的模块中更详细地介绍它。</span><span class="sxs-lookup"><span data-stu-id="2cdca-365">It is covered in more detail in a later module.</span></span>

## <a name="various-webparts"></a><span data-ttu-id="2cdca-366">各种 Web 部件</span><span class="sxs-lookup"><span data-stu-id="2cdca-366">Various WebParts</span></span>

<span data-ttu-id="2cdca-367">ASP.NET 2.0 船舶与各种 Web 部件。</span><span class="sxs-lookup"><span data-stu-id="2cdca-367">ASP.NET 2.0 ships with various Web Parts.</span></span> <span data-ttu-id="2cdca-368">这些将在后面的模块中详细介绍。</span><span class="sxs-lookup"><span data-stu-id="2cdca-368">These will be covered in detail in a later module.</span></span>
