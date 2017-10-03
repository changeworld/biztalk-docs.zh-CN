---
title: "单一登录： 事件 11026 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e39b252d-2ed0-4006-aac2-4dce6504afb2
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: ecee6d3c3e6dcf01b8489c4041f4aab717eba585
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="single-sign-on-event-11026"></a>单一登录： 事件 11026
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|企业单一登录|  
|产品版本|[!INCLUDE[btsSSOVersion](../includes/btsssoversion-md.md)]|  
|事件 ID|11026|  
|事件源|ENTSSO|  
|组件|N/A|  
|符号名称|SSO_WARN_EXISTING_GROUP_MAPPING|  
|消息正文|无法创建新的组映射，因为与现有的映射存在冲突。 请删除现有映射，然后重试。%r<br /><br /> 现有的映射: %1 %r<br /><br /> 新映射: %2 %r<br /><br /> 外部帐户: %3 %r<br /><br /> 应用程序名称： %4|  
  
## <a name="explanation"></a>解释  
 最可能的原因是您的系统使用的是旧版本的企业单一登录和旧的组应用程序。  
  
## <a name="user-action"></a>用户操作  
 删除并重新创建警告中建议的映射。 如果该操作失败，则您可能需要升级到更新版本的企业单一登录。