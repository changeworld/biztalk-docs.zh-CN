---
title: 未批处理的协议配置组接收器设置 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 57b205e9-aaab-43d1-b373-17d206957814
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 534d426d192e27bbe7c6c7e866399b42360a8e3a
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36990638"
---
# <a name="the-group-receiver-settings-are-not-configured-for-agreement-of-batch"></a>未针对批协议配置组接收器设置
## <a name="details"></a>详细信息  
  
|                 |                                                                                                                                     |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------|
|  产品名称   |                         [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]                          |
| 产品版本 |                                     [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]                                      |
|    事件 ID     |                                                                  -                                                                  |
|  事件源   |                       [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI                        |
|    组件    |                                                           批处理引擎                                                           |
|  符号名称  |                                                      GroupReceiverNotSelected                                                       |
|  消息正文   | 未批处理的协议配置组接收器设置{0}。 需要先完成此设置才能进行批处理。 |
  
## <a name="explanation"></a>解释  
 此错误/警告/信息事件表明发生了以下两种情况之一：  
  
-   批处理业务流程无法验证其已接收的批处理元素，因为没有设置包含编码语法的 UNB1.1 字段（对于 EDIFACT 编码的交换）。  
  
-   批处理业务流程无法为批处理元素创建信封设置，因为标头属性不完整（X12 交换的 ISA、GS 和 ST 属性，EDIFACT 交换的 UNA、UNB、UNG 和 UNH 属性）。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请执行以下操作之一：  
  
-   如果批处理业务流程由于未设置编码语法而无法验证其已接收的批处理元素，请在“EDI 属性”对话框的“UNB 段定义”页中为 UNB1.1 字段设置编码语法。  
  
-   如果批处理业务流程由于标头属性不完整而无法为批处理元素创建信封设置，请确保设置 X12 交换的 ISA、GS 和 ST 属性，或者设置 EDIFACT 交换的 UNA、UNB、UNG 和 UNH 属性。