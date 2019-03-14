---
title: 配置 Blazor 链接器
author: guardrex
description: 了解在构建 Blazor 应用时如何控制中间语言 (IL) 链接器。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/20/2019
uid: host-and-deploy/razor-components/configure-linker
ms.openlocfilehash: 7c53e7912ec3b0ae471ea38777f874f55a32487d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064534"
---
# <a name="configure-the-linker-for-blazor"></a><span data-ttu-id="1c911-103">配置 Blazor 链接器</span><span class="sxs-lookup"><span data-stu-id="1c911-103">Configure the Linker for Blazor</span></span>

<span data-ttu-id="1c911-104">作者：[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="1c911-104">By [Luke Latham](https://github.com/guardrex)</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="1c911-105">Blazor 将在每个版本模式生成期间执行[中间语言 (IL)](/dotnet/standard/managed-code#intermediate-language--execution) 链接，以从输出程序集中删除不必要的 IL。</span><span class="sxs-lookup"><span data-stu-id="1c911-105">Blazor performs [Intermediate Language (IL)](/dotnet/standard/managed-code#intermediate-language--execution) linking during each Release mode build to remove unnecessary IL from the output assemblies.</span></span>

<span data-ttu-id="1c911-106">你可以使用以下任何一种方法控制程序集链接：</span><span class="sxs-lookup"><span data-stu-id="1c911-106">You can control assembly linking with either of the following approaches:</span></span>

* <span data-ttu-id="1c911-107">使用 MSBuild 属性全局禁用链接。</span><span class="sxs-lookup"><span data-stu-id="1c911-107">Disable linking globally with an MSBuild property.</span></span>
* <span data-ttu-id="1c911-108">使用配置文件在每个程序集基础上控制链接。</span><span class="sxs-lookup"><span data-stu-id="1c911-108">Control linking on a per-assembly basis with a configuration file.</span></span>

## <a name="disable-linking-with-an-msbuild-property"></a><span data-ttu-id="1c911-109">使用 MSBuild 属性禁用链接</span><span class="sxs-lookup"><span data-stu-id="1c911-109">Disable linking with an MSBuild property</span></span>

<span data-ttu-id="1c911-110">在构建应用程序（包括发布）时，默认在发布模式下启用链接。</span><span class="sxs-lookup"><span data-stu-id="1c911-110">Linking is enabled by default in Release mode when an app is built, which includes publishing.</span></span> <span data-ttu-id="1c911-111">若要禁用所有程序集链接，请在项目文件中将 `<BlazorLinkOnBuild>` MSBuild 属性设置为 `false`：</span><span class="sxs-lookup"><span data-stu-id="1c911-111">To disable linking for all assemblies, set the `<BlazorLinkOnBuild>` MSBuild property to `false` in the project file:</span></span>

```xml
<PropertyGroup>
  <BlazorLinkOnBuild>false</BlazorLinkOnBuild>
</PropertyGroup>
```

## <a name="control-linking-with-a-configuration-file"></a><span data-ttu-id="1c911-112">使用配置文件控制链接</span><span class="sxs-lookup"><span data-stu-id="1c911-112">Control linking with a configuration file</span></span>

<span data-ttu-id="1c911-113">通过提供 XML 配置文件并在项目文件中将该文件指定为 MSBuild 项，可以在每个程序集的基础上控制链接。</span><span class="sxs-lookup"><span data-stu-id="1c911-113">Linking can be controlled on a per-assembly basis by providing an XML configuration file and specifying the file as an MSBuild item in the project file.</span></span>

<span data-ttu-id="1c911-114">以下是使用配置文件示例 (Linker.xml)：</span><span class="sxs-lookup"><span data-stu-id="1c911-114">The following is an example configuration file (*Linker.xml*):</span></span>

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!--
  This file specifies which parts of the BCL or Blazor packages must not be
  stripped by the IL Linker even if they aren't referenced by user code.
-->
<linker>
  <assembly fullname="mscorlib">
    <!--
      Preserve the methods in WasmRuntime because its methods are called by 
      JavaScript client-side code to implement timers.
      Fixes: https://github.com/aspnet/Blazor/issues/239
    -->
    <type fullname="System.Threading.WasmRuntime" />
  </assembly>
  <assembly fullname="System.Core">
    <!--
      System.Linq.Expressions* is required by Json.NET and any 
      expression.Compile caller. The assembly isn't stripped.
    -->
    <type fullname="System.Linq.Expressions*" />
  </assembly>
  <!--
    In this example, the app's entry point assembly is listed. The assembly
    isn't stripped by the IL Linker.
  -->
  <assembly fullname="MyCoolBlazorApp" />
</linker>
```

<span data-ttu-id="1c911-115">若要详细了解配置文件的文件格式，请参阅 [IL 链接器：xml 描述符语法](https://github.com/mono/linker/blob/master/src/linker/README.md#syntax-of-xml-descriptor)。</span><span class="sxs-lookup"><span data-stu-id="1c911-115">To learn more about the file format for the configuration file, see [IL Linker: Syntax of xml descriptor](https://github.com/mono/linker/blob/master/src/linker/README.md#syntax-of-xml-descriptor).</span></span>

<span data-ttu-id="1c911-116">使用 `BlazorLinkerDescriptor` 项在项目文件中指定配置文件：</span><span class="sxs-lookup"><span data-stu-id="1c911-116">Specify the configuration file in the project file with the `BlazorLinkerDescriptor` item:</span></span>

```xml
<ItemGroup>
  <BlazorLinkerDescriptor Include="Linker.xml" />
</ItemGroup>
```
