---
title: "在使用 SQL 适配器的 SQL Server 中执行表值函数 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3fb8c81c-9384-4eba-b0a0-baed1782245b
caps.latest.revision: "8"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e69877f214a2a4b700de22ec043094510707114d
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="execute-table-valued-functions-in-sql-server-using-the-sql-adapter"></a>在使用 SQL 适配器的 SQL Server 中执行表值函数
SQL Server 中的 TRANSACT-SQL 和 CLR 表值函数中的操作作为进行展示[!INCLUDE[adaptersql](../../includes/adaptersql-md.md)]。 中的操作名称[!INCLUDE[adaptersqlshort](../../includes/adaptersqlshort-md.md)]是相同的表的名称值在 SQL Server 中的函数。  
  
 表值函数中的所有参数都公开在相应的操作。 如果不指定表值函数的输入的参数[!INCLUDE[adaptersqlshort](../../includes/adaptersqlshort-md.md)]内部调用使用 DEFAULT 关键字的函数。 这意味着表值函数的执行使用定义的函数时指定的默认值。  
  
 有关详细信息：  
  
-   使用[!INCLUDE[adaptersqlshort](../../includes/adaptersqlshort-md.md)]与 BizTalk Server 中调用 SQL Server 中的表值函数，请参阅[Invoking Table-Valued 函数通过使用 BizTalk Server 的 SQL Server 中](../../adapters-and-accelerators/adapter-sql/invoke-table-valued-functions-in-sql-server-using-biztalk-server.md)。  
  
-   消息结构和表值函数的 SOAP 操作，请参阅[过程和函数的消息架构](../../adapters-and-accelerators/adapter-sql/message-schemas-for-procedures-and-functions.md)。  
  
## <a name="see-also"></a>另请参阅  
 [哪些操作可以是执行使用适配器？](https://msdn.microsoft.com/library/cc185435(v=bts.10).aspx)