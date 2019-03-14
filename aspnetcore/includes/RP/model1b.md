---
ms.openlocfilehash: 025a244812a50709bfd48de9f47a234a547c53e2
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57047414"
---
<span data-ttu-id="4b6e9-101"><!-- THIS INCLUDE USED BY MVC AND RP --> 向 `Movie` 类添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="4b6e9-101"><!-- THIS INCLUDE USED BY MVC AND RP --> Add the following properties to the `Movie` class:</span></span>

[!code-csharp[](~/tutorials/razor-pages/razor-pages-start/sample/RazorPagesMovie22/Models/Movie.cs?name=snippet1)]

<span data-ttu-id="4b6e9-102">`Movie` 类包含：</span><span class="sxs-lookup"><span data-stu-id="4b6e9-102">The `Movie` class contains:</span></span>

* <span data-ttu-id="4b6e9-103">数据库需要 `ID` 字段以获取主键。</span><span class="sxs-lookup"><span data-stu-id="4b6e9-103">The `ID` field is required by the database for the primary key.</span></span>
* <span data-ttu-id="4b6e9-104">`[DataType(DataType.Date)]`：[DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) 属性指定数据的类型（日期）。</span><span class="sxs-lookup"><span data-stu-id="4b6e9-104">`[DataType(DataType.Date)]`:  The [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) attribute specifies the type of the data (Date).</span></span> <span data-ttu-id="4b6e9-105">通过此特性：</span><span class="sxs-lookup"><span data-stu-id="4b6e9-105">With this attribute:</span></span>

  * <span data-ttu-id="4b6e9-106">用户无需在数据字段中输入时间信息。</span><span class="sxs-lookup"><span data-stu-id="4b6e9-106">The user is not required to enter time information in the date field.</span></span>
  * <span data-ttu-id="4b6e9-107">仅显示日期，而非时间信息。</span><span class="sxs-lookup"><span data-stu-id="4b6e9-107">Only the date is displayed, not time information.</span></span>

<span data-ttu-id="4b6e9-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) 会在后续教程中介绍。</span><span class="sxs-lookup"><span data-stu-id="4b6e9-108">[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) are covered in a later tutorial.</span></span>