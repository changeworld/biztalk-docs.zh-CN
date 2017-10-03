---
title: "为协议的回退设置处于禁用状态 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f14a5e46-1028-4250-af7b-8137fa927d7e
caps.latest.revision: "3"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9060dbe2bf3644310d862d4949d2cf944269105d
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# 协议的后备设置处于禁用状态
## 详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]|  
|产品版本|[!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]|  
|事件 ID|-|  
|事件源|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI|  
|组件|EDI 引擎|  
|符号名称|AgreementResolutionFallbackSettingsDisabled|  
|消息正文|{0} 协议的回退设置处于禁用状态。|  
  
## 解释  
 此错误/警告/信息事件表明 BizTalk Server 能够解析到某个协议且已重定向到回退设置，但发现特定协议的回退设置处于禁用状态。  
  
## 用户操作  
 若要解决此错误，请启用回退设置特定的协议。