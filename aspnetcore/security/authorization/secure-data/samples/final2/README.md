---
ms.openlocfilehash: e40d28e9a7ca12efe45988fabef23dece893d428
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049104"
---
# <a name="how-to-buildrun-secure-user-data-sample"></a><span data-ttu-id="d4527-101">如何生成/运行安全的用户数据示例</span><span class="sxs-lookup"><span data-stu-id="d4527-101">How to build/run Secure user data sample</span></span>

* <span data-ttu-id="d4527-102">使用机密管理器工具设置密码：</span><span class="sxs-lookup"><span data-stu-id="d4527-102">Set password with the Secret Manager tool:</span></span>

  `dotnet user-secrets set SeedUserPW <pw>`

* <span data-ttu-id="d4527-103">更新数据库：</span><span class="sxs-lookup"><span data-stu-id="d4527-103">Update the database:</span></span>

    `dotnet ef database update`

* <span data-ttu-id="d4527-104">在项目中启用 HTTPS</span><span class="sxs-lookup"><span data-stu-id="d4527-104">Enable HTTPS in the project</span></span>
