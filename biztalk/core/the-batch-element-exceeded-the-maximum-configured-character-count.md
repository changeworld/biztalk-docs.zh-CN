---
title: 批处理元素已超过最大配置的字符计数 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7ad12733-295a-43ba-8147-34c8716c2d37
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 689ba342affa3ed4f246e9aa963f8ea4e22704af
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36992414"
---
# <a name="the-batch-element-exceeded-the-maximum-configured-character-count"></a>批处理元素已超过配置的最大字符数
## <a name="details"></a>详细信息  
  
|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  产品名称   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 产品版本 |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    事件 ID     |                                           -                                            |
|  事件源   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    组件    |                                    批处理引擎                                     |
|  符号名称  |                             MessageExceededCharacterCount                              |
|  消息正文   |           批处理元素已超过配置的最大字符数            |
  
## <a name="explanation"></a>解释  
 此错误/警告/信息事件表明批处理业务流程无法生成经过批处理的交换，因为由批处理业务流程选取的批处理元素中的字符数已超过批处理发布条件的“交换中的最大字符数量”属性中指定的字符数。 生成此错误消息的批处理元素将不是为批处理所选取的第一个批处理元素，但第一个批处理元素之后的批处理元素已进行批处理。 请注意，与最大数量相比，字符数并不包含信封中的字符数。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请执行以下操作之一：  
  
1.  增加“作为交换接收方的参与方”的“EDI 属性”对话框的“交换批处理创建设置”页中“”属性。 为此，您必须停止业务流程实例，增加属性中的最大字符数，然后重新启动业务流程实例。  
  
2.  让发送方发送字符数低于最大字符数的事务集。