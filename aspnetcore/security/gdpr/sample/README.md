---
ms.openlocfilehash: 96cd8c78178b02ad3eb4a471540950b4581af583
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57033374"
---
# <a name="gdpr-sample"></a>GDPR 示例

* 在*appsettings.json*，请设置`CheckNotConsentNeeded`到`false`需要同意; 否则设置为 true，或省略。 测试应用程序与`CheckNotConsentNeeded`设置为`false`并将设置为`true`。
* 使用的每个变体创建基本的和不必要的 cookie`CheckConsentNeeded`和授予许可。
* 注册用户。
* 删除 cookie。
