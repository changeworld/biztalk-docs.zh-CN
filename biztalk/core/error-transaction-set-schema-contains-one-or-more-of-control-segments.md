---
title: 事务集架构包含一个或多个控制段 ISA、 IEA、 GS、 GE |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7589d8f0-c727-47df-afbc-77b0f190f3e2
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 4f0ab50802cbb872d7ba884a8256824426fbe098
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37008200"
---
# <a name="transaction-set-schema-contains-one-or-more-of-control-segments-isa-iea-gs-ge"></a>事务集架构包含一个或多个控制段 ISA、IEA、GS、GE
## <a name="details"></a>详细信息  
  
|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  产品名称   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 产品版本 |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    事件 ID     |                                           -                                            |
|  事件源   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    组件    |                                       EDI 引擎                                       |
|  符号名称  |                       SchemaCode114EOtherControlSegmentsPresent                        |
|  消息正文   |    事务集架构包含一个或多个控制段 ISA、IEA、GS、GE    |
  
## <a name="explanation"></a>解释  
 此错误/警告/信息事件表明接收管道无法处理传入的事务集或发送管道无法处理传出的事务集，因为事务集的文档架构至少定义了一个 ISA、IEA、GS 或 GE 段。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请取消部署文档架构，从架构中删除 ISA、IEA、GS 或 GE 段，然后重新部署架构。