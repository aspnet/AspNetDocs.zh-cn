---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 母版页 |微软文档
author: rick-anderson
description: 成功网站的关键组件之一是外观一致。 在ASP.NET 1.x 中，开发人员使用用户控件来复制通用页面 elem...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: b493feb21d2e3d6429f0a23df5aab66e0c4c5b07
ms.sourcegitcommit: 022f79dbc1350e0c6ffaa1e7e7c6e850cdabf9af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81543179"
---
# <a name="master-pages"></a>母版页

由[微软](https://github.com/microsoft)

> 成功网站的关键组件之一是外观一致。 在ASP.NET 1.x 中，开发人员使用用户控件跨 Web 应用程序复制公共页面元素。 虽然这当然是一个可行的解决方案，但使用用户控件确实有一些缺点。 例如，更改用户控件的位置需要更改到站点中的多个页面。 在页面上插入后，用户控件也不会在"设计"视图中呈现。

成功网站的关键组件之一是外观一致。 在ASP.NET 1.x 中，开发人员使用用户控件跨 Web 应用程序复制公共页面元素。 虽然这当然是一个可行的解决方案，但使用用户控件确实有一些缺点。 例如，更改用户控件的位置需要更改到站点中的多个页面。 在页面上插入后，用户控件也不会在"设计"视图中呈现。

ASP.NET 2.0 引入母版页作为保持一致外观和感觉的一种方式，正如您很快就会看到的那样，母版页代表了对用户控制方法的重大改进。

## <a name="why-master-pages"></a>为什么选择母版页？

您可能想知道为什么 ASP.NET 2.0 需要母版页。 毕竟，网站开发人员已经在ASP.NET 1.x 中使用用户控件在页面之间共享内容区域。 实际上，用户控件是创建公共布局的不太理想的解决方案的原因有很多。

用户控件实际上不定义页面布局。 相反，它们定义页面的一部分的布局和功能。 这两者之间的区别很重要，因为它使用户控制解决方案的可管理性变得更加困难。 例如，如果要更改页面上的用户控件的位置，必须编辑显示用户控件的实际页面。 如果你只有几页，这很好，但在大型网站，它迅速成为一个网站管理噩梦！

使用用户控件定义公共布局的另一个缺点是ASP.NET本身的体系结构。 如果更改了用户控件的任何公共成员，则需要重新编译使用用户控件的所有页面。 反过来，ASP.NET将在首次访问页面时重新 JIT。 这再次产生了一个不可扩展的体系结构和大型站点的站点管理问题。

ASP.NET 2.0 中的母版页很好地解决了这两个问题（以及更多问题）。

## <a name="how-master-pages-work"></a>母版页的工作原理

母版页类似于其他页面的模板。 应在其他页面（即菜单、边框等）之间共享的页面元素将添加到母版页中。 将新页面添加到网站时，可以将它们与母版页相关联。 与母版页关联的页面称为**内容页**。 默认情况下，内容页从母版页中呈现外观。 但是，在创建母版页时，可以定义内容页可以替换为其自己的内容的部分内容。 这些部分使用 ASP.NET 2.0 中引入的新控件进行定义;**ContentPlaceHolder 控件**。

母版页可以包含任意数量的 ContentPlaceHolder 控件（或根本没有。在内容页上，"ContentPlaceHolder"控件中的内容将显示在**内容**控件中，这是 ASP.NET 2.0 中的另一个新控件。 默认情况下，内容页 内容控件为空，以便您可以提供自己的内容。 如果要使用内容控件内母版页中的内容，可以执行此操作，正如您将在此模块的后面部分看到的。 内容控件通过内容控件的"内容霍尔德ID"属性映射到 ContentPlaceHolderId 控件。 下面的代码将内容控件映射到主页上称为 mainBody 的 ContentPlaceHolder 控件。

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> 您经常会听到人们将母版页描述为其他页面的基类。 这实际上不是真的。 母版页和内容页之间的关系不是继承关系。

**图 1**显示了母版页和关联的内容页，因为它们出现在 Visual Studio 2005 中。 您可以在母版页中查看 ContentPlaceHolder 控件，并在内容页中看到相应的内容控件。 请注意，内容霍尔德持有人外部的母版页内容可见，但在内容页中显示为灰色。 只有 ContentPlaceHolder 中的内容可以由内容页取代。 来自母版页的所有其他内容是不可改变的。

![母版页及其关联内容页](master-pages/_static/image1.jpg)

**图 1**： 母版页及其关联内容页

## <a name="creating-a-master-page"></a>创建母版页

要创建新的母版页，

1. 打开 Visual Studio 2005 并创建新网站。
2. 单击"文件，新建，文件"。
3. 从"添加新项目"对话框中选择主文件，如图**2**所示。
4. 单击“添加”。

![创建新母版页](master-pages/_static/image2.jpg)

**图 2**： 创建新母版页

请注意，母版页的文件扩展名是 *.master*。 这是母版页与普通页面不同的方式之一。 另一个主要区别是，母版页代替指令@Page，包含一个@Master指令。 切换到您刚刚创建的母版页的源视图并查看代码。

默认情况下，新的母版页将有一个 ContentPlaceHolder 控件。 在大多数情况下，首先创建公共页面元素，然后插入需要自定义内容的 ContentPlaceHolder 控件更有意义。 在这些情况下，开发人员将希望删除默认的 ContentPlaceHolder 控件，并在页面开发时插入新的控件。 ContentPlaceHolder 控件虽然确实显示大小调整句柄，但它们不会调整大小。 ContentPlaceHolder 控件的大小会自动基于它包含的内容，但有一个例外;如果将 ContentPlaceHolder 控件放置在块元素（如表单元格）内，则该控件将根据元素的大小进行大小调整。

## <a name="lab-1-working-with-master-pages"></a>实验室 1 使用母版页

在本实验中，您将创建一个新的母版页，并定义三个 ContentPlaceHolder 控件。 然后，您将创建新的内容页，并至少从其中一个 ContentPlaceHolder 控制中替换内容。

1. 创建母版页并插入内容霍尔德控件。 

    1. 如上文所述，创建新的母版页。
    2. 删除默认的"内容放置"控件。
    3. 通过单击控件的上边框，然后点击键盘上的 DEL 键将其删除，选择 ContentPlaceHolder 控件。
    4. 使用*标题和侧*模板插入新表，如图 3 所示。 将宽度和高度更改为 90%，以便整个表在设计器中可见。

![](master-pages/_static/image3.jpg)

**图 3**

1. 将光标放入表的每个单元格中，并将*valign*属性设置为*顶部*。
2. 在工具箱中，在表的顶部单元格（标题单元格）中插入 ContentPlaceHolder 控件。
3. 插入此 ContentPlaceHolder 控件时，您会注意到行高度将占用几乎整个页面，如图 4 所示。 在这一点上不要担心。

![空白空间与内容霍尔德位于同一单元格中](master-pages/_static/image1.gif)

**图 4**： 空白空间与内容霍尔德位于同一单元格中

1. 将 ContentPlaceHolder 控件放在其他两个单元格中。 插入其他 ContentPlaceHolder 控件后，表单元格的大小应如您所料。 该页现在应类似于**图 5**所示的页面。

![包含所有内容位置所有者控件的主控形状。 请注意，头单元格的单元格高度现在正是它应该的](master-pages/_static/image2.gif)

**图 5**： 包含所有内容霍尔德控件的主控形状。 请注意，头单元格的单元格高度现在正是它应该的

1. 在三个 ContentPlaceHolder 控件中的每个控件中输入您选择的文本。
2. 将母版页另存为练习1.master。
3. 创建新的 Web 窗体并将其与练习1.master 页相关联。
4. 选择文件，新建，文件在可视化工作室2005年。
5. 在"添加新项目"对话框中选择 **"Web 窗体**"。
6. 确保选中"选择母版页"复选框，如图 6 所示。

![添加新的内容页](master-pages/_static/image3.gif)

**图 6**： 添加新的内容页

1. 单击“添加”。
2. 在"选择母版页对话框中选择练习1.master，如图 7 所示。
3. 单击"确定"以添加新内容页。

新内容页显示在 Visual Studio 中，母版页上每个 ContentPlaceHolder 控件都有一个内容控件。 默认情况下，内容控件为空，以便您可以添加自己的内容。 如果您希望他们使用母版页上的 ContentPlaceHolder 控件中的内容，只需单击智能标记符号（控件右上角的小黑箭头），然后从智能标记中选择 *"默认到母版内容*"，如图**8**所示。 执行此操作时，菜单项将更改为 *"创建自定义内容*"。 此时单击它会从母版页中删除内容，允许您为该特定内容控件定义自定义内容。

![将内容控件设置为默认为母版页内容](master-pages/_static/image4.gif)

**图 7**：将内容控件设置为默认为母版页内容

## <a name="connecting-master-page-and-content-pages"></a>连接母版页和内容页

母版页和内容页之间的关联可以通过以下四种不同方式之一进行配置：

- 指令的@Page<strong>母版页面文件</strong>属性
- 在代码中设置**Page.MasterPageFile**属性。
- 应用程序配置文件中的**&lt;页面&gt;** 元素（应用程序根文件夹中的 Web.config）
- 子文件夹配置文件中的**&lt;页面&gt;** 元素（子文件夹中的 Web.config）

## <a name="masterpagefile-attribute"></a>母版文件属性

MasterPageFile 属性使将母版页应用于特定ASP.NET页面变得容易。 当您选中 **"选择母版页**"复选框时，它也是用于应用母版页的方法，就像练习 1 中所做的那样。

## <a name="setting-pagemasterpagefile-in-code"></a>设置页面.MasterPage文件代码

通过在代码中设置 MasterPageFile 属性，可以在运行时将特定的母版页应用于您的内容。 在可能需要根据用户角色或其他一些条件应用特定母版页的情况下，这非常有用。 必须在 PreInit 方法中设置 MasterPageFile 属性。 如果在 PreInit 方法之后设置，将引发无效操作异常。 正在设置此属性的页面还必须具有"内容"控件作为该页的顶级控件。 否则，在设置 MasterPageFile 属性时，将引发 HttpException。

## <a name="using-the-ltpagesgt-element"></a>使用&lt;页面&gt;元素

您可以通过在 Web.config 文件的&lt;页面&gt;元素中设置 masterPageFile 属性来配置页面的母版页。 使用此方法时，请记住，应用程序结构中较低的 Web.config 文件可以覆盖此设置。 @Page指令中的任何 MasterPageFile 属性集也将覆盖此设置。 使用&lt;页面&gt;元素可以创建可在特定文件夹或文件中在必要时重写*的主版*页变得简单。

## <a name="properties-in-master-pages"></a>母版页中的属性

母版页只需在母版页中公开这些属性，即可公开属性。 例如，以下代码定义名为"某些属性"的属性：

[!code-csharp[Main](master-pages/samples/sample2.cs)]

要从"内容"页访问"某些属性"属性，您需要使用"主"属性，如下所示：

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>嵌套母版页

母版页是确保大型 Web 应用程序的共同外观的完美解决方案。 但是，大型站点的某些部分共享公共接口，而其他部分共享不同的接口的情况并不少见。 为了满足这一需求，多个母版页是完美的解决方案。 但是，这仍然不能解决大型应用程序可能具有某些组件（例如菜单）这一事实，这些组件仅在网站的某些部分之间共享的所有页面和其他组件之间共享。 对于这种情况，嵌套母版页很好地满足了需求。 正如您所看到的，普通母版页由母版页和内容页组成。 在嵌套母版页的情况下，有两个母版页;父主控形状和子母版。 子母版页也是内容页，其母版页是父母版页。

下面是典型母版页的代码：

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

在嵌套主方案中，这将是父主控形状。 另一个母版页将使用此页作为其母版页，该代码如下所示：

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

请注意，在这种情况下，子母版也是父主控形状的内容页。 所有子主控内容都显示在内容控件中，该控件从父级的 ContentPlaceHolder 控件中获取其内容。

> [!NOTE]
> 设计器支持不适用于嵌套母版页。 使用嵌套母版进行开发时，需要使用源视图。

此视频显示了使用嵌套母版页的演练。

![](master-pages/_static/image1.png)

[打开全屏视频](master-pages/_static/nested1.wmv)

![选择母版页](master-pages/_static/image4.jpg)

**图 8**： 选择母版页
