---
title: "解决 BizTalk Server 性能的问题 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dbf21fb9-1ae1-48b5-a65a-e96839b23945
caps.latest.revision: "18"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: df98f717c71198d4be6f8d13eaa539e5c1e16786
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="troubleshooting-biztalk-server-performance"></a>解决 BizTalk Server 性能
本部分包含诊断和解决与 BizTalk 消息引擎相关的性能问题的一般准则。  
  
## <a name="estimating-document-processing-requirements"></a>评估文档处理要求  
 在将解决方案部署到生产环境之前，进行规划和测试，以确定消息引擎性能需求。 这将有助于您正确地构建 BizTalk Server 和 SQL Server 环境。  
  
1.  规划与容错、备份和恢复需要相关的开销  
  
    -   是否要将 SQL Server 磁盘配置为 RAID 阵列？  
  
    -   是否要为 BizTalk 主机、SQL Server 或企业单一登录使用 Windows 群集？ 有关详细信息请参阅[高可用性规划](../core/planning-for-high-availability3.md)。  
  
    -   是否将使用网络负载平衡？  
  
    -   环境的备份和恢复要求是什么？ 有关详细信息，请参阅[Backing Up and Restoring BizTalk Server Databases](../core/backing-up-and-restoring-biztalk-server-databases.md)。  
  
2.  请按照中的准则[持续性能规划](../core/planning-for-sustained-performance.md)来计划、 测试和缩放你的 BizTalk Server 和 SQL Server 环境。  
  
3.  请按照中的准则[跟踪性能特征](../core/tracking-performance-characteristics.md)规划文档跟踪要求与关联的开销。  
  
## <a name="optimizing-an-existing-biztalk-server-environment"></a>优化现有 BizTalk Server 环境  
 按照以下步骤优化现有 BizTalk Server 环境：  
  
1.  请按照中的准则[识别性能瓶颈](../core/identifying-performance-bottlenecks.md)定点 BizTalk Server 环境中可能的瓶颈。  
  
2.  请按照中的准则[优化资源使用通过主机限制](../core/optimizing-resource-usage-through-host-throttling.md)以最大化 BizTalk Server 环境的文档吞吐量。  
  
3.  请考虑修改中所述的参数[配置参数会影响适配器性能](../core/configuration-parameters-that-affect-adapter-performance.md)来最大化适配器性能在某些情况下。  
  
4.  请按照中的准则[如何 BizTalk 服务器进程大消息](../core/how-biztalk-server-processes-large-messages.md)在处理大型消息 (超过 100 MB) 时优化消息引擎性能。  
  
5.  为发送适配器、接收适配器和业务流程创建单独的主机和主机实例。 这将使每个适配器都在单独的主机实例中运行，并确保一个适配器不会对另一个适配器产生不利影响。 由于可在主机级别配置主机阻止设置，因而将处理逻辑分为不同的主机还可基于每个主机的处理要求来配置阻止设置。  
  
## <a name="diagnosing-performance-problems-in-an-existing-biztalk-server-environment"></a>诊断现有 BizTalk Server 环境中的性能问题  
 通常，可以将性能问题的范围缩小到以下 BizTalk Server 环境的组件之一：  
  
-   接收适配器或正向此适配器发送文档的系统。 例如，如果 HTTP 适配器正以非最佳速率接收文档，则导致性能问题的可能是 HTTP 接收适配器或正向此 HTTP 适配器发送内容的客户端。  
  
-   业务流程服务实例。  
  
-   保存的 Microsoft SQL server 的性能[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]数据库。  
  
-   发送适配器或正接收此适配器发送的文档的系统。 例如，如果文档发送速率并非最佳的 SQL 适配器则问题可能与 SQL 发送适配器或运行的计算机[!INCLUDE[btsSQLServerNoVersion](../includes/btssqlservernoversion-md.md)]更新 SQL 适配器。  
  
 使用以下准则来帮助识别的各组件[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]不良执行的环境：  
  
-   捕获任何警告或错误中生成[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]或[!INCLUDE[btsSQLServerNoVersion](../includes/btssqlservernoversion-md.md)]事件查看器。  
  
-   按照中的步骤[识别性能瓶颈](../core/identifying-performance-bottlenecks.md)有助于查明性能瓶颈。  
  
 确定了性能较差的组件后，请遵循以下相应的准则来帮助解决问题：  
  
 **用于解决相关发送和接收适配器的性能问题的指导原则**  
  
-   请参阅[疑难解答 BizTalk Server 适配器](../core/troubleshooting-biztalk-server-adapters.md)来排查问题的一般信息[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]适配器。 本部分包含常规疑难解答信息，包括有关如何设置某些适配器的日志记录的信息，还包括可用于诊断网络问题、与 MSDTC 相关的问题、与注册表相关的问题、与文件系统相关的问题以及与 IIS 相关的问题的信息。  
  
-   请参阅的相应部分[疑难解答 BizTalk Server 依赖项](../core/troubleshooting-biztalk-server-dependencies.md)解决与 MSDTC、 证书、 Enterprise 上单一登录，问题的一般信息和[!INCLUDE[btsSQLServerNoVersion](../includes/btssqlservernoversion-md.md)]。  
  
 **以解决与业务流程相关的性能问题的指导原则**  
  
-   修改 BTSNTSvc.exe.config 文件中所述的相应部分[业务流程引擎配置](../core/orchestration-engine-configuration.md)。  
  
 **以解决与 SQL Server 相关的性能问题的指导原则**  
  
-   SQL Server Profiler 可用于捕获发送至 SQL Server 的 Transact-SQL 语句和这些语句的 SQL Server 结果集。 由于 BizTalk Server 与 SQL Server 紧密集成，因此，对于在从 SQL Server 数据库读取和向 SQL Server 数据库写入时在 BizTalk Server 中发生的问题，SQL Server 配置文件跟踪分析将是一个非常有用的问题分析工具。 有关如何使用 SQL Server Profiler 的信息，请参阅 SQL Server 文档。  
  
-   [!INCLUDE[btsSQLServer2008](../includes/btssqlserver2008-md.md)]查询编辑器可以用于执行直接针对 SQL Server 数据库的 SQL 语句。 在某些情况下，此功能对于查询 BizTalk Server 数据库或更新 BizTalk Server 数据库很有用。 有关更多信息，请参阅查询编辑器[!INCLUDE[btsSQLServer2008](../includes/btssqlserver2008-md.md)]文档。  
  
-   查看[故障排除 SQL Server](../core/troubleshooting-sql-server.md)有关其他信息。  
  
## <a name="see-also"></a>另请参阅  
 [故障排除](../core/troubleshooting.md)