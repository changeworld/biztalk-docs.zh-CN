---
title: "分隔记录中标记处理 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 568eb804-bea5-46d4-8547-8bc30b87156c
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5be9d28e3de6b1a7613db8d0c5ac7365a298a679
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="tag-handling-in-delimited-records"></a>分隔记录中处理的标记

## <a name="overview"></a>概述
分隔的记录可以包含字符，称为一个标记，它可用于消除歧义一种从另一个记录类型的已知的序列。 这将允许平面文件拆装器正确地标识相应**记录**包含正确分析的平面文件记录所需的信息的架构中的节点。  
  
 你可以使用**标记标识符**属性指定分隔记录中的标记。 不同于位置记录中的标记，分隔记录中的标记必须出现在分隔记录的开头，并记录转换为其等效的 XML 格式时永远不会自动包含在数据。  
  
## <a name="see-also"></a>另请参阅  
-  [分隔记录的注意事项](../core/delimited-record-considerations.md)   
-  **标记标识符 （的平面文件架构的节点属性）**[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]