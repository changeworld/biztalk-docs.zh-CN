---
title: 分隔符不唯一 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1c37cc55-8923-4124-9004-91ee5093df9c
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 0d724533fb89d3f4d43654aadaf43094adb80e06
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36966740"
---
# <a name="delimiters-are-not-unique"></a>分隔符不唯一
## <a name="details"></a>详细信息  
  
|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  产品名称   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 产品版本 |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    事件 ID     |                                           -                                            |
|  事件源   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    组件    |                                       EDI 引擎                                       |
|  符号名称  |                                           -                                            |
|  消息正文   |                               分隔符不唯一                                |
  
## <a name="explanation"></a>解释  
 此错误/警告/信息事件表明 EDI 发送管道无法处理传出交换，因为交换中标识的两个或多个分隔符（用于分隔交换的多个方面）相同。 这些分隔符是在 X12 交换的 ISA 分段以及 EDIFACT 交换的 UNA 分段中标识的。 保留的批方案中可能会发生两个或多个分隔符具有相同值的情况，或者如果交换通过直通传输接收，然后由发送端口选取作为 MessageBox 中的 XML 文件，也可能会发生这种情况。 此错误将会导致处理交换失败。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请标识交换中具有相同值的分隔符，并更改其中一个分隔符的值。