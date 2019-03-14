---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: 生成章节下载 EF 5 mvc 4 个教程 |Microsoft Docs
author: Rick-Anderson
description: Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 的 ASP.NET MVC 4 应用程序...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 6b5d10ba9e878908953e999bd1fd44970acf4ca5
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065564"
---
<a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a>生成章节下载 EF 5 mvc 4 个教程
====================
通过[Rick Anderson]((https://twitter.com/RickAndMSFT))

[下载已完成的项目](http://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大学示例 web 应用程序演示如何创建使用 Entity Framework 5 Code First 和 Visual Studio 2012 的 ASP.NET MVC 4 应用程序。 若要了解系列教程，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。


## <a name="building-the-chapter-downloads"></a>生成章节下载

1. 下载并解压缩项目示例 zip 文件。 在解压缩的下载包中，您会发现其他 zip 文件，分别对应于每一章的完成。
2. 右键单击所需的 zip 文件中，单击**属性**，然后单击**解除阻止**按钮。  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. 将文件解压缩。
4. 双击*CUx.sln*文件以启动 Visual Studio。
5. 从**工具**菜单上，单击**NuGet 包管理器**，然后**程序包管理器控制台**。  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. 在包管理器控制台 (PMC) 中，单击**还原**。  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. 退出 Visual Studio。
8. 重新启动 Visual Studio 中，打开在前面步骤中要关闭的解决方案文件。
9. 在包管理器控制台 (PMC) 中，输入`Update-Database`命令：  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > 如果收到以下错误：  
    >   
    >  *术语更新数据库未识别为 cmdlet、 函数、 脚本文件或可操作程序的名称。检查名称的拼写或如果已包含路径，验证路径正确，然后重试。*  
    > 退出并重新启动 Visual Studio。

    每个迁移将运行，则将运行 seed 方法。 你现在可以运行该应用程序。

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [上一篇](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
