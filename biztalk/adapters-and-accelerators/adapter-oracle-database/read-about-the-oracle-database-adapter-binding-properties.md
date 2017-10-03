---
title: "阅读有关 Oracle 数据库适配器绑定属性 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- binding properties
- binding properties, setting
- adapter, binding properties
ms.assetid: d626136e-c6c1-4352-94fc-3c034c423ef4
caps.latest.revision: "27"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 3c934ec415f336074534ed1add342530bcf2023b
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="read-about-the-oracle-database-adapter-binding-properties"></a>阅读有关 Oracle 数据库适配器绑定属性
[!INCLUDE[adapteroracle](../../includes/adapteroracle-md.md)]呈现几个绑定属性。 通过设置这些属性，可以控制某些适配器的行为。 本部分介绍[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]绑定属性。 它还演示如何访问它们通过使用.NET 编程或通过设置属性[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]物理端口绑定。  
  
## <a name="the-adapter-binding-properties"></a>适配器绑定属性  
 下表显示[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]绑定属性按类别分组。 类别是指在其下每个绑定属性将显示在提供的不同应用程序可配置的适配器 （或绑定） 的对话框中的节点。  
  
|绑定属性|类别|Description|.NET 类型|  
|----------------------|--------------|-----------------|---------------|  
|**CloseTimeout**|常规|[!INCLUDE[nextref_btsWinCommFoundation](../../includes/nextref-btswincommfoundation-md.md)]连接关闭超时。 默认值为 1 分钟。 不提供支持。|System.TimeSpan|  
|**EnableBizTalkCompatibilityMode**|常规|设置到此绑定属性的值**True**时与 BizTalk Server 使用适配器。 否则，必须设置到此绑定属性的值**False**。|bool (System.Boolean)|  
|**InboundOperationType**|常规|指定是否想要执行**轮询**或**通知**入站操作。 默认值是**轮询**。<br /><br /> 有关详细信息**轮询**请参阅[支持基于接收轮询的 Oracle 数据库中的数据更改消息](../../adapters-and-accelerators/adapter-oracle-database/support-for-receiving-polling-based-data-changed-messages-in-oracle-database.md)。 有关详细信息**通知**，请参阅[接收数据库更改通知使用注意事项的 Oracle 数据库适配器](../../adapters-and-accelerators/adapter-oracle-database/before-you-receive-database-change-notifications-using-the-oracle-db-adapter.md)。|枚举|  
|**名称**|常规|一个只读的值，返回生成的文件的名称[!INCLUDE[addadapterservreflong](../../includes/addadapterservreflong-md.md)]来保存[!INCLUDE[nextref_btsWinCommFoundation](../../includes/nextref-btswincommfoundation-md.md)]客户端类。 [!INCLUDE[addadapterservrefshort](../../includes/addadapterservrefshort-md.md)]窗体的值通过追加"客户端"的文件名称**名称**属性。 返回的值是"OracleDBBinding";对于此值，生成的文件将命名为"OracleDBBindingClient"。|string|  
|**OpenTimeout**|常规|ODP.NET 属性。 指定[!INCLUDE[nextref_btsWinCommFoundation](../../includes/nextref-btswincommfoundation-md.md)]连接打开超时。 默认值为 1 分钟。 通过使用 ODP.NET 实现此属性。<br /><br /> **重要说明：** [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]始终使用**OpenTimeout**在打开与 Oracle 数据库的连接时设置的连接打开超时。 适配器将忽略任何超时 (**System.TimeSpan**) 时打开通信对象，例如通道传递的参数。|System.TimeSpan|  
|**ReceiveTimeout**|常规|指定[!INCLUDE[nextref_btsWinCommFoundation](../../includes/nextref-btswincommfoundation-md.md)]消息接收超时。 从根本上来说，这意味着的最大适配器等待入站消息的时间量。 默认值为 10 分钟。<br /><br /> **重要说明：**对于如轮询的入站操作，我们建议将超时设置为最大可能的值，该值是 24.20:31:23.6470000 （24 天）。 使用的适配器时[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]，将超时设置为较大的值不会影响的适配器的功能。|System.TimeSpan|  
|**SendTimeout**|常规|ODP.NET 属性。 指定[!INCLUDE[nextref_btsWinCommFoundation](../../includes/nextref-btswincommfoundation-md.md)]消息发送超时。 默认值为 1 分钟。 不提供支持。|System.TimeSpan|  
|**DataFetchSize**|BufferManagement|ODP.NET 属性。 以字节为单位，从一个服务器往返中的结果集提取 ODP.NET 中指定数据的量。 默认值为 65536。 此属性用于性能优化。|长时间 (System.Int64)|  
|**InsertBatchSize**|BufferManagement|指定对多个记录的插入操作的批大小。 默认值为一个。 值**InsertBatchSize**大于 1，[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]到一个 ODP.NET 调用批处理指定的数目的记录。 如果插入操作中的记录数不是批大小的倍数，最终批将包含较少的记录，比批次大小值。 例如，如果插入消息具有 10 个记录和**InsertBatchSize**是设置为 1，适配器读取各个记录并将其写入到 Oracle 数据库。 因此，适配器执行对 Oracle 数据库 10 个单独的操作。 同样，如果插入消息具有 10 个记录和**InsertBatchSize**设置为 5，该适配器将读取和写入的 5 个记录一次到 Oracle 数据库中，因此执行仅 2 个插入操作。<br /><br /> 如果记录的结构不相同跨一个批处理， **Microsoft.ServiceModel.Channels.Common.XmlReaderParsingException**引发异常，事务将回滚整个插入操作的。 精选值**InsertBatchSize**可以大大改善对多个记录的插入操作的适配器性能。|int (System.Int32)|  
|**LongDatatypeColumnSize**|BufferManagement|以字节为单位 (32512) 的 Oracle long 数据类型列指定的最大大小。 默认值为 0。 如果你不执行 long 数据类型上的操作，必须使用默认值。 若要预提取数据，必须指定**-1**为此绑定属性的值。 如果你是，必须显式设置此绑定属性的适当值：<br /><br /> -执行包含的 long 数据类型参数的存储的过程。<br /><br /> -执行包含长整型数据类型的列和 SELECT 语句的表选择操作不包括的主键列。<br /><br /> **注意：**此绑定属性已弃用。|长时间 (System.Int64)|  
|**MaxOutputAssociativeArrayElements**|BufferManagement|指定适配器创建时执行在响应中返回的关联阵列的操作相关联数组的大小。 适配器进行通信到 ODP.NET，反过来创建具体取决于数组大小的缓冲区数组的大小。 默认值为 32。<br /><br /> 执行涉及 PL/SQL 表类型的操作时，此绑定属性很有用。|int (System.Int32)|  
|**MetadataPooling**|BufferManagement|ODP.NET 属性。 指定是否 ODP.NET 缓存执行的查询的元数据信息。 默认值是**True**，从而使元数据池。 缓存此信息提高性能;但是，如果对基础 Oracle 项目的更改发生在 Oracle 系统，此共用的元数据将同步。这可能导致对 Oracle 系统返回意外的异常执行的操作。 此属性用于性能优化。|bool (System.Boolean)|  
|**StatementCachePurge**|BufferManagement|ODP.NET 属性。 指定连接返回到连接池时是否清除与连接关联的 ODP.NET 语句缓存。 默认值是**False**，这将禁用语句缓存清除。 此属性用于性能优化。|bool (System.Boolean)|  
|**StatementCacheSize**|BufferManagement|ODP.NET 属性。 指定的最大可由每个 ODP.NET 连接缓存的语句数。 此属性设置为非零值启用语句缓存的连接。 默认值为 10。 此属性用于性能优化。|int (System.Int32)|  
|**EnablePerformanceCounters**|诊断|指定是否启用[!INCLUDE[afproductnameshort](../../includes/afproductnameshort-md.md)]性能计数器和[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]LOB 延迟性能计数器。 默认值是**False**; 性能计数器已禁用。 LOB 延迟性能计数器测量所花费的总时间[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]中对 Oracle 数据库进行调用。|bool (System.Boolean)|  
|**EnableSafeTyping**|元数据|启用或禁用安全键入。 默认值是**False**; 安全键入处于禁用状态。 此功能控制如何适配器呈现特定 Oracle 数据类型。 有关安全键入的详细信息，请参阅[基本 Oracle 数据类型 1>](../../adapters-and-accelerators/adapter-oracle-database/basic-oracle-data-types1.md)。|bool (System.Boolean)|  
|**UseSchemaInNameSpace**|元数据|指定是否将架构名称 （SCOTT、 人力资源部门等） 包含在操作和其关联的类型的 xml 命名空间。 默认值是**True**; 架构名称包含在命名空间。 没有命名空间中包含的方案名称的优点是，如果没有具有相同名称 (例如，EMP) 的表中两个不同的架构，则相同的 XML 可以用于执行简单 SQL 上的操作 （插入、 更新、 删除、 选择） 这两个表。<br /><br /> 例如，如果**UseSchemaInNamespace**属性为 true，SCOTT 进行这些操作的命名空间。EMP 表是"http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/EMP";如果为 false，则命名空间为"http://Microsoft.LobServices.OracleDB/2007/03/Table/EMP"。<br /><br /> **重要说明：**的消息操作不受**UseSchemaInNamesapce**绑定属性; 它始终包括架构名称。<br /><br /> **重要说明：**我们强烈建议将此绑定属性设置为**True**生成元数据时。 如果此属性设置为 false 时，Oracle 架构名称 (例如，SCOTT) 将不能生成的架构的 XML 命名空间中。 因此，如果有两个表具有相同名称在两个不同的 Oracle 架构中，以及将它们添加到相同的 BizTalk 项目，BizTalk 项目将无法生成和部署。 如果你想要在相同的 BizTalk 项目中包含此类架构，则必须手动编辑它们以包括 XML 命名空间中的 Oracle 架构名称。|bool (System.Boolean)|  
|**NotificationPort**|通知|指定 ODP.NET 必须打开侦听从 Oracle 数据库的数据库更改通知的端口号。 默认值为-1，表示 ODP.NET 使用有效的、 随机的未使用的端口号。<br /><br /> **重要说明：**适配器客户端将不会收到数据库更改通知，如果 Windows 防火墙处于打开状态。 此外，关闭 Windows 防火墙，以接收通知并不是建议。 因此，若要接收通知，而不会影响客户端计算机的安全性，我们建议指定正整数值为端口号，然后将该端口号添加到 Windows 防火墙例外列表。 如果将此绑定属性设置为默认值为-1，ODP.NET 使用一个随机端口，并且适配器客户端将无法知道哪个端口将添加到 Windows 防火墙例外列表。 有关如何将端口添加到 Windows 防火墙例外列表的说明，请参阅[http://go.microsoft.com/fwlink/?LinkID=196959](http://go.microsoft.com/fwlink/?LinkID=196959)。<br /><br /> **注意：**接收通知使用应用程序域中的多个应用程序是否[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]、 **NotificationPort**所有应用程序必须设置为相同的端口的绑定属性数。 这是因为 ODP.NET 创建只有一个侦听器，它在应用程序域内的一个端口上侦听。|int (System.Int32)|  
|**NotificationStatement**|通知|指定用来注册获取通知从 Oracle 数据库的 SELECT 语句。 SELECT 语句可能类似于以下示例。<br /><br /> `SELECT TID,ACCOUNT,PROCESSED FROM SCOTT.ACCOUNTACTIVITY WHERE PROCESSED = ‘n’`<br /><br /> **注意：**必须指定数据库对象的名称以及架构名称。 例如， `SCOTT.ACCOUNTACTIVITY`。<br /><br /> 仅在指定的 SELECT 语句更改的结果集时该适配器从 Oracle 数据库中获取一条通知消息。|string|  
|**NotifyOnListenerStart**|通知|指定适配器是否将通知消息发送到适配器客户端，通知的接收位置正在运行，侦听器启动时。 默认值是**True**。|bool (System.Boolean)|  
|**ConnectionLifetime**|OracleConnectionPool|ODP.NET 属性。 指定以秒为单位的连接的最大持续时间。 默认值为 0。 此属性用于性能优化。|int (System.Int32)|  
|**DecrPoolSize**|OracleConnectionPool|ODP.NET 属性。 指定已关闭时，如果过多的建立连接未被使用的连接数。 默认值为 1。 这用于性能优化。|int (System.Int32)|  
|**IncrPoolSize**|OracleConnectionPool|ODP.NET 属性。 指定要请求新的连接以及 ODP.NET 连接池中没有可用连接时，创建的新连接的数目。 默认值为 5。 此属性用于性能优化。|int (System.Int32)|  
|**MaxPoolSize**|OracleConnectionPool|ODP.NET 属性。 指定在 ODP.NET 连接池中的最大连接数。 默认值为 100。 此属性用于性能优化。<br /><br /> **重要说明：**必须设置**MaxPoolSize**谨慎。 如果此值设置过大，它是可能会耗尽 ODP.NET，从可用连接数。|int (System.Int32)|  
|**MinPoolSize**|OracleConnectionPool|ODP.NET 属性。 指定在 ODP.NET 连接池中的最小连接数。 默认值为 1。 此属性用于性能优化。|int (System.Int32)|  
|**UseOracleConnectionPool**|OracleConnectionPool|ODP.NET 属性。 指定是否使用 ODP.NET 连接池。 默认值是**True**，从而使连接池。 [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]实现通过使用 ODP.NET 连接池的连接池。|bool (System.Boolean)|  
|**PolledDataAvailableStatement**|PollingReceive|指定执行，以确定任何数据是否可用于轮询的特定表的 SELECT 语句。 指定的语句必须返回的结果集行和列组成。 结果集的第一个单元中的值指示适配器是否执行指定的值**PollingStatement**绑定属性。 如果结果的第一个单元包含一个正值，适配器执行的轮询语句。 例如，将为此绑定属性有效的语句：<br /><br /> `Select * from <table_name>`<br /><br /> 此绑定属性的默认值设置为：<br /><br /> `SELECT 1 FROM DUAL`<br /><br /> 这意味着，适配器必须继续而不考虑轮询表是否具有数据的轮询。<br /><br /> **注意：**您不能指定此绑定属性的存储的过程。 此外，此语句不能修改基础的 Oracle 数据库。|string|  
|**PollingAction**|PollingReceive|指定轮询操作的操作。 你可以确定特定操作从元数据生成操作使用适配器服务外接程序使用的轮询操作。|string|  
|**PollingInterval**|PollingReceive|指定的事务处理的轮询间隔，也就是说，以秒为单位的间隔[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]执行对 Oracle 数据库的轮询语句。 默认值为 500。 以下情况下，由适配器使用的轮询间隔：<br /><br /> 的连续两次轮询之间时间间隔。 此间隔用于运行轮询和后轮询查询。 如果在指定间隔内执行这些查询，该适配器休眠的剩余时间的时间间隔内。<br /><br /> -轮询事务超时值。 此值必须设置为足够大，以包括轮询语句执行时间、 后轮询语句 （如果指定） 执行时和从客户端应用程序以提交事务中接收答复的时间。<br /><br /> 如果客户端应用程序发送答复的轮询间隔到期之前，该适配器将提交事务，并等待，直到达到轮询间隔执行下一次轮询。<br /><br /> 如果客户端应用程序会返回一个错误，该适配器将终止事务。<br /><br /> 如果在客户端应用程序发送回复之前，将过期的轮询间隔，事务将会超时。有关如何在轮询方案中使用绑定属性的详细信息，请参阅[支持基于接收轮询的 Oracle 数据库中的数据更改消息](../../adapters-and-accelerators/adapter-oracle-database/support-for-receiving-polling-based-data-changed-messages-in-oracle-database.md)。|int (System.Int32)|  
|**PollingStatement**|PollingReceive|指定的轮询语句。 你可以指定简单的 SELECT 语句或存储的过程、 函数或打包的过程或函数进行轮询。<br /><br /> -如果你想要轮询的表或视图，你必须指定此绑定属性中的 SELECT 查询。<br /><br /> -如果你想要轮询使用存储的过程、 函数或过程或函数在一个包内的，你必须在绑定属性中指定相应的操作的整个请求消息。<br /><br /> 仅当通过执行的语句执行轮询语句**PolledDataAvailableStatement**绑定属性返回的某些数据。<br /><br /> **重要说明：** [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]内 Oracle 事务时，（如果指定） 执行轮询语句和后轮询语句。 如果你正在使用中的 SELECT 语句**PollingStatement**绑定属性，我们建议在您的 SELECT 语句中指定 FOR UPDATE 子句。 这将确保所选的记录，都在事务处理期间将锁定且后轮询语句可以对选定的记录执行任何所需的更新。<br /><br /> 有关如何在轮询方案中使用绑定属性的详细信息，包括 FOR UPDATE 子句中; 的使用请参阅[支持基于接收轮询的 Oracle 数据库中的数据更改消息](../../adapters-and-accelerators/adapter-oracle-database/support-for-receiving-polling-based-data-changed-messages-in-oracle-database.md)。|string|  
|**PollWhileDataFound**|PollingReceive|指定是否[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]忽略轮询间隔和持续轮询 Oracle 数据库时，如果数据中轮询的表。 如果表中可用的任何数据不，该适配器将恢复执行 SQL 语句按照指定的轮询间隔。 默认值是**False**。<br /><br /> 请考虑其中轮询间隔设置为 60 秒，但为 PolledDataAvailableStatement 指定该语句返回的数据可用进行轮询的方案。 然后，适配器执行 PollingInput 绑定属性指定的语句。 假定该适配器需要仅 10 秒钟的时间来执行语句，它将现在必须等待 50 秒，然后再次执行 PolledDataAvailableStatement 并随后执行轮询语句。 相反，若要优化可以设置绑定属性为 true，以便该适配器可以开始执行的下一步轮询 PollWhileDataFound 的性能并重新打开上一轮询周期结束时，就会立即。<br /><br /> **注意：**此绑定属性是适用于轮询对表和视图和使用存储的过程、 函数或打包的过程或函数轮询。|string|  
|**PostPollStatement**|PollingReceive|指定在轮询语句之后和之前 /POLLINGSTMT 消息发送给使用者执行的 PL/SQL 块。 默认值是**null**; 没有后轮询语句。 轮询事务内执行后轮询语句。 后轮询语句的两个常见用途包括：<br /><br /> -更新轮询语句，以指示它们是已处理并且不需要从后续轮询查询所返回的行中的列。<br /><br /> -移动处理到另一个表的记录。<br /><br /> **重要说明：**如果未指定后期轮询语句， **PollingInterval**应设置为足够大，以便用于完成时间间隔到期之前的 PL/SQL 块。<br /><br /> 有关如何在轮询方案中使用绑定属性的详细信息，请参阅[支持基于接收轮询的 Oracle 数据库中的数据更改消息](../../adapters-and-accelerators/adapter-oracle-database/support-for-receiving-polling-based-data-changed-messages-in-oracle-database.md)。|string|  
|**SkipNilNodes**|运行时行为|指定是否[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]插入或更新请求 XML 中将被标记为 nil 的节点的值将跳过。 此绑定属性是适用于插入或更新表中的记录和记录的存储过程中的类型参数。 默认值是**True**，这意味着该适配器将跳过将被标记为 nil 的节点的值传递。 在这种情况下，Oracle （如果指定） 中的默认值是考虑到标记为 nil 的节点。 如果设置为**False**，适配器显式传递这些节点的 null 值。<br /><br /> **注意：**对于在请求 XML 中不存在的节点，该适配器始终跳过将值，而不考虑的值传递**SkipNilNodes**绑定属性。对于 PL/SQL 表的记录，该适配器将始终传递节点被标记为 nil 或不存在请求的 XML，不管的值中的 null 值**SkipNilNodes**绑定属性。<br /><br /> 下面的示例说明根据为此绑定属性设置的值为适配器配置中的差异。 假设请求 XML 如下所示：<br /><br /> `<EMPNO>1000</EMPNO> <ENAME>John</ENAME> <SAL nil=’true’></SAL>`<br /><br /> 如果**SkipNilNodes**设置为**True**，适配器执行以下命令：<br /><br /> `INSERT INTO EMP (EMPNO, ENAME) VALUES (1000, “John”);`<br /><br /> 如果**SkipNilNodes**设置为**False**，适配器执行以下查询：<br /><br /> `INSERT INTO EMP (EMPNO, ENAME, SAL) VALUES (1000, “John”, null);`<br /><br /> 请注意，在第二个语句中，适配器显式插入参数"SAL"的 null 值。|bool (System.Boolean)|  
|**UseAmbientTransaction**|中的|指定是否[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]执行使用由调用方提供的事务上下文的操作。 默认值是**True**，这意味着，适配器始终执行操作在事务上下文中，假设客户端提供的事务上下文。 如果没有参与该事务的其他资源，创建的连接在 System.Transaction 中登记，并且会提升为 MSDTC 事务。<br /><br /> 但是，可以在你不希望在事务上下文中执行操作的适配器的方案。 例如：<br /><br /> -时执行简单的选择操作 Oracle 数据库 （在上发送端口）。<br /><br /> 而指定轮询语句执行选择操作并不涉及对表的 DELETE 语句通过或通过调用存储的过程 （在接收端口） 上的任何更改。<br /><br /> 这两个操作不要对数据库表进行任何更新，因此，从而提升这些操作使用 MSDTC 事务可以是性能开销。 在这种情况下，可以将绑定属性设置为 false，以便[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]没有在事务上下文中执行的操作。<br /><br /> **注意：**最好仅对未对数据库进行更改的操作未在事务上下文中执行操作是。 对于更新数据库中的数据的操作，我们建议将绑定属性设置为 true; 否则为既可能会遇到消息丢失或重复消息，具体取决于您执行的入站或出站操作。|bool (System.Boolean)|  
|**GeneratedUserTypesAssemblyFilePath**|UDT.NET 类型生成设计时|指定的名称和适配器生成时生成元数据，包含的元数据中使用的所有 Udt 的 dll 的路径。 如果正在生成包、 存储的过程或函数，以便用 Udt 的元数据，必须指定 DLL 名称。 指定 DLL 名称是可选的表和具有 Udt 的视图。 生成的 DLL 将保存到与可执行文件相同的位置。<br /><br /> 只有在生成元数据时，此绑定属性是必需的。<br /><br /> **注意：**必须指定一个文件名。 元数据中的所有 udt，适配器生成具有给定名称的单个文件。 如果不指定一个名称，适配器将生成的 GUID 名称与 DLL。 此绑定属性不是 BizTalk Server 中提供配置时**WCF OracleDB**接收或发送端口。|string|  
|**GeneratedUserTypesAssemblyKeyFilePath**|UDT.NET 类型生成设计时|指定的名称和密钥文件适配器用来创建强类型的程序集的路径。<br /><br /> 此绑定属性是可选的只有在生成元数据时才需要。<br /><br /> **注意：**此绑定属性不是 BizTalk Server 中提供配置时**WCF OracleDB**接收或发送端口。|string|  
|**UserAssembliesLoadPath**|UDT.NET 类型生成运行时|指定的 Dll，以分号，这将生成元数据时创建的适配器分隔的名称。 在为指定的位置保存这些 Dll **GeneratedUserTypesAssemblyFilePath**生成元数据时绑定属性。 你必须手动将这些 Dll 复制到以下位置：<br /><br /> **对于 BizTalk 项目**： 复制 Dll 作为 BTSNTSvc.exe 所在的位置。 有关[!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)]，这是通常下提供\<安装驱动器 >: files\microsoft [!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)]。<br /><br /> **对于.NET 项目**： 将 Dll 复制到你的.NET 项目文件夹中的 \bin\Development 文件夹中。<br /><br /> 只有在发送和接收消息，在 Oracle 数据库上执行操作时，此绑定属性是必需的。|string|  
|**AcceptCredentialsInUri**|不显示[!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]或[!INCLUDE[addadapterservrefshort](../../includes/addadapterservrefshort-md.md)]。|指定 Oracle 连接 URI 是否可包含 Oracle 数据库的用户凭据。 默认值是**False**，这将禁用连接 URI 中的用户凭据。 如果**AcceptCredentialsInUri**是**False**和 Oracle 连接 URI 包含用户凭据[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]引发异常。 你可以设置**AcceptCredentialsInUri**到**True**如果必须在 URI 中指定凭据。 有关详细信息，请参阅[创建 Oracle 数据库连接 URI](../../adapters-and-accelerators/adapter-oracle-database/create-the-oracle-database-connection-uri.md)。|bool (System.Boolean)|  
  
