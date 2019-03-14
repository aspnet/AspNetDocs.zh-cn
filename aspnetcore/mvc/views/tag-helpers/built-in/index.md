---
title: ASP.NET Core 内置标记帮助程序
author: pkellner
description: 了解 ASP.NET Core 内置标记帮助程序如何提高生产力。
ms.author: riande
ms.custom: mvc
ms.date: 10/10/2018
uid: mvc/views/tag-helpers/builtin-th/Index
---

# <a name="aspnet-core-built-in-tag-helpers"></a><span data-ttu-id="ec68c-103">ASP.NET Core 内置标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="ec68c-103">ASP.NET Core built-in Tag Helpers</span></span>

<span data-ttu-id="ec68c-104">作者：[Peter Kellner](http://peterkellner.net)</span><span class="sxs-lookup"><span data-stu-id="ec68c-104">By [Peter Kellner](http://peterkellner.net)</span></span>

<span data-ttu-id="ec68c-105">有关标记帮助程序的概述，请参阅 <xref:mvc/views/tag-helpers/intro>。</span><span class="sxs-lookup"><span data-stu-id="ec68c-105">For an overview of Tag Helpers, see <xref:mvc/views/tag-helpers/intro>.</span></span>

> [!NOTE]
> <span data-ttu-id="ec68c-106">内置的标记帮助程序未在文档中描述。</span><span class="sxs-lookup"><span data-stu-id="ec68c-106">There are built-in Tag Helpers which aren't described in the documentation.</span></span> <span data-ttu-id="ec68c-107">[Razor](xref:mvc/views/razor) 视图引擎在内部使用这些标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="ec68c-107">These Tag Helpers are used internally by the [Razor](xref:mvc/views/razor) view engine.</span></span> <span data-ttu-id="ec68c-108">这包括针对扩展到网站根路径的 `~`（波浪号）字符所适用的标记帮助程序。</span><span class="sxs-lookup"><span data-stu-id="ec68c-108">This includes a Tag Helper for the `~` (tilde) character, which expands to the root path of the website.</span></span>

## <a name="built-in-aspnet-core-tag-helpers"></a><span data-ttu-id="ec68c-109">内置 ASP.NET Core 标记帮助程序</span><span class="sxs-lookup"><span data-stu-id="ec68c-109">Built-in ASP.NET Core Tag Helpers</span></span>

<span data-ttu-id="ec68c-110">**[定位点标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ec68c-110">**[Anchor Tag Helper](xref:mvc/views/tag-helpers/builtin-th/anchor-tag-helper)**</span></span>

<span data-ttu-id="ec68c-111">**[缓存标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ec68c-111">**[Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/cache-tag-helper)**</span></span>

<span data-ttu-id="ec68c-112">**[分布式缓存帮助程序](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ec68c-112">**[Distributed Cache Tag Helper](xref:mvc/views/tag-helpers/builtin-th/distributed-cache-tag-helper)**</span></span>

<span data-ttu-id="ec68c-113">**[环境标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ec68c-113">**[Environment Tag Helper](xref:mvc/views/tag-helpers/builtin-th/environment-tag-helper)**</span></span>

[comment]: **[FormActionTagHelper](xref:mvc/views/tag-helpers/builtin-th/form-action-tag-helper)**

<span data-ttu-id="ec68c-114">**[表单标记帮助程序](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ec68c-114">**[Form Tag Helper](xref:mvc/views/working-with-forms#the-form-tag-helper)**</span></span>

<span data-ttu-id="ec68c-115">**[图像标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ec68c-115">**[Image Tag Helper](xref:mvc/views/tag-helpers/builtin-th/image-tag-helper)**</span></span>

<span data-ttu-id="ec68c-116">**[输入标记帮助程序](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ec68c-116">**[Input Tag Helper](xref:mvc/views/working-with-forms#the-input-tag-helper)**</span></span>

<span data-ttu-id="ec68c-117">**[标签标记帮助程序](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ec68c-117">**[Label Tag Helper](xref:mvc/views/working-with-forms#the-label-tag-helper)**</span></span>

[comment]: **[LinkTagHelper](xref:mvc/views/tag-helpers/builtin-th/link-tag-helper)**

[comment]: **[OptionTagHelper](xref:mvc/views/tag-helpers/builtin-th/option-tag-helper)**

[comment]: **[ScriptTagHelper](xref:mvc/views/tag-helpers/builtin-th/script-tag-helper)**

<span data-ttu-id="ec68c-118">**[部分标记帮助程序](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ec68c-118">**[Partial Tag Helper](xref:mvc/views/tag-helpers/builtin-th/partial-tag-helper)**</span></span>

<span data-ttu-id="ec68c-119">**[选择标记帮助程序](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ec68c-119">**[Select Tag Helper](xref:mvc/views/working-with-forms#the-select-tag-helper)**</span></span>

<span data-ttu-id="ec68c-120">**[文本区标记帮助程序](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ec68c-120">**[Textarea Tag Helper](xref:mvc/views/working-with-forms#the-textarea-tag-helper)**</span></span>

<span data-ttu-id="ec68c-121">**[验证消息标记帮助程序](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ec68c-121">**[Validation Message Tag Helper](xref:mvc/views/working-with-forms#the-validation-message-tag-helper)**</span></span>

<span data-ttu-id="ec68c-122">**[验证摘要标记帮助程序](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span><span class="sxs-lookup"><span data-stu-id="ec68c-122">**[Validation Summary Tag Helper](xref:mvc/views/working-with-forms#the-validation-summary-tag-helper)**</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec68c-123">其他资源</span><span class="sxs-lookup"><span data-stu-id="ec68c-123">Additional resources</span></span>

* <xref:mvc/views/tag-helpers/intro>
* <xref:mvc/views/tag-helpers/th-components>
