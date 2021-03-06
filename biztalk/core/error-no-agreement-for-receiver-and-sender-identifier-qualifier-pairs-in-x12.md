---
title: 故障发生在处理 X12 消息在发送端口： 不存在用于收件人和发件人标识符限定符对协议 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 72ae7926-f5c1-42f4-8c29-11f34c138dd4
caps.latest.revision: 15
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8fa38616bfc4117614ab81d4a369f64d3b85e13f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36988798"
---
# <a name="a-failure-occurred-in-processing-x12-message-on-send-port-no-agreement-for-receiver-and-sender-identifier-qualifier-pairs"></a>故障发生在处理 X12 消息在发送端口： 不存在用于收件人和发件人标识符限定符对的协议
## <a name="details"></a>详细信息  
  
|                 |                                                                                                                                                               |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  产品名称   |                                      [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]                                       |
| 产品版本 |                                                  [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]                                                   |
|    事件 ID     |                                                                               -                                                                               |
|  事件源   |                                    [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI                                     |
|    组件    |                                                                          EDI 引擎                                                                           |
|  符号名称  |                                                                               -                                                                               |
|  消息正文   | 故障发生在处理 X12 消息发送端口上的{0}。 不存在 {1}、{2}、{3}、{4} 的接收方和发送方标识符/限定符对的协议。 |
  
## <a name="explanation"></a>解释  
 此错误/警告/信息事件表明 BizTalk Server 无法解析该参与方的 EDIFACT 交换，因为 BizTalk Server 无法匹配提升发件人限定符和标识符属性，并提升接收方限定符和为参与方的相应值的标识符属性。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请确保参与方的“EDI 属性”对话框的“ISA 段定义”页中定义的发送方限定符和标识符（ISA5 和 ISA6）以及接收方限定符和标识符（ISA7 和 ISA8）与交换的上下文中相对应的升级后的属性匹配。