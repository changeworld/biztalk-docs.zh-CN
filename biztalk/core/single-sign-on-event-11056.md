---
title: 单一登录： 事件 11056 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 37e2dd5e-0fa4-4764-8ee1-de2ca2b263d1
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 127ff9581779963cc93ff32987cff2549119efe8
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37010955"
---
# <a name="single-sign-on-event-11056"></a>单一登录： 事件 11056
## <a name="details"></a>详细信息  
  
|                 |                                                                                                                                                                                                                                                                                                                          |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  产品名称   |                                                                                                                                                企业单一登录                                                                                                                                                 |
| 产品版本 |                                                                                                                                [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                                                                                                                |
|    事件 ID     |                                                                                                                                                          11056                                                                                                                                                           |
|  事件源   |                                                                                                                                                          ENTSSO                                                                                                                                                          |
|    组件    |                                                                                                                                                           N/A                                                                                                                                                            |
|  符号名称  |                                                                                                                                           SSO_WARN_PS_DIRECT_GET_CREDS_FAILED                                                                                                                                            |
|  消息正文   | 由于无法从 SSO 数据库获得现有外部凭据，因此，未直接更改外部帐户的密码。%r<br /><br /> 跟踪 ID: %1 %r<br /><br /> 应用程序名称: %2 %r<br /><br /> Windows 帐户: %3 %r<br /><br /> 外部帐户: %4 %r<br /><br /> 错误代码： %5 |
  
## <a name="explanation"></a>解释  
 密码直接未更改外部帐户由于无法从 SSO 数据库获得现有外部凭据。  
  
## <a name="user-action"></a>用户操作  
 使用提供的信息并联系 Microsoft 产品支持服务。