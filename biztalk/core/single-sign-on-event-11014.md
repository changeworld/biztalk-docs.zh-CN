---
title: 单一登录： 事件 11014 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 71e4c9bd-8bda-46ca-9e76-f7b4fa033167
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8e86642a7f62b53d45f20e140131d6a12d0771ec
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37001112"
---
# <a name="single-sign-on-event-11014"></a>单一登录： 事件 11014
## <a name="details"></a>详细信息  
  
|                 |                                                                                                                                                          |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
|  产品名称   |                                                                企业单一登录                                                                 |
| 产品版本 |                                                [!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]                                                |
|    事件 ID     |                                                                          11014                                                                           |
|  事件源   |                                                                          ENTSSO                                                                          |
|    组件    |                                                                           N/A                                                                            |
|  符号名称  |                                                                  SSO_ERROR_ACCESS_CHECK                                                                  |
|  消息正文   | 访问检查失败。%r<br /><br /> 客户端用户： %1\\%2 %r<br /><br /> 应用程序名称: %3 %r<br /><br /> 其他数据: %4 %r<br /><br /> 错误代码： %5 |
  
## <a name="explanation"></a>解释  
 所列客户端和应用程序的访问检查失败。  
  
## <a name="user-action"></a>用户操作  
 其他信息应该可以帮助您解决该问题。 为了避免将来再出现此错误，您还可以降低审核级别。