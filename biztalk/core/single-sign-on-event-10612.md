---
title: 单一登录： 事件 10612 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b9d9e6f5-06b8-4989-a0dc-6e2e5980443b
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 3fdc86dd2143bf8b2b4c27dab66cc4c06ddff5ae
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36973014"
---
# <a name="single-sign-on-event-10612"></a>单一登录： 事件 10612
## <a name="details"></a>详细信息  
  
|                 |                                                                                                                                                                                                                                                                                 |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  产品名称   |                                                                                                                            企业单一登录                                                                                                                            |
| 产品版本 |                                                                                                           [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                                                                                            |
|    事件 ID     |                                                                                                                                      10612                                                                                                                                      |
|  事件源   |                                                                                                                                     ENTSSO                                                                                                                                      |
|    组件    |                                                                                                                                       N/A                                                                                                                                       |
|  符号名称  |                                                                                                                          SSO_WARN_TRANSACTION_TIMEOUT                                                                                                                           |
|  消息正文   | 事务超时时间超出了此操作的建议最大值。 有关详细信息，请参阅文档。%r<br /><br /> 事务 ID: %1 %r<br /><br /> 事务超时： %2 分钟 （零表示无限超时） %r<br /><br /> 建议最大值： %3 分钟 |
  
## <a name="explanation"></a>解释  
 一个具有过大超时值的事务已进入系统。 如果 ENTSSO 系统轮询 SSO 数据库，但该数据库被某个长时间运行的事务将其锁定，则系统最终会处于脱机状态。  
  
## <a name="user-action"></a>用户操作  
 不需要任何用户操作。