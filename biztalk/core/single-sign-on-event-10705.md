---
title: 单一登录： 事件 10705 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 81456bdd-dfd8-4483-aa76-5ec72350cc70
caps.latest.revision: 12
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c74e4ebe0119698348668eb2ca6f78b5697cc5d0
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36976894"
---
# <a name="single-sign-on-event-10705"></a>单一登录： 事件 10705
## <a name="details"></a>详细信息  

|                 |                                                                                                            |
|-----------------|------------------------------------------------------------------------------------------------------------|
|  产品名称   |                                         企业单一登录                                          |
| 产品版本 |                         [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                         |
|    事件 ID     |                                                   10705                                                    |
|  事件源   |                                                   ENTSSO                                                   |
|    组件    |                                                    N\A                                                     |
|  符号名称  |                                          SSO_WARN_PS_NOT_ADAPTER                                           |
|  消息正文   | 指定的适配器不是适配器应用程序。 检查应用程序类型。%r<br /><br /> 适配器： %1 |

## <a name="explanation"></a>解释  
 此警告事件表明，指定的适配器不是适配器应用程序。  

## <a name="user-action"></a>用户操作  
 若要解决此警告问题，请执行以下操作：  

- 使用 SSO Admin MMC 管理单元，右键单击指定的适配器，然后单击“属性”以确定应用程序类型，或者使用命令行工具 ssops -list and ssops -display 来确定应用程序类型。  

- 使用 SSO Admin MMC 管理单元或 ssops-addapp 设置适配器应用程序。  

  有关详细信息，请参阅下列资源：  

- [如何管理密码同步](../core/how-to-administer-password-synchronization.md)
