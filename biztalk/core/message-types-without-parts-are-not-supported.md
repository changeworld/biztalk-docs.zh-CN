---
title: 消息类型不支持部分没有 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d0bfb042-feda-4282-a7fa-c13be4ff6254
caps.latest.revision: 10
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 60bb78e2bbf06ff80315bd9bbc2b33346ed18d5d
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37024163"
---
# <a name="message-types-without-parts-are-not-supported"></a>不支持没有消息部分的消息类型
## <a name="details"></a>详细信息  
  
|                 |                                                                                                                           |
|-----------------|---------------------------------------------------------------------------------------------------------------------------|
|  产品名称   |                    [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]                     |
| 产品版本 |                                [!INCLUDE[btsWCFVersion](../includes/btswcfversion-md.md)]                                 |
|    事件 ID     |                                                             0                                                             |
|  事件源   |                                                             0                                                             |
|    组件    |                                                             0                                                             |
|  符号名称  |                                                             0                                                             |
|  消息正文   | 不支持没有部分的消息类型。 更正服务说明"{0}"消息类型"{1}"，然后重新运行该向导。 |
  
## <a name="explanation"></a>解释  
 此错误表示尝试使用的服务没有定义消息类型。  
  
## <a name="user-action"></a>用户操作  
 将服务更正为具有正确的消息类型，然后尝试使用此服务（如果您拥有要尝试使用的 WCF 服务）。 否则，请联系服务提供商。  有关消息的其他信息，请参阅中的以下资源[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]帮助：  
  
-   [构造 Web 消息](../core/constructing-web-messages.md)