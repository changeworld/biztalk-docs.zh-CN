---
title: 单一登录： 事件 10523 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6cee5e88-7c30-45f7-9a2a-f907d8f5bd91
caps.latest.revision: 13
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: be71c63079dfda8a8573bf6f1316fce0e1e0b9c9
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36972478"
---
# <a name="single-sign-on-event-10523"></a>单一登录： 事件 10523
## <a name="details"></a>详细信息  

|                 |                                                                                                                                                                                                           |
|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  产品名称   |                                                                                         企业单一登录                                                                                         |
| 产品版本 |                                                                        [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                                                         |
|    事件 ID     |                                                                                                   10523                                                                                                   |
|  事件源   |                                                                                                  ENTSSO                                                                                                   |
|    组件    |                                                                                                    N\A                                                                                                    |
|  符号名称  |                                                                                        SSO_INFO_RESTORE_SECRET_OK                                                                                         |
|  消息正文   | 主密钥已成功还原。%r<br /><br /> 文件名称: %1 %r<br /><br /> 当前 MSID: %2 %r<br /><br /> 上一个 MSID: %3 %r<br /><br /> 客户端用户: %4 %r<br /><br /> 客户端计算机： %5 |

## <a name="explanation"></a>解释  
 此信息事件表明主密钥已成功还原。  

## <a name="user-action"></a>用户操作  

- 不需要用户进行任何操作。  

  有关详细信息，请参阅 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 帮助中的以下资源：  

- [管理主密钥](../core/managing-the-master-secret.md)  

- [主密钥服务器](../core/master-secret-server.md)
