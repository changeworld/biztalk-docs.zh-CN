---
title: 交换发生了结构错误。 可能的原因是无效的段终止符由于缺少回车行和-或换行分隔符而造成 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 035e37d5-d4a8-49d0-8d75-3bcf2426cac7
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 4e1d3c90d69b3e482ac570538f5dcc6997a63aea
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36988766"
---
# <a name="the-interchange-had-structural-error-a-likely-cause-is-invalid-segment-terminator-due-to-missing-carriage-line-and-or-line-feed-seperators"></a>交换发生了结构错误。 可能的原因是无效的段终止符由于缺少回车行和-或换行分隔符
## <a name="details"></a>详细信息  
  
|                 |                                                                                                                                                                                                                                                                                       |
|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  产品名称   |                                                                                                  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]                                                                                                   |
| 产品版本 |                                                                                                              [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]                                                                                                               |
|    事件 ID     |                                                                                                                                           -                                                                                                                                           |
|  事件源   |                                                                                                [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI                                                                                                 |
|    组件    |                                                                                                                                      EDI 引擎                                                                                                                                       |
|  符号名称  |                                                                                                                        EfactInterchangeStructuralErrorAfterUnb                                                                                                                        |
|  消息正文   | 交换 id 为 '{0}，发送方 id{1}，接收方 id{2}发生了结构错误。 可能的原因是段终止符由于缺少回车符和/或换行符而无效。 错误之后的部分已被挂起，请参阅“挂起队列”以获取详细信息。 |
  
## <a name="explanation"></a>解释  
 此错误/警告/信息事件表明接收管道、发送管道或批处理业务流程无法处理 EDIFACT 交换，因为交换中的某个段没有所需的段终止符。 对于传入的交换，是在“UNA 段”中标识分隔符的，如果“UNA 段”不存在，则为 EfactDelimiters 管道属性。 对于传出的交换，是在“EDI 属性”对话框的“UNA 段定义”页中标识的。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请确保交换中的所有段具有所需的段终止符，然后重新发送交换。