---
title: "单一登录： 事件 10595 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1517478c-7217-4e34-a5cb-ff7deea367ed
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9139eb7479b0a048e2fab197863b42c47f87992a
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="single-sign-on-event-10595"></a>单一登录： 事件 10595
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|企业单一登录|  
|产品版本|[!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]|  
|事件 ID|10595|  
|事件源|ENTSSO|  
|组件|N/A|  
|符号名称|SSO_WARN_APP_INCOMPLETE_FIELDS|  
|消息正文|由于此应用程序的字段未完成，因此无法启用该应用程序。%r<br /><br /> 应用程序名称: %1 %r<br /><br /> 定义的字段数: %2 %r<br /><br /> 创建的字段的数目： %3|  
  
## <a name="explanation"></a>解释  
 当创建 API 级别的应用程序时，您指定了应用程序将要定义的字段数（例如：用户 ID 和密码）。 还必须创建每个已定义的字段。 此警告消息列出了应用程序名称、定义的字段数量，以及创建的字段数量。  
  
## <a name="user-action"></a>用户操作  
 确定已定义但未创建哪些字段，然后返回并创建它们。