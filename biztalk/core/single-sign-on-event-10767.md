---
title: 单一登录： 事件 10767 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ef5efc04-a0b5-4fc7-9d0e-f7aa9a9c413d
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a14733abb624207704b304ef9718608c9df1c4bf
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36977334"
---
# <a name="single-sign-on-event-10767"></a>单一登录： 事件 10767
## <a name="details"></a>详细信息  
  
|                 |                                                                                                                         |
|-----------------|-------------------------------------------------------------------------------------------------------------------------|
|  产品名称   |                                                企业单一登录                                                |
| 产品版本 |                               [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                |
|    事件 ID     |                                                          10767                                                          |
|  事件源   |                                                         ENTSSO                                                          |
|    组件    |                                                           N/A                                                           |
|  符号名称  |                                                 ENTSSO_E_NO_SSO_SERVER                                                  |
|  消息正文   | 无法联系 SSO 服务器“%1”。 请检查是否正确配置了 SSO 以及 SSO 服务是否正在该服务器上运行。 |
  
## <a name="explanation"></a>解释  
 ENTSSO 客户端无法联系 ENTSSO 服务器。  
  
## <a name="user-action"></a>用户操作  
 检查网络连接性并确保您正确拼写了服务器名称。