---
title: 可接受 Edifact 功能组控制编号的最大限制已达到参与方 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2fde516b-59f1-49a1-8456-127469df0e02
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 291aada2014f0ed3f1b2b2b1926aa5b550ca7ae6
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37022147"
---
# <a name="max-limit-of-acceptable-edifact-functional-group-control-number-has-reached-for-party"></a>已达到参与方的可接受 EDIFACT 功能组控制编号最大限制
## <a name="details"></a>详细信息  
  
|                 |                                                                                                                                                                                                   |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  产品名称   |                                                        [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]                                                         |
| 产品版本 |                                                                    [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]                                                                     |
|    事件 ID     |                                                                                                 -                                                                                                 |
|  事件源   |                                                      [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI                                                       |
|    组件    |                                                                                            EDI 引擎                                                                                             |
|  符号名称  |                                                                                    PartyEdifactUngNumberError                                                                                     |
|  消息正文   | 可接受 Edifact 功能组控制编号的最大限制已达到参与方{0}。 导航到合作伙伴协议管理器的接收方角色屏幕中“参与方”中的字段 UNG 5 可重置计数器 |
  
## <a name="explanation"></a>解释  
 此错误/警告/信息事件表明发送管道无法处理传出的 EDIFACT 交换，因为在参与方设置中指定的 UNG5 字段中的组控制编号（具体来说就是字段 UNG5.2 中的参考编号）大于所允许的最大值。 所允许的组控制编号的最大值取决于 UNG5 中三个字段的值。 最大字符数是 14（对于字段 UNG5.2 中的参考编号）、13（对于 UNG5.1 中的前缀）、13（对于 UNG5.3 中的后缀）以及 14（对于所有三个字段的组合）。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请按照如下方式重置组控制编号的参考编号字段 (UNG5.2)：  
  
1.  在为交换解析的参与方的“EDI 属性”对话框中，打开作为交换接收方的参与方的“UNG 和 UNH 段定义”页。  
  
2.  单击与 UNG5 字段关联的“编辑”字段。  
  
3.  将组控制编号的中间字段（UNG5.2 中的参考编号）设置为新值，以便该字段具有可接受的位数。