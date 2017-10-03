---
title: "适用于 SQL 适配器客户端的功能 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f638154b-0a09-4f89-9c52-2a62fafec7dc
caps.latest.revision: "5"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: d0d1df3a7d5c5748db4b0d3f365d80d84ff1f670
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="features-for-sql-adapter-clients"></a>适用于 SQL 适配器客户端的功能
除了对在的主题中讨论的功能[概述的 BizTalk Adapter for SQL Server](../../adapters-and-accelerators/adapter-sql/overview-of-biztalk-adapter-for-sql-server.md)、[!INCLUDE[adaptersql](../../includes/adaptersql-md.md)]还提供了以下功能，可用于适配器客户端：  
  
-   **配置使用绑定属性的适配器的支持**。 适配器客户端可以配置[!INCLUDE[adaptersqlshort](../../includes/adaptersqlshort-md.md)]通过指定特定的绑定属性。 例如，客户端可以指定在连接池中允许特定连接字符串通过设置连接的最大数**MaxConnectionPoolSize**绑定属性。 有关详细信息，请参阅[了解针对 SQL Server 适配器绑定属性的 BizTalk 适配器](../../adapters-and-accelerators/adapter-sql/read-about-the-biztalk-adapter-for-sql-server-adapter-binding-properties.md)。  
  
-   **有关操作参数的 null 值的支持**。 适配器客户端可以使用 XSD"nillable"属性的操作参数提供 null 值。  
  
-   **BizTalk 中的动态端口支持**。 通过 BizTalk [!INCLUDE[wcfadapter_short](../../includes/wcfadapter-short-md.md)]、[!INCLUDE[adaptersqlshort](../../includes/adaptersqlshort-md.md)]支持动态端口，使动态路由的消息从[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]基于消息上下文属性。 有关详细信息，请参阅[配置动态端口](../../adapters-and-accelerators/adapter-sql/configure-dynamic-ports-in-the-sql-adapter.md)。  
  
-   **对性能计数器支持**。 [!INCLUDE[adaptersqlshort](../../includes/adaptersqlshort-md.md)]以适配器客户端使用支持基于 WCF 的性能计数器。 有关性能计数器的详细信息，请参阅[使用性能计数器与 SQL 适配器](../../adapters-and-accelerators/adapter-sql/use-performance-counters-with-the-sql-adapter.md)。  
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 的 BizTalk Adapter 的概述](../../adapters-and-accelerators/adapter-sql/overview-of-biztalk-adapter-for-sql-server.md)