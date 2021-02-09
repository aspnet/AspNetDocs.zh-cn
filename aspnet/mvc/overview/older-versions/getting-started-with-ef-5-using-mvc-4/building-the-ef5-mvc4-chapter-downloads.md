---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
title: 为 EF 5 MVC 4 教程构建章节下载 |Microsoft Docs
author: Rick-Anderson
description: Contoso 大学示例 web 应用程序演示如何使用实体框架 5 Code First 和 Visual Studio .。。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: d0a89089-eed8-4f61-a478-c5ffa30186f5
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/building-the-ef5-mvc4-chapter-downloads
msc.type: authoredcontent
ms.openlocfilehash: 0e3db273d43fef6956c07a5340eb9aa1d1425d59
ms.sourcegitcommit: b4cdcf246850751579e45da80c9780fe56330dd0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2021
ms.locfileid: "99985123"
---
# <a name="building-the-chapter-downloads-for-the-ef-5-mvc-4-tutorials"></a>为 EF 5 MVC 4 教程构建章节下载

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架 5 Code First 和 Visual Studio 2012 创建 ASP.NET MVC 4 应用程序。 若要了解教程系列，请参阅[本系列中的第一个教程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

## <a name="building-the-chapter-downloads"></a>生成章节下载

1. 下载并解压缩项目示例 zip 文件。 在解压缩的下载包中，你将找到其他 zip 文件，每个章节完成一个。
2. 右键单击所需的 zip 文件，单击 " **属性**"，然后单击 " **取消阻止** " 按钮。  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image1.png)
3. 解压缩文件。
4. 双击 *CUx* 文件以启动 Visual Studio。
5. 从 " **工具** " 菜单中依次单击 " **NuGet 包管理器**" 和 " **程序包管理器控制台**"。  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image2.png)
6. 在包管理器控制台中 (PMC ") 中，单击" **还原**"。  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image3.png)
7. 退出 Visual Studio。
8. 重新启动 Visual Studio，打开在上述步骤中关闭的解决方案文件。
9. 在 "包管理器控制台 (PMC") 中，输入 `Update-Database` 以下命令：  
  
    ![](building-the-ef5-mvc4-chapter-downloads/_static/image4.png)  

    > [!NOTE]
    > 如果收到以下错误信息：  
    >   
    >  *术语 "更新-数据库" 未被识别为 cmdlet、函数、脚本文件或可运行程序的名称。检查名称的拼写，如果包含路径，请验证路径是否正确，然后重试。*  
    > 退出并重新启动 Visual Studio。

    每个迁移将运行，种子方法将运行。 你现在可以运行该应用程序。

    ![](building-the-ef5-mvc4-chapter-downloads/_static/image5.png)

> [!div class="step-by-step"]
> [上一页](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
