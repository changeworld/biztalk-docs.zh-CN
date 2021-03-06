---
title: 清单： 维护并解决 BizTalk Server 数据库 |Microsoft 文档
description: 请参阅最佳实践，以帮助保持你的 BizTalk Server 数据库，包括自动更新统计信息，最大并行度，重新生成索引、 查找锁定和块，检查数据库大小、 使用跟踪，启用 SQL Server 代理作业、 检查挂起的实例，并检查磁盘性能。 请参阅有关 BizTalk 终止符工具。
ms.custom: ''
ms.date: 06/11/2018
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 58931faf-fc84-46fe-8359-506da94c3756
caps.latest.revision: 4
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 821521713a615189246e801483ccb8fd8b43300a
ms.sourcegitcommit: 7deb2b5a17d740b777a17566d557b25bdd505302
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35290393"
---
# <a name="checklist-maintaining-and-troubleshooting-biztalk-server-databases"></a>清单： 维护和故障排除 BizTalk Server 数据库
BizTalk Server 数据库和它们的运行状况是成功的 BizTalk Server 数据库邮件服务环境非常重要。 本主题列出在维护或故障排除的 BizTalk Server 数据库时必须遵循的步骤。  
  
-   [维护 BizTalk Server 数据库](../technical-guides/checklist-maintaining-and-troubleshooting-biztalk-server-databases.md#BKMK_MaintainDB)  
  
-   [故障排除的 BizTalk Server 数据库](../technical-guides/checklist-maintaining-and-troubleshooting-biztalk-server-databases.md#BKMK_Troubleshoot)  
  
<a name="BKMK_MaintainDB"></a>   
## <a name="maintaining-biztalk-server-databases"></a>维护 BizTalk Server 数据库  
  
|步骤|参考|  
|---|---|  
|禁用**自动更新统计信息**和**自动创建统计信息**选项 （仅适用于 BizTalk Server MessageBox 数据库）。 | **注意：** BizTalk Server 配置的一部分默认情况下完成这些设置。 你不应更改这些设置。 <br/><br/> 若要查看这些设置将被禁用，请在 SQL Server 中执行以下存储的过程：<br/><br/> 选择 DATABASEPROPERTYEX('BizTalkMsgBoxDB', 'IsAutoCreateStatistics') AS IsAutoCreateStatistics<br/>选择 DATABASEPROPERTYEX('BizTalkMsgBoxDB', 'IsAutoUpdateStatistics') AS IsAutoUpdateStatistics<br/><br/>返回值应是**0**以指示设置处于禁用状态。 如果**0**是未返回，禁用此设置通过在 SQL Server 中执行以下：<br/><br/>ALTER 数据库 BizTalkMsgBoxDB 集 AUTO_CREATE_STATISTICS 关闭<br/>ALTER 数据库 BizTalkMsgBoxDB 集 AUTO_UPDATE_STATISTICS 关闭<br/><br/> 有关这些设置的详细信息，请参阅：<br/><br/> -   **917845**-["你遇到阻止，死锁条件或其他 SQL Server 问题，当你尝试连接到 BizTalk Server 中的 BizTalkMsgBoxDb 数据库时"](http://go.microsoft.com/fwlink/?LinkId=153429)<br />-   **912262**-["自动更新统计信息选项的自动创建统计信息选项和承载 BizTalk Server BizTalkMsgBoxDB 数据库的 SQL Server 数据库实例中关闭的并行度设置"](http://go.microsoft.com/fwlink/?LinkId=153430)|  
|设置最大并行度属性度|**注意：** BizTalk Server 配置的一部分默认情况下完成这些设置。 你不应更改这些设置。 <br /><br /> 设置最大并行度**run_value**和**config_value**为一 (1) 上承载 BizTalk Server Messagebox 数据库的 SQL Server 实例的值的属性。 若要检查最大并行度设置度，请执行以下存储过程对主 SQL Server 中的数据库：<br /><br /> exec sp_configure 'max degree of parallelism<br /><br /> 如果**run_value**和**config_value**是未设置为值一 (1)，在 SQL Server 中执行以下存储的过程：<br /><br /> exec sp_configure 'max degree of parallelism'、 '1' reconfigure 替代方法<br /><br /> 有关如何最大并行度设置度影响 BizTalk Server 的详细信息，请参阅以下 Microsoft 知识库文章：<br /><br /> -   **899000**-["的实例的 SQL Server 配置 BizTalk Server 时的并行度设置"](http://go.microsoft.com/fwlink/?LinkId=153432) (http://go.microsoft.com/fwlink/?LinkId=153432)。<br />-   **917845**-["你遇到阻止，死锁条件或其他 SQL Server 问题，当你尝试连接到 BizTalk Server 中的 BizTalkMsgBoxDb 数据库时"](http://go.microsoft.com/fwlink/?LinkId=153429) (http://go.microsoft.com/fwlink/?LinkId=153429)。|  
|确定当重新生成 BizTalk Server 索引|聚集大部分 BizTalk Server 数据库中的索引 (索引 ID: 1)。 DBCC SHOWCONTIG 命令可以用于显示 BizTalk Server 数据库中表的碎片信息。 这些索引是基于 GUID 的因此是正常的碎片发生。 如果 DBCC SHOWCONTIG 扫描密度值是小于 30%，可以在停机期间重新生成索引。 在 BizTalk Server 数据库中的多个表包含使用数据类型定义不能执行联机索引的列。 因此，在 BizTalk Server 数据库中的表的索引应永远不会重新生成时 BizTalk 正在处理数据。 有关如何重新生成 BizTalk 索引的详细信息，请参阅以下 Microsoft 知识库文章：<br /><br /> -   **917845**-["你遇到阻止，死锁条件或其他 SQL Server 问题，当你尝试连接到 BizTalk Server 中的 BizTalkMsgBoxDb 数据库时"](http://go.microsoft.com/fwlink/?LinkId=153429) (http://go.microsoft.com/fwlink/?LinkId=153429)。<br /><br /> **注意：** 还可以使用 sys.dm_db_index_physical_stats 函数以查找 SQL Server 中的碎片信息。 有关详细信息，请参阅[sys.dm_db_index_physical_stats (TRANSACT-SQL)](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql)。|  
|监视数据库的锁、 块或死锁|它是锁和块发生于 BizTalk Server 使用的 SQL Server 数据库的预期的行为。 但是，因此不应具有这些锁或块的时间长的时间继续。 BizTalk Server 使用的数据库扩展阻止和 SQL Server 上死锁情况进行的潜在问题的指示器。 当前已知的死锁情况和 BizTalk Server 使用的 SQL Server 数据库上阻止的原因，查看以下 Microsoft 知识库文章：<br /><br /> -   **917845**-["你遇到阻止，死锁条件或其他 SQL Server 问题，当你尝试连接到 BizTalk Server 中的 BizTalkMsgBoxDb 数据库时"](http://go.microsoft.com/fwlink/?LinkId=153429) (http://go.microsoft.com/fwlink/?LinkId=153429)。|  
|监视数据库和表的大小|BizTalk Server Messagebox 数据库的大小通常应不超过大约 5 GB。  BizTalkMsgBoxDb 数据库不应为保存任何数据，并且应被视为缓冲区，直到处理数据或将其移到 BizTalkDTADb 数据库。 具有强大的 SQL Server 后端和多长时间运行的业务流程的环境可能具有 BizTalkMsgBoxDb 数据库大于 5 GB。 任何长时间运行业务流程的大容量环境应具有 BizTalk Server Messagebox 数据库远小于 5 GB。 BizTalk Server 跟踪数据库可能大不相同的大小，但如果查询性能会显著降低，然后跟踪数据库可能是太大。 根据经验，大于 15 到 20 GB 的 BizTalk Server 跟踪数据库被视为太大，可能会对性能产生不利影响。 以下问题可能是由引起太大的 BizTalk Server 数据库：<br /><br /> -BizTalk Server Messagebox 数据库将不断增长时仍然很大的数据大小 （而不仅仅是日志文件）。 BizTalk Server 采用较长的时间比平时处理甚至简单消息流方案。<br />组中心查询需要比平时更长时间，并可能甚至超时。<br />-数据库日志文件永远不会被截断。<br />-BizTalk SQL 代理作业运行速度慢于正常。<br />-具有过多行相比为 normal 或者某些表很大得多。<br /><br /> BizTalk Server 数据库会变得大的原因包括：<br /><br /> -BizTalk SQL 代理作业未运行<br />-过多挂起的消息或服务实例<br />磁盘故障<br />-高级别的跟踪<br />-BizTalk Server 限制<br />的 SQL Server 性能降低<br />网络延迟问题<br /><br /> 同样，你可以在表中有太多行。 没有任何组具有太多的行数。 此外，此数目的行因表中存储什么类型的数据而异。 例如， *dta_DebugTrace*可能具有多个 100 万行的表具有行过多。 A *HostNameQ_Suspended*可能有多个 200,000 行的表具有行过多。<br /><br /> 请确保你知道的预期内容你的环境以确定是否在发生数据问题。|  
|启用 BizTalk Server 主机上的跟踪|默认情况下，默认主机上启用跟踪。 BizTalk 需要**允许主机跟踪**选项检查一台主机上。 跟踪数据解码服务 (TDDS) 启用跟踪后，将跟踪移动到 BizTalk Server 跟踪数据库从 BizTalk Server Messagebox 数据库的事件数据。 如果没有 BizTalk Server 主机配置为具有选项**允许主机跟踪**或如果跟踪主机已停止，则将不会运行 TDDS 和 BizTalk Server Messagebox 数据库中的 TrackingData_x_x 表将会增长未选中状态。 因此，应将专用的 BizTalk Server 主机配置的选项**允许主机跟踪**。 有关配置专用的跟踪主机的详细信息请参阅[配置专用的跟踪主机](~/technical-guides/configuring-a-dedicated-tracking-host.md)。 **注意：** 若要允许 TDDS 维护在大容量方案中的新跟踪事件，你可以创建单个跟踪主机的多个实例，但不是能超过一个主机应配置对其进行跟踪。|  
|使用正确的 BizTalk SQL Server 代理作业|用于管理 BizTalk Server 数据库以及保持最佳性能，BizTalk Server SQL 代理作业的执行至关重要。<br /><br /> -**备份 BizTalk Server** SQL Server 代理作业是唯一受支持的方法，以将 BizTalk Server 数据库备份。 此作业需要将 BizTalk Server 中的所有数据库都设置为使用完整恢复模式。 你应配置此作业的一个正常的 BizTalk Server 环境。 SQL Server 方法可用于将 BizTalk Server 数据库备份，仅当 SQL Server 服务已停止并且 BizTalk Server 中的所有进程都已都停止。 **注意：** 有关配置 SQL 代理备份 BizTalk Server 作业时使用的 SQL Server 完整恢复模型的详细信息，请参阅[日志传送](http://go.microsoft.com/fwlink/?LinkId=153450)(http://go.microsoft.com/fwlink/?LinkId=153450)或[备份在完整恢复模型](http://go.microsoft.com/fwlink/?LinkId=156509)(http://go.microsoft.com/fwlink/?LinkId=156509)。<br />- **MessageBox_Message_ManageRefCountLog_BizTalkMsgBoxDb** SQL Server 代理作业旨在无限期运行。 因此 SQL 代理作业历史记录可能不表示此 SQL 代理作业已成功完成;此行为是设计使然。 如果失败，作业将在 1 分钟内重新启动，并继续运行全速。 因此，通常可以忽略此作业的失败通知。 如果 MessageBox_Message_ManageRefCountLog_BizTalkMsgBoxDb SQL Server 代理作业的作业历史记录表示此作业是不断发生故障，重新启动到可能的原因的进一步调查的失败/重新启动周期可能需要。<br />- **MessageBox_Message_Cleanup_BizTalkMsgBoxDb** SQL Server 代理作业是仅应手动启用，因为它由 MessageBox_Message_ManageRefCountLog_BizTalkMsgBoxDb 作业启动的作业。<br />- **DTA 清除和存档**SQL Server 代理作业清除和存档跟踪的消息通过维护 BizTalk Server 跟踪数据库。 此作业将读取表中的每个行，并比较每个行，以确定是否应删除记录的时间戳。 **注意：** 进行疑难解答时 BizTalk Server SQL Server 代理作业，验证 MessageBox_Message_ManageRefCountLog_BizTalkMsgBoxDb 除外的所有 SQL 代理作业是否都完成未出现错误。 <br /><br /> 有关在 SQL Server 中使用 BizTalk Server SQL 代理作业的详细信息：<br /><br /> -请参阅[数据库结构和作业](http://go.microsoft.com/fwlink/?LinkId=153451)(http://go.microsoft.com/fwlink/?LinkId=153451)。<br />-请参阅[说明 SQL Server 代理作业在 BizTalk Server](http://go.microsoft.com/fwlink/?LinkId=153452) (http://go.microsoft.com/fwlink/?LinkId=153452)。|  
|监视和终止挂起的实例|服务实例可能已挂起 （恢复），或已挂起 （不恢复）。 消息传递、 业务流程或端口，可能是这些服务实例。 BizTalk Server 通过使用组中心数据库页在 BizTalk Server 管理控制台或通过使用 Terminate.vbs 脚本还包含终止和删除这些实例。 有关 Terminate.vbs 脚本的详细信息，请参阅[删除挂起的服务实例](http://go.microsoft.com/fwlink/?LinkId=153453)(http://go.microsoft.com/fwlink/?LinkId=153453)。 **提示：** 你还可以使用终止符工具删除挂起的实例。 [终止符工具](http://go.microsoft.com/fwlink/?LinkId=151931)位于[ http://go.microsoft.com/fwlink/?LinkId=151931 ](http://go.microsoft.com/fwlink/?LinkId=151931)。 使用此工具不支持由 Microsoft 和 Microsoft 则没有此程序的适用性的保证。 使用此程序风险自负。 <br /><br /> 术语"孤立行"和"傀儡"通常是交替使用。 孤立或僵停消息是一条消息，不具有关联的服务实例，通常因为服务实例已终止之前已接收消息。 孤立或僵停服务是一种服务，没有任何关联的消息。 请参阅有关僵停消息和服务的详细信息了解在 BizTalk Server 中的实例[BizTalk Server 中的僵尸](http://go.microsoft.com/fwlink/?LinkId=153454)(http://go.microsoft.com/fwlink/?LinkId=153454)。|  
|监视性能计数器的**PhysicalDisk**性能对象|BizTalk 服务器在一分钟内对 SQL Server 中进行大量的较短的非常快速的事务。 如果 SQL Server 无法承受此活动，你可能会遇到 BizTalk Server 性能问题。 监视器**avg.Disk sec/Read**， **avg.Disk sec/Transfer**，和**avg.Disk sec/Write**性能监视器计数器**PhysicalDisk**性能对象。 最佳值是小于 10 毫秒 （毫秒）。 一个或更大的 20 毫秒的值被视为较差的性能。<br /><br />-有关 BizTalk Server 数据库高可用性的详细信息，请参阅[BizTalk Server 数据库提供高可用性](../core/providing-high-availability-for-biztalk-server-databases.md)。|  
|遵循 BizTalk Server 数据库的最佳实践。|请参阅[维护 BizTalk Server 数据库的最佳实践](~/technical-guides/best-practices-for-maintaining-biztalk-server-databases.md)。|  
  
<a name="BKMK_Troubleshoot"></a>   
## <a name="troubleshooting-biztalk-server-databases"></a>故障排除的 BizTalk Server 数据库  
 执行以下任务与 BizTalk Server 数据库的任何问题进行疑难解答。  
  
|步骤|参考|  
|-----------|---------------|  
|确保所有必需的 BizTalk SQL Server 代理作业处于启用状态且正在运行|所有 BizTalk SQL Server 代理都作业除外**MessageBox_Message_ManageRefCountLog_BizTalkMsgBoxDb**作业应成功为启用并正在运行。 请勿禁用任何其他作业。<br /><br /> 如果发生故障，使用**查看历史记录**以查看错误信息，并相应地解决失败的 SQL Server 中的选项。 请记住， **MessageBox _Message_ManageRefCountLog_BizTalkMsgBoxDb** SQL Server 代理作业将无限期运行。 因此，你只应考虑如果作业历史记录报告作业不断失败和重启。|  
|使用 MsgBoxViewer 工具来分析 BizTalk MessageBox 和其他数据库|**重要说明：** Microsoft，不支持使用此工具和 Microsoft 则没有此程序的适用性的保证。 使用此程序风险自负。 <br /><br /> MsgBoxViewer 工具是可从[ http://go.microsoft.com/fwlink/?LinkId=151930 ](http://go.microsoft.com/fwlink/?LinkId=151930) (http://go.microsoft.com/fwlink/?LinkId=151930)。 MsgBoxViewer 工具可用于故障排除，因为它提供的详细信息表的大小和行计数的 HTML 报表。 报表还可以帮助确定是否限制 BizTalk Server。 此外，此工具提供的 BizTalk Server 数据库和 BizTalk Server 配置的快照。<br /><br /> BizTalk Server 运行时比平常慢，运行 MsgBoxViewer 工具中，单击选中的所有查询**可选查询**选项卡，然后查看生成的 HTML 报告的任何问题。 **摘要报表**部分列出在为红色的黄色的潜在问题的警告。<br /><br /> 此外，MsgBoxViewer 工具可用于确定哪些表是最大和具有大多数记录。 通常增长 larges 的表的列表以及有关如何管理这些表的说明，请参阅[大增长 BizTalk Server 数据库表](~/technical-guides/large-growing-biztalk-server-database-tables.md)。|  
|使用终止符工具来解决问题，如果任何，由 MsgBoxViewer 工具|**重要说明：** Microsoft，不支持使用此工具和 Microsoft 则没有此程序的适用性的保证。 使用此程序风险自负。 <br /><br /> 运行终结器工具，可在[终止符](http://go.microsoft.com/fwlink/?LinkId=151931)(http://go.microsoft.com/fwlink/?LinkId=151931)。 此工具使用户能够轻松地解决由 BizTalk MsgBoxViewer 工具标识的任何问题。 有关如何与 BizTalk MsgBoxViewer 工具集成终止符工具的详细信息，请参阅[使用 BizTalk 终止符，若要解决问题由 BizTalk MsgBoxViewer](http://go.microsoft.com/fwlink/?LinkId=151932) (http://go.microsoft.com/fwlink/?LinkId=151932)。|  
|调查死锁方案|在死锁方案中，启用 SQL Server 上的 DBCC 跟踪，以便死锁信息写入到 SQLERROR 日志。<br /><br /> 在 SQL Server，执行以下语句以启用 DBCC 跟踪死锁方案：<br /><br /> DBCC TRACEON (1222，则为-1)<br /><br /> 您还可以使用 PSSDIAG 实用工具用于收集数据的**Lock: Deadlock**事件和**Lock: Deadlock Chain**事件。 有关 PSSDIAG 实用工具的详细信息，请参阅[PSSDIAG 数据收集实用程序](http://go.microsoft.com/fwlink/?LinkId=153627)(http://go.microsoft.com/fwlink/?LinkId=153627)。<br /><br /> BizTalkMsgBoxDB 数据库是大容量和高事务联机事务处理 (OLTP) 数据库。 与此类数据库中，某些死锁情况预期，并且此死锁情况由 BizTalk Server 引擎内部处理。 在这种情况，在错误日志中不列出任何错误。 后调查死锁情况时，必须使用事件日志中的死锁错误关联正在调查在输出中死锁。|  
|查找阻塞的进程|可以使用 SQL Server 中的活动监视器获取锁定系统进程的服务器进程标识符 (SPID)。 然后可以运行 SQL 事件探查器，以确定在锁定 SPID 中执行的 SQL 语句。 PSSDIAG 实用工具可用于解决 SQL Server 中的锁定和阻塞问题。 该实用工具捕获具有启用阻止脚本的所有 TRANSACT-SQL 事件。 有关 PSSDIAG 实用工具的详细信息，请参阅[PSSDIAG 数据收集实用程序](http://go.microsoft.com/fwlink/?LinkId=153627)(http://go.microsoft.com/fwlink/?LinkId=153627)。<br /><br /> 在 SQL Server，你可以指定**阻塞的进程阈值**设置，以确定 SPID 或 Spid 阻塞时间长于你指定的阈值。 Blocked 的 process threshold 选项有关的详细信息，请参阅[阻塞的进程阈值选项](http://go.microsoft.com/fwlink/?LinkId=153628)(http://go.microsoft.com/fwlink/?LinkId=153628)。 **注意：** 时遇到 SQL Server 中的锁定或正在阻塞问题，我们建议您与 Microsoft 客户支持服务部门联系。 Microsoft 客户支持服务可以帮助你配置正确的 PSSDiag 实用程序选项。|  
|删除所有不需要的数据|如果数据库已增大，会变得太大，如果在数据库中包含的数据将不会需要过更长，首选的方法是删除的数据。 **注意：** 不要使用此方法在任何环境中知道数据的业务关键型或如果所需要的数据。 <br /><br /> **若要清除 BizTalkMsgBox 数据库**<br /> 1.下载并安装在该终止符工具[Biztalk 终止符](http://go.microsoft.com/fwlink/?LinkId=220869)(http://go.microsoft.com/fwlink/?LinkId=220869)。<br />2.按照本主题中的步骤[如何手动清除数据从测试环境中的 MessageBox 数据库](http://go.microsoft.com/fwlink/?LinkID=158064)(http://go.microsoft.com/fwlink/?LinkID=158064) BizTalk MessageBox 数据库中创建 bts_CleanupMsgbox 存储过程。<br />3.使用终止符工具执行 bts_CleanupMsgbox 存储过程并清除 BizTalk MessageBox 数据库。 **警告：** 确实在运行 BizTalk Server 生产服务器上运行 bts_CleanupMsgbox 存储过程。 您仅应在测试环境中运行 bts_CleanupMsgbox 存储过程。 不支持运行 bts_CleanupMsgbox 在生产环境中的存储的过程。<br />4.重新启动所有主机和 BizTalk Server 服务。<br /><br /> **若要清除 BizTalkDTADb 数据库**<br /> <ul><li>**方法 1**<br /><br /> <ol><li>备份所有 BizTalk Server 数据库。</li><li>执行**dtasp_PurgeAllCompletedTrackingData**存储过程。 有关存储过程的详细信息，请参阅[如何手动清除数据从 BizTalk 跟踪数据库](http://go.microsoft.com/fwlink/?LinkId=153635)(http://go.microsoft.com/fwlink/?LinkId=153635)。</li></ol></li><li>**方法 2**。 仅当 BizTalkDTADb 数据库包含多个未完成的实例，则必须删除，请使用此选项。<br /><br /> <ol><li>备份所有 BizTalk Server 数据库。</li><li>停止所有 BizTalk 主机、 服务和自定义独立的适配器。 如果你使用 HTTP 或 SOAP 适配器，请重新启动 IIS 服务。</li><li>执行**dtasp_CleanHMData** BizTalkDTADb 数据库上的存储过程。</li><li>重新启动所有主机和 BizTalk Server 服务。</li></ol></li></ul> **注意：** 必须具有跟踪数据，备份 BizTalkDTADb 数据库中，如果将数据库还原到另一个 SQL Server，然后清除原始 BizTalkDTADb 数据库。|  
  
 如果你想分析 MsgBoxViewer 数据或 PSSDIAG 输出的帮助，请与 Microsoft 客户支持服务联系。 请联系客户支持服务之前，压缩 MsgBoxViewer 数据、 PSSDIAG 输出和更新的事件日志 （.evt 文件）。 你可能需要发送给 BizTalk Server 这些文件支持工程师。
  
## <a name="next"></a>Next
  
-   [维护 BizTalk Server 数据库的最佳做法](~/technical-guides/best-practices-for-maintaining-biztalk-server-databases.md)  
  
-   [大量增长的 BizTalk Server 数据库表](~/technical-guides/large-growing-biztalk-server-database-tables.md)  
  
-   [用于故障排除的工具和实用程序](../technical-guides/tools-and-utilities-for-troubleshooting.md)  
  
## <a name="see-also"></a>请参阅  
 [不可更改的 SQL Server 设置](~/technical-guides/sql-server-settings-that-should-not-be-changed.md)
