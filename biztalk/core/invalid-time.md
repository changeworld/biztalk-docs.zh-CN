---
title: 无效的时间 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6942eb77-3ef1-460c-ac4f-8f1339c25d1b
caps.latest.revision: 8
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 555934e0be188011a69efb3966e5316bc716c254
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37023819"
---
# <a name="invalid-time"></a>无效的时间
## <a name="details"></a>详细信息  
  
|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  产品名称   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 产品版本 |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    事件 ID     |                                           -                                            |
|  事件源   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    组件    |                                       EDI 引擎                                       |
|  符号名称  |                              X12Ta1InvalidTimeDescription                              |
|  消息正文   |                                      无效的时间                                      |
  
## <a name="explanation"></a>解释  
 此错误/警告/信息事件表明接收管道无法处理传入的交换，因为数据元素中的某个时间值不符合 EDI 架构指定的数据类型或者 X12 交换中 GS05 字段标头的此时间值不符合服务架构（BaseArtifacts.dll 中的 X12ServiceSchema）。 对于 X12，服务架构在 GS05 字段中定义了一个 X12_TM 数据类型的时间，字符长度介于 4 和 8 个字符之间。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请确保数据元素中的时间值符合 EDI 架构指定的数据类型或 X12 交换的 GS05 标头中的时间值符合服务架构，然后重新发送交换。