---
title: "使用 Oracle 数据库适配器处理事务 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 971c2fba-640c-4ae5-9ab3-2d8227c1627d
caps.latest.revision: "5"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: d45355100e728220745620e1c0df3552f523f649
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="handle-transactions-with-the-oracle-database-adapter"></a>与 Oracle 数据库适配器的句柄事务
[!INCLUDE[adapteroracle](../../includes/adapteroracle-md.md)]并不会启动一个事务执行对 Oracle 数据库操作时。 相反，适配器执行的操作使用提供的适配器客户端的事务上下文。 若要执行操作在事务中使用[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]，你必须：  
  
-   启用适配器客户端中的事务。 例如，若要启用中的事务[!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)]，您必须选择**使用事务**中的复选框**事务**区域**消息**有关选项卡WCF 自定义或 WCF OracleDB 端口。  
  
-   设置的值**UseAmbientTransaction**属性绑定到**True**适配器中。 有关绑定属性的详细信息，请参阅[用于 Oracle 数据库配置的绑定属性](../../adapters-and-accelerators/adapter-oracle-database/configure-the-binding-properties-for-oracle-database.md)。  
  
> [!IMPORTANT]
>  若要使用该适配器上的 Oracle 数据库执行事务，你必须安装**Microsoft Transaction Server 的 Oracle 服务**组件时，运行适配器的计算机上安装 Oracle 客户端，时客户端。  
  
## <a name="transactions-in-the-outbound-operations"></a>中的出站操作的事务  
 [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]在单个事务中执行的出站操作。 对于复合操作，所有操作都执行在单个事务，而是使用不同的 ODP.NET 连接。 有关显示的出站操作详细信息[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]，请参阅[原理适配器面 Oracle 元数据？](https://msdn.microsoft.com/library/cc185310(v=bts.10).aspx)。  
  
## <a name="transactions-in-the-inbound-operations"></a>中的入站操作的事务  
 [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]公开以下两个入站的操作：  
  
-   **轮询**： 轮询语句和后轮询语句 （如果指定） 的执行在事务中，而在不同事务中执行的轮询的数据可用语句。 同样，轮询语句后轮询语句执行和使用相同的 ODP.NET 连接，而使用不同的 ODP.NET 连接执行轮询的数据可用语句。  
  
-   **通知**： 在使用单个 ODP.NET 连接事务中执行通知操作。  
  
 有关显示的入站操作详细信息[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]，请参阅[原理适配器面 Oracle 元数据？](https://msdn.microsoft.com/library/cc185310(v=bts.10).aspx)。  
  
## <a name="see-also"></a>另请参阅  
 [用于 Oracle 数据库的 BizTalk Adapter 的概述](../../adapters-and-accelerators/adapter-oracle-database/overview-of-biztalk-adapter-for-oracle-database.md)