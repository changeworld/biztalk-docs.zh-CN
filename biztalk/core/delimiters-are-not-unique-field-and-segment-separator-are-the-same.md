---
title: "分隔符不唯一，是相同的字段和段分隔符 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1441434a-e969-4803-8e44-c7738d9b23ed
caps.latest.revision: "9"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 440ffb1213936fba4b08a8ee478f6c141eba38fc
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="delimiters-are-not-unique-field-and-segment-separator-are-the-same"></a>分隔符不唯一，字段和段分隔符相同
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]|  
|产品版本|[!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]|  
|事件 ID|-|  
|事件源|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI|  
|组件|EDI 引擎|  
|符号名称|-|  
|消息正文|分隔符不唯一，字段和段分隔符相同|  
  
## <a name="explanation"></a>解释  
 此错误/警告/信息事件表明 EDI 发送管道无法处理传出的交换，因为数据元素和段分隔符是相同的值。 在 X12 交换中，数据元素分隔符是 ISA 段的第四个字符位置中的字符，段终止符是 ISA 段的最后一个字符位置中的字符。 在 EDIFACT 交换中，数据元素分隔符是 UNA2 字段中的字符，段终止符是 UNA6 字段中的字符。 保留的批方案中可能会发生两个分隔符具有相同值的情况（但这会导致错误），或者如果交换通过直通传输接收，然后由发送端口选取作为 MessageBox 中的 XML 文件，也可能会发生这种情况。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请更改交换中数据元素或段分隔符的值，然后重新提交交换。