## <a name="how-do-i-set-oracle-binding-properties"></a>如何设置绑定属性的 Oracle？  
 指定与 Oracle 数据库的连接时，你可以设置 Oracle 绑定属性。 有关如何设置绑定属性的信息时您：  
  
-   使用[!INCLUDE[consumeadapterservlong](../../includes/consumeadapterservlong-md.md)]或[!INCLUDE[addadapterservreflong](../../includes/addadapterservreflong-md.md)]，请参阅[连接到 Visual Studio 使用使用适配器服务中的 Oracle 数据库](../../adapters-and-accelerators/adapter-oracle-database/connect-to-oracle-database-in-visual-studio-using-the-consume-adapter-service.md)。  
  
    > [!IMPORTANT]
    >  在使用[!INCLUDE[consumeadapterservlong](../../includes/consumeadapterservlong-md.md)]或[!INCLUDE[addadapterservreflong](../../includes/addadapterservreflong-md.md)]，如果未指定的字符串类型的绑定属性的值，并且其默认值为 null，则该绑定属性将不可用绑定文件 （XML 文件） 或 app.config 文件中分别。 你必须手动添加绑定属性，并且其值在绑定文件或 app.config 文件中，如果需要。  
  
-   配置发送端口或接收端口 （位置） 中[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]解决方案，请参阅[手动配置到 Oracle 数据库适配器的物理端口绑定](../../adapters-and-accelerators/adapter-oracle-database/manually-configure-a-physical-port-binding-to-the-oracle-database-adapter.md)。  
  
-   使用编程解决方案中的 WCF 通道模型，请参阅[创建一个通道，使用 Oracle 数据库](../../adapters-and-accelerators/adapter-oracle-database/create-a-channel-using-oracle-database.md)。  
  
-   使用 WCF 服务模型编程解决方案中，请参阅[配置客户端绑定用于 Oracle 数据库](../../adapters-and-accelerators/adapter-oracle-database/configure-a-client-binding-for-the-oracle-database.md)。  
  
-   使用 WCF ServiceModel 元数据实用工具 (svcutil.exe)，请参阅[ServiceModel 元数据实用工具使用 BizTalk 适配器将用于 Oracle 数据库](../../adapters-and-accelerators/adapter-oracle-database/use-the-servicemodel-metadata-utility-with-the-oracle-db-adapter-in-biztalk.md)。  
  
## <a name="see-also"></a>另请参阅  
 [BizTalk 应用程序部署的开发任务](../../core/development-tasks-for-biztalk-application-deployment.md)