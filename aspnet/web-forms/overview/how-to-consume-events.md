---
title: 如何：在 Web 窗体应用程序中使用事件
description: 了解如何处理 ASP.NET Web 窗体应用中的按钮单击事件。
author: rick-anderson
ms.author: riande
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- events [ASP.NET], Web Forms
- Web Forms controls, and events
- event handlers [ASP.NET], Web Forms
- events [ASP.NET], consuming
- Web Forms, event handling
ms.assetid: 73bf8638-c4ec-4069-b0bb-a1dc79b92e32
ms.openlocfilehash: 2e1807fed7d03db5893e1767a7a3a0de81862e7f
ms.sourcegitcommit: db13f9477981daabd57b99a410ec34e31e8d6aae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94674799"
---
# <a name="how-to-consume-events-in-a-web-forms-app"></a><span data-ttu-id="37c40-103">如何：在 Web 窗体应用程序中使用事件</span><span class="sxs-lookup"><span data-stu-id="37c40-103">How to: Consume events in a Web Forms app</span></span>

<span data-ttu-id="37c40-104">ASP.NET Web 窗体应用程序中的一种常见情况是使用控件填充网页，然后根据用户单击的控件执行特定操作。</span><span class="sxs-lookup"><span data-stu-id="37c40-104">A common scenario in ASP.NET Web Forms applications is to populate a webpage with controls, and then perform a specific action based on which control the user clicks.</span></span> <span data-ttu-id="37c40-105">例如，当用户在网页中单击 <xref:System.Web.UI.WebControls.Button?displayProperty=nameWithType> 控件时，该控件会引发一个事件。</span><span class="sxs-lookup"><span data-stu-id="37c40-105">For example, a <xref:System.Web.UI.WebControls.Button?displayProperty=nameWithType> control raises an event when the user clicks it in the webpage.</span></span> <span data-ttu-id="37c40-106">通过处理事件，应用可以对按钮单击执行相应的应用逻辑。</span><span class="sxs-lookup"><span data-stu-id="37c40-106">By handling the event, your application can perform the appropriate application logic for that button click.</span></span>  
  
## <a name="handle-a-button-click-event-on-a-webpage"></a><span data-ttu-id="37c40-107">处理网页上的按钮单击事件</span><span class="sxs-lookup"><span data-stu-id="37c40-107">Handle a button-click event on a webpage</span></span>  
  
1. <span data-ttu-id="37c40-108">创建一个具有 <xref:System.Web.UI.WebControls.Button> 控件的 ASP.NET Web 窗体页，并将控件的 `OnClick` 值设置为下一步中定义的方法名称。</span><span class="sxs-lookup"><span data-stu-id="37c40-108">Create a ASP.NET Web Forms page (webpage) that has a <xref:System.Web.UI.WebControls.Button> control with the `OnClick` value set to the name of method that you will define in the next step.</span></span>  
  
    ```xml  
    <asp:Button ID="Button1" runat="server" Text="Click Me" OnClick="Button1_Click" />  
    ```  
  
2. <span data-ttu-id="37c40-109">定义一个事件处理程序，使之与 <xref:System.Web.UI.WebControls.Button.Click> 事件委托签名匹配，并且具有为 `OnClick` 值定义的名称。</span><span class="sxs-lookup"><span data-stu-id="37c40-109">Define an event handler that matches the <xref:System.Web.UI.WebControls.Button.Click> event delegate signature and that has the name you defined for the `OnClick` value.</span></span>  
  
    ```csharp  
    protected void Button1_Click(object sender, EventArgs e)  
    {  
        // perform action  
    }  
    ```  
  
    ```vb  
    Protected Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click  
        ' perform action  
    End Sub  
    ```  
  
     <span data-ttu-id="37c40-110"><xref:System.Web.UI.WebControls.Button.Click> 事件将 <xref:System.EventHandler> 类用于委托类型，并将 <xref:System.EventArgs> 类用于事件数据。</span><span class="sxs-lookup"><span data-stu-id="37c40-110">The <xref:System.Web.UI.WebControls.Button.Click> event uses the <xref:System.EventHandler> class for the delegate type and the <xref:System.EventArgs> class for the event data.</span></span> <span data-ttu-id="37c40-111">ASP.NET 页框架会自动生成代码来创建 <xref:System.EventHandler> 的实例，并将此委托实例添加到 <xref:System.Web.UI.WebControls.Button.Click> 实例的 <xref:System.Web.UI.WebControls.Button> 事件。</span><span class="sxs-lookup"><span data-stu-id="37c40-111">The ASP.NET page framework automatically generates code that creates an instance of <xref:System.EventHandler> and adds this delegate instance to the <xref:System.Web.UI.WebControls.Button.Click> event of the <xref:System.Web.UI.WebControls.Button> instance.</span></span>  
  
3. <span data-ttu-id="37c40-112">在步骤 2 中定义的事件处理程序方法会添加代码以执行事件发生时所需的各种操作。</span><span class="sxs-lookup"><span data-stu-id="37c40-112">In the event handler method that you defined in step 2, add code to perform any actions that are required when the event occurs.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="37c40-113">另请参阅</span><span class="sxs-lookup"><span data-stu-id="37c40-113">See also</span></span>

- [<span data-ttu-id="37c40-114">检查与插入、更新和删除相关联的事件</span><span class="sxs-lookup"><span data-stu-id="37c40-114">Examine the Events Associated with Inserting, Updating, and Deleting</span></span>](data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)
- [<span data-ttu-id="37c40-115">.NET 中的事件</span><span class="sxs-lookup"><span data-stu-id="37c40-115">Events in .NET</span></span>](/dotnet/standard/index.md)
