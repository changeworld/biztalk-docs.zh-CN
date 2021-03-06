---
title: 单一登录： 事件 10724 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 022a6f73-a24b-4058-91a5-b831f6875409
caps.latest.revision: 11
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b53fcdeaaadefbbb90738c9e8d4e2c0d234e338b
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36986166"
---
# <a name="single-sign-on-event-10724"></a>单一登录： 事件 10724
## <a name="details"></a>详细信息  

|                 |                                                                                                                                                                                                    |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  产品名称   |                                                                                     企业单一登录                                                                                      |
| 产品版本 |                                                                     [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                                                     |
|    事件 ID     |                                                                                               10724                                                                                                |
|  事件源   |                                                                                               ENTSSO                                                                                               |
|    组件    |                                                                                                N\A                                                                                                 |
|  符号名称  |                                                                                    SSO_ERROR_REPLAY_SECURITY_2                                                                                     |
|  消息正文   | 已经对重播或进度文件的初始安全值进行了更改。%r<br /><br /> 文件名称: %1 %r<br /><br /> 当前文件安全性: %2 %r<br /><br /> 原始文件安全性： %3 |

## <a name="explanation"></a>解释  
 此错误事件表示已更改的重播或进度文件的安全性。  

 重播文件存储在重播文件目录中。 默认情况下，SSO 服务帐户用来创建重播文件和重播文件目录。 创建之后，SSO 会验证是否未对重播文件和重播文件目录的安全配置进行更改。 如果重播文件目录是使用其他帐户创建的，则当密码同步尝试在该目录中创建重播文件时，可能会返回此错误。 强烈建议用户不要更改重播文件和重播文件目录的任何安全配置。  

## <a name="user-action"></a>用户操作  
 若要解决此错误，请执行以下操作：  

- 检查用来创建重播文件的帐户的权限。 这通常是 SSO 系统帐户。  

  有关详细信息，请参阅下列资源：  

- [如何配置密码同步](../core/how-to-configure-password-synchronization.md)  

- [密码同步](../core/password-synchronization2.md)
