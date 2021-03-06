---
title: 在多计算机环境中安装 BizTalk Server |Microsoft Docs
description: 当 BizTalk 和 SQL Server 安装在不同的计算机，其中包括 BAM 上多服务器安装和设置指南
ms.custom: ''
ms.date: 09/27/2018
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e4d0e707-6b9e-49e1-9f17-19b3bac1229e
caps.latest.revision: 27
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5243cb9dd53fdeec4d3dac46f54f2851befa1b15
ms.sourcegitcommit: 53b16fe6c1b1707ecf233dbd05f780653eb19419
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/01/2018
ms.locfileid: "50753237"
---
# <a name="install-biztalk-server-in-a-multi-computer-environment"></a>在多计算机环境中安装 BizTalk Server

## <a name="overview"></a>概述

有许多事情需要考虑在计划的 Microsoft® BizTalk® Server 多计算机安装。 通常的网络基础结构存在和 BizTalk Server 必须与其他网络应用程序共存。 本指南介绍了一些适用于 BizTalk Server 和多计算机的分布式部署中的业务活动监视 (BAM) 安装的注意事项。 此信息可帮助您计划安装和配置 BizTalk Server 和业务活动监视 (BAM) 和应用程序和组件依赖于。

单服务器安装指南包含一些重要过程和在本文档中不重复的更多背景信息。 例如，在单服务器安装指南中详细讨论了以下信息：

- 详细的安装过程
- BizTalk Server 功能和依存关系的说明
- BizTalk Server 基本配置设置的详细信息
- 软件和硬件要求
- CAB 文件可再发行组件列表

## <a name="high-availability"></a>高可用性
BizTalk Server 提供了使用网络负载平衡 (NLB) 群集和故障转移群集和 SQL Server Always On 使用可用性组 (AG) 的高可用性解决方案。 高可用性解决方案可帮助硬件或软件故障时尽量减少停机时间。 

**NLB 和故障转移群集**相互补充在复杂的体系结构中。 NLB 群集用于前端 Web 服务器之间的负载平衡请求。 故障转移群集为 BizTalk Server 进程内宿主、企业单一登录主密钥服务器以及 BizTalk Server 数据库提供高可用性。 这通常用于在本地环境。 以下是有用的资源： 

* [BizTalk Server：高可用性生存指南](http://social.technet.microsoft.com/wiki/contents/articles/6532.biztalk-server-high-availability-survival-guide.aspx)

* [通过使用 Windows Server 故障转移群集或 Windows Server 群集改进 BizTalk Server 中的容错能力](http://go.microsoft.com/fwlink/p/?LinkId=154499)

**SQL Server Always On AG**可用与在本地环境和 Azure 虚拟机。 可用性组支持 BizTalk Server 2016 开始，任何较新版本的 BizTalk Server 中支持。 可用性组包含主数据库副本和辅助数据库副本。 BizTalk Server 连接到主数据库副本，而辅助数据库副本提供冗余和故障转移。 [Always On 可用性组 (SQL Server)](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/always-on-availability-groups-sql-server)提供可用性组的工作原理的详细信息。 

[BizTalk HA 使用 SQL Server Always On AG](../core/high-availability-using-sql-server-always-on-availability-groups.md)从 BizTalk 的角度提供更多详细信息。

## <a name="separate-runtime-and-administration"></a>单独的运行时和管理
BizTalk Server 支持在生产环境中实施多种安装方案。 例如，您可以在一台计算机上安装、配置和部署仅限运行时的安装，在第二台计算机上执行仅限管理工具的安装。

在仅限管理工具安装期间，将安装以下组件：BizTalk 管理控制台、BM.exe 和 BTSDeploy.exe。 创建仅管理工具的 BizTalk Server 安装时需要考虑以下事项：

- SQL Server 代理必须运行在作为 BizTalk Server MessageBox 数据库宿主的所有计算机上。 SQL Server 代理需要跟踪 BizTalk Server 消息引擎中的消息正文。

- 当你运行 BizTalk Server 配置向导时，将创建 Analysis Services 数据库。

- 不支持联合使用 BizTalk 跟踪数据库和 SQL Server Analysis Services。

- 不支持使用 SQL Server Analysis Services 的命名实例。

若要仅安装管理工具为 BizTalk Server，请选择仅**管理工具**在安装过程。 在完成安装后，打开自定义配置管理器并且加入现有的企业单一登录 (SSO) 系统和 BizTalk 组。
返回页首

## <a name="enable-msdtc"></a>启用 MSDTC
在多计算机环境中安装和配置 BizTalk Server 之前，请启用所有 BizTalk Server 上的网络 DTC 访问和网络 COM+ 访问以及 BizTalk Server 使用的任何远程 SQL Server 实例。 请参阅[用于优化环境的配置后步骤](post-configuration-steps-to-optimize-your-environment.md)。

其他：

- 所有 BizTalk server 和 SQL 服务器组中必须都具有相同的远程过程调用 (RPC) 身份验证级别应用。 DTC 代理可能不正确时进行身份验证 DTC 的计算机使用不同的操作系统、 连接到工作组，或位于不同域不信任彼此。 请参阅[MSDTC 无法相互进行身份验证](https://msdn.microsoft.com/library/ms686976(VS.85).aspx)。

- 如果使用防火墙，请打开所需的 DTC 和 RPC 端口。 请参阅[服务概述和网络端口要求 Windows](http://support.microsoft.com/kb/832017)。

- 若要确保 DTC 设置正确无误，请使用 DTC 测试人员和 DTC Ping 工具。 这些工具以及 DTC 疑难解答的详细，请参阅[BizTalk Server-MSDTC 疑难解答](https://social.technet.microsoft.com/wiki/contents/articles/2031.biztalk-server-troubleshooting-problems-with-msdtc.aspx)。

## <a name="remote-sql-server"></a>远程 SQL Server
如果在远程计算机上安装了 SQL Server:

- [SQL Server 管理工具](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)（较新的 SQL 版本） 或 SQL Server 客户端工具连接 （较旧的 SQL 版本） 必须安装本地 BizTalk Server 计算机上，当 SQL Server 是远程数据库。 SQL Server Tools 安装所需的 SQL Server 远程实例进行通信的客户端库。 本地 BizTalk Server 计算机上的 SQL Server 工具的版本必须是远程的 SQL Server 安装的版本相同。

- 如果您计划远程使用 Analysis Services，则 SQL Server OLAP 客户端必须安装在本地计算机上。 OLAP 客户端可能随附[SQL Server 2016 功能包](https://www.microsoft.com/download/details.aspx?id=52676)。

- 在 BizTalk Server 配置期间必须运行远程 SQL Server。

- 您在 SQL Server 安装过程中指定的 TCP 和 UDP 端口在 BizTalk Server 配置期间必须打开。

- 若要配置 BAM 工具，请在 BizTalk BAM 服务器上安装 SQL Server 管理工具（基本工具和完整工具）。 有关设置和多计算机环境中配置 BAM 的详细信息，请参阅[安装并配置 BAM （业务活动监视） 在多计算机环境中](https://social.technet.microsoft.com/wiki/contents/articles/1888.install-and-configure-bam-business-activity-monitoring-in-a-multi-computer-environment.aspx)。 

- 不支持的 SQL Server Analysis Services 命名的实例。

### <a name="sql-server-topologies"></a>SQL Server 拓扑
在 BizTalk 服务器上，或在另一台服务器专用于 SQL Server 上，可以本地安装 SQL Server。 大多数生产方案包括 BizTalk Server 和 SQL Server 安装在单独的计算机上。 

有关受支持的 SQL Server 版本的列表，请参阅： 

* [BizTalk Server 2016 软件要求](hardware-and-software-requirements-for-biztalk-server-2016.md) 
* [BizTalk Server 2013R2 和 2013年软件要求](hardware-and-software-requirements-for-biztalk-server-2013-and-2013-r2.md)

> [!IMPORTANT]
> 支持其他 Service Pack 和 Windows Update，并且应进行安装。

### <a name="maintain-and-troubleshoot-databases"></a>维护和故障排除的数据库

请参阅[如何维护和故障排除 BizTalk Server 数据库](http://support.microsoft.com/kb/952555)。

## <a name="business-activity-monitoring-bam"></a>业务活动监视 (BAM)
BizTalk Server 提供了多种工具的信息工作者，在它们之间 BAM。 组件体系结构的一个基本了解可帮助你规划 BizTalk Server 安装，以便利用可用于您的服务器资源。
业务活动监视 (BAM) 是一系列的工具用于管理聚合、 警报和配置文件，以监视相关业务度量，称为关键性能指标或 Kpi。

BAM 是一个模块，可提供端到端可见性业务流程以提供有关状态和结果的各种操作流程和事务的信息。 可以使用 BAM 输出确定出现问题的方面并解决企业内部的问题。 有关 BAM 生命周期的详细信息，请参阅在业务活动监视 (BAM) 海报[BizTalk Server BAP 海报](https://www.microsoft.com/download/details.aspx?id=56123)。

BAM 由以下层组成：

| 层 | 作用 | 示例 | 安装了 |
|---| ---|---|---|
| 表示和工具 | 为业务用户和开发人员提供前端服务。 显示数据，可让业务用户和开发人员定义和管理模板和配置文件;以及其他功能。 | Office Excel，BAM 门户 | Excel、管理工具和自定义用户界面安装在业务用户或开发人员的工作站上。 在 BAM 基础结构的基础上构建的 BAM 门户和自定义 Web 应用程序安装在服务器上。 |
| Web Services 和处理 | 链接表示层和数据库层；实现业务规则和业务流程；聚合和分析数据。 | Windows SharePoint Services (WSS)、贸易合作伙伴管理 Web Services、BAM 管理 Web Services 和 BizTalk Server 引擎。 | 在使用 IIS，SQL 通知服务，并可能为自定义 web 服务，具体取决于应用程序的服务器。 在此服务器上，或在多个具有三个或多台计算机的计算机配置中的独立服务器上，也可以安装 BizTalk 主机服务。 |
| 数据库和平台服务 | 数据存储和检索；安全性和身份验证；网络；操作系统功能 | SQL Server、 Windows Server、 企业单一登录 (SSO)，并故障转移和 NLB 群集 | 在 Windows Server、 SQL Server 的服务器。 出于性能原因，此服务器通常不会不运行 BizTalk 主机服务。 |

### <a name="install-bam"></a>安装 BAM
分步指南：[安装并配置 BAM （业务活动监视） 在多计算机环境中](https://social.technet.microsoft.com/wiki/contents/articles/1888.install-and-configure-bam-business-activity-monitoring-in-a-multi-computer-environment.aspx)

它是更轻松地了解 BAM、 安装和配置过程和依赖项通过将拆分为下表中所述的三个 BizTalk Server 环境：

| 运行时环境 | 设计时环境 | 使用时环境 |
|---|---|---|
| 基本 BizTalk Server 运行时环境可能包括以下服务器： <ul><li>BizTalk Server</li><li>SQL Server</li><li>BizTalk BAM 服务器</li><li>Web 服务器</li></ul> | 在 BAM 开发和部署过程中涉及三个角色。 角色包括： <ul><li>业务分析员</li><li>业务管理员</li><li>应用程序开发人员</li></ul> | 实现和部署 BAM 解决方案之后，业务最终用户可以查看各种报告工具生成的报表。 这些工具包括： <ul><li>BAM 门户 </li><li>SQL Server Reporting Services</li><li>Microsoft PerformancePoint Monitoring Server</li><li>自定义 BAM 报告应用程序</li></ul> |

下表描述了要安装的 BAM 组件：

|类别 |BAM 组件|用途|
|---|---|---|
| 门户组件 | 业务活动监视 | 选择业务活动监视组件将安装的软件，为业务用户提供其异构业务流程，使他们能够做出重要业务决策的实时视图。 |
| 其他软件 | BAM 警报 | 将安装所需的软件，使 BizTalk Server 能够提供业务活动监视 (BAM) 警报。 <br/><br/>BizTalk Server 2013 R2 和更高版本的 BAM 警报使用 SQL Server Database Mail。 不使用或不支持 SQL Notification Services。<br/><br/>BizTalk Server 2013 与 SQL Server 2012 上的 BAM 警报使用 SQL Notification Services。 BizTalk Server 2013 的 SQL Server 2008 R2 上的 BAM 警报使用 SQL Notification Services。 |
| | BAM 客户端 | 选择 BAM 客户端组件将安装必要的客户端软件，使业务用户能够使用 BizTalk Server 的业务活动监视功能。 | 
| | BAM-Eventing | 选择 Bam-eventing 侦听器用于 Windows Workflow Foundation 和 Windows Communication Foundation 的 Bam-eventing Support 组件安装的软件。 选择该组件还可安装用于从自定义应用程序向 BAM 数据库发送事件的 BAM Event API。 Bam-eventing Support 是 BizTalk Server 中的业务活动监视功能的一部分。 | 

### <a name="configure-bam"></a>配置 BAM
分步指南：[安装并配置 BAM （业务活动监视） 在多计算机环境中](https://social.technet.microsoft.com/wiki/contents/articles/1888.install-and-configure-bam-business-activity-monitoring-in-a-multi-computer-environment.aspx)

打开 BizTalk Server 配置，然后选择[自定义配置](configure-biztalk-server.md)。 在自定义配置中，你可以配置高级的选项和有选择地配置或取消配置每项功能。 

### <a name="install-and-configure-sql-server-for-bam"></a>安装和配置 BAM 的 SQL Server

在中[新增功能、 安装、 配置和升级](biztalk-server-what-s-new-installation-configuration-and-upgrade.md)，你可以： 

- 请参阅 BizTalk Server，包括支持的 SQL Server 版本的受支持的软件要求
- 安装必备软件，包括 SQL Server。 有关特定于 SQL Server 的安装步骤，请参阅[安装 SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup)或[安装 SQL Server 2014](https://msdn.microsoft.com/library/bb500469(v=sql.120).aspx)。

除了所需的数据库服务通过 BizTalk Server 核心功能，BAM 还具有以下要求：

- SQL Server Analysis Services (SSAS)

- SQL Server Integration Services (SSIS)

- SQL Server 数据库邮件或 SQL Server Notification Services (SSNS)

##### <a name="configure-ssis"></a>配置 SSIS
如果不在 BizTalk Server 的计算机上安装 SQL Server，然后配置 SSIS。 在此任务中，将 SSIS 配置为使用远程 SQL Server 上的 msdb 数据库。

1. 打开命令提示符。

2. 将目录更改为 %ProgramFiles%\Microsoft SQL Server\100\DTS\Binn。

3. 运行以下命令： notepad MsDtsSrvr.ini.xml

4. 在记事本中，更新内的文本"<ServerName>"标记添加到 SQL Server 的主机名。 保存更改。

5. 从命令提示符下，执行以下命令： net stop MsDtsServer

6. 从命令提示符下，执行以下命令： net start MsDtsServer

    **其他**:  
    默认情况下，Integration Services 服务配置为管理存储在数据库引擎的本地默认实例的 msdb 数据库中的程序包。 若要管理的命名的实例或数据库引擎的远程实例中或在数据库引擎的多个实例中存储的包，修改配置文件。 例如，可以创建 SqlServerFolder 类型的更多根文件夹，以管理数据库引擎的多个实例的 msdb 数据库中的程序包。如果该服务停止，你还可以修改配置文件以允许程序包继续运行。 此选项显示对象资源管理器中的多个根文件夹，或指定由 Integration Services 服务管理的文件系统中的另一个文件夹或多个文件夹。

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDTS\ServiceConfigFile`注册表项指定的位置和 Integration Services 服务使用的配置文件的名称。 注册表项的默认值为 C:\Program Files\Microsoft SQL server\100\dts\binn \ MsDtsSrvr.ini.xml。 可以更新该注册表项的值，以使配置文件使用其他名称和位置。

#### <a name="configure-bam-databases"></a>配置 BAM 数据库
您可以在不同计算机上配置 BAM 主导入数据库、BAM 存档数据库、BAM 星型架构数据库、BAM 分析数据库和 BAM Notification Services 应用程序数据库。 以下是在非 BizTalk Server 的计算机上安装 SQL Server 的软件要求：

| BAM 功能 | 功能配置 | BizTalk Server | SQL Server | 
|---|---|---|---|
|BAM 工具 | BAM 主导入表和 BAM 存档数据库 | ADOMD.NET SQL Server Integration Services | 受支持的 SQL Server 版本。 请参阅[最新内容、 安装、 配置和升级](biztalk-server-what-s-new-installation-configuration-and-upgrade.md)。|
| BAM 工具| 为 BAM 聚合启用 Analysis Services| SQL Server Integration Services| SQL Server Analysis Services| 
| BAM Notification Services 应用程序数据库| BAM 警报| BAM 警报 <br/>中列出的要求[新增功能、 安装、 配置和升级](biztalk-server-what-s-new-installation-configuration-and-upgrade.md)。| 如果使用 SQL Server 2012 或 SQL Server 2014，配置 SQL Server Database Mail。 如果使用 SQL Server 2008 R2，安装 SQL Server 2005 Notification Services 引擎组件。<br/><br/>BAM 警报要求记录在准备安装您的计算机。

> [!NOTE] 
> 用于 OLAP 服务的服务帐户应该对 BAM 星型架构数据库具有 db_datareader 权限。

##### <a name="notification-services--biztalk-2013--sql-server-2008-r2-only"></a>通知服务 – BizTalk 2013 / 仅限 SQL Server 2008 R2

> [!IMPORTANT]
> 当使用 SQL Server 2008 R2，此部分才适用。

您可以在 Notification Services 的提供者、生成者和分发者角色位于不同计算机的多计算机环境中安装 SQL Server Notification Services。 下面介绍该方案中的依存关系：

- AggregationEventProvider.dll 应安装在承载提供程序角色的计算机上。 在 BizTalk Server 安装期间安装 BAM 警报聚合事件提供程序时，将安装此.dll 文件。 如果安装了 BizTalk 运行时、管理工具或者开发人员工具和 SDK，将存在 BAM 警报聚合事件处理程序。

- EmailNotification.xslt 和 FileNotification.xslt 被必需托管分发服务器角色的计算机上。 从现有的 BizTalk Server 复制中的以下路径的文件： BizTalk Server \Program Files\Microsoft*版本*\Tracking

- 托管分发服务器角色的计算机上的.xslt 文件的确切位置更新 Notification Services 应用程序定义文件 （.adf 文件）。 

**更新应用程序定义文件 （.adf 文件）**:  

1. 在计算机上安装 BizTalk Server，打开 Notification Services 命令提示符。
2. 浏览到 files\microsoft BizTalk Server*版本*\Tracking。
3. 执行 ProcessBamNsFiles.vbs 以便创建初始的 .adf 文件。
4. 修改 .adf 文件中 .xslt 文件的路径。
5. 再次执行 ProcessBamNsFiles.vbs 以更新 .adf 文件。
6. 重新启动 BAMAlerts NT 服务。

##### <a name="bam-scale-out-alerts-topology"></a>BAM 向外扩展警报拓扑
如果你要将现有的 BAM 向外扩展警报拓扑升级至 BizTalk Server 2013，则在每个服务器上执行以下步骤：

1. 停止 Notification Service，然后注销 Notification Service 的实例：
    1. 在中**程序**，单击**Microsoft SQL Server 2005**，单击**配置工具**，然后单击**Notification Services 命令提示**.
    1. 在命令提示符处，键入： `net stop NS$<instance_name>`。 例如，键入： `net stop NS$BamAlerts`。
    1. 若要注销该实例，键入以下命令： `nscontrol unregister -name BamAlerts`。 

        注销实例会删除注册表项、NS$instance_name 服务（如果存在），还会删除该服务的性能计数器。

2. 升级到更高版本的 SQL Server 2005 Notification Services 的 Notification Services 实例的服务器。

3. 若要根据您要从升级的 SQL Server 版本将 BAM 数据库迁移，请运行位于 BizTalk Server Tracking 文件夹中的迁移数据库命令 bm.exe 程序。 例如，如果 SQL Server 2005 升级到 SQL Server 2008 R2，运行以下命令在命令提示符中使用管理凭据： `bm.exe migrate-sql –From:sql2005 –To:sql2008 –NSUser:<username>`。

4. 重新注册 Notification Service 除迁移程序 (bm.exe) 正在使用的位置的服务器的所有服务器上。

   1. 在中**程序**，单击**Microsoft SQL Server 2005**，单击**配置工具**，然后单击**Notification Services 命令提示**.
   2. 在命令提示符下键入： `nscontrol register -name BamAlerts -server <NS DB Server> -service -serviceusername "<NSServiceUserName>" -servicepassword "<NSServicePassword>"`

      这可使 Notification Services 登录到正确的数据库 （此信息保留在服务计算机的注册表中由 nscontrol）。

      > [!IMPORTANT] 
      > 请记得使用新的 Notification Services 数据库服务器中重新注册该服务时在-server 选项。 此外，使用新的 Notification Services 服务的同一用户名称与旧。

5. 验证 BAM 警报： 打开**Notification Services 命令提示符**并键入： `nscontrol.exe status –name BAMAlerts –server <NS DB Server>`。

### <a name="bam-portal"></a>BAM 门户
门户组件是一组服务业务人员用来进行通信、 协作和做出决策，使他们能够进行交互，配置和监视业务流程和工作流。 若要使用此功能，安装 Internet 信息服务 (IIS)。 IIS 要求属于[新增功能、 安装、 配置和升级](biztalk-server-what-s-new-installation-configuration-and-upgrade.md)。

### <a name="bam-add-in-from-excel"></a>BAM 外接程序从 Excel
[添加或删除外接程序](https://support.office.com/article/add-or-remove-add-ins-0af570c4-5cf3-4fa9-9b88-403625a0b460)excel 中列出的步骤。 BAM 外接程序名称是**业务活动监视**。

### <a name="configure-multiple-biztalk-groups-to-use-a-single-bam-database"></a>配置多个 BizTalk 组，以使用单个 BAM 数据库
在多个 BizTalk 组间共享 BAM 数据库：

1. 配置具有 BAM 功能的第一个 BizTalk 组。 这些功能包括 BAM 工具、 BAM 分析数据库、 BAM 警报和 BAM 门户。

2. 配置后面的 BizTalk 组并执行 BizTalk Server 配置向导中的以下操作：

   1. 选择**BAM 工具**，然后选择**启用业务活动监视工具**并**为 BAM 聚合启用 Analysis Services**复选框。

   2. 更改**服务器名称**并**数据库名称**的 BAM 数据存储以匹配配置的第一个 BizTalk 组时使用的相同名称。

   3. 选择**BAM 警报**，然后选择**启用 BAM 警报**。

   4. 更改服务帐户为 BAM 警报，因此它是一个空的用户名和密码。

   5. 更改 BAM 警报 SMTP 服务器，BAM 警报文件位置，SQL Server 警报数据库并警报数据库名称以匹配配置的第一个 BizTalk 组时使用的相同名称的前缀。

      > !请注意] 相同的主导入表 (PIT) 可以使用，但使用不同的 BAM 存档、 BAM 分析和星型架构数据库。 但是，此选项会影响使用同一 PIT 的所有组。

3. 选择**BAM 门户**，然后选择**启用 BAM 门户**复选框。

    > [!NOTE]
    > 此屏幕上的所有字段都是只读的，因为在 BAM 主导入数据库和 BAM 门户之间存在一对一的关系。 多个 BizTalk 组共享 BAM 门户时配置对相同的 BAM 数据库。

4. 选择**应用配置**。

### <a name="bam-client-software-requirements"></a>BAM 客户端软件要求
- 对于 web 客户端，您需要 Internet Explorer 和 Office Web Components 11 版本 4.0 或更高版本。

- 如果您运行 web 客户端并使用 SQL Server 2008 R2 Analysis Services，安装 Microsoft SQL Server 2008 R2 Analysis Services 10.0 OLE DB 访问接口。 

- 对于 Excel 客户端，你将需要 Microsoft Excel 和 BAM Excel 外接程序提供与 BizTalk Server。


## <a name="groups-and-service-accounts"></a>组和服务帐户
手动创建所有域组和帐户，然后在多计算机安装中配置 BizTalk Server。 以下信息可在创建这些组和帐户。

在多计算机环境中，BizTalk Server 仅支持域组和域服务帐户。 

- BizTalk Server 仅支持<NetBIOSDomainName>\<用户 > 名称格式的 Windows 组和服务帐户。

- 在多计算机配置中，BizTalk Server 仅支持 Active Directory 域组和用户帐户。 域组包括域本地组、全局组和通用组，在单计算机环境和多计算机环境中均支持这些组。

- 一般情况下，因为它们的使用需要的所有服务器，包括 BizTalk Server 基础结构中的 SQL 服务器，属于同一个域，不建议域本地组。 这一注意事项并不适用于较小的网络，在这些网络中，所有服务器和用户帐户都驻留在单个域中。 [Active Directory 组](http://technet.microsoft.com/library/cc733001.aspx)提供了详细信息。

- 安装和配置 BizTalk Server 在多计算机环境中时，不支持 NT AUTHORITY\LOCAL SERVICE、 NT AUTHORITY\NETWORK SERVICE、 NT AUTHORITY\SERVICE、 NT AUTHORITY\SYSTEM 和 Everyone 之类的内置帐户。

- 运行 BizTalk Server 配置的用户必须属于以下用户组： 本地计算机上的 SQL Server 计算机，用于 BizTalk Server Administrators 域组的系统管理员组上的管理员组组和用于 SSO 管理员组的域组。

- 只要可能，使用在设置期间创建的默认帐户名称。 BizTalk Server 安装程序会自动配置已安装的组件要使用的默认帐户。 使用默认名称可以简化安装和配置，但它并不总是可能。 例如，可以有多个活动域森林内的 BizTalk Server 组。 在此情况下，必须修改帐户名，以避免冲突。 或者，你的组织可能使用的命名标准的服务和用户帐户因此更改默认帐户，以符合标准。

### <a name="windows-groups"></a>Windows 组
下表列出了 BizTalk Server 使用的 Windows 组及其成员。 它还给出了这些组的 SQL Server 角色或数据库角色。

| Group | 组说明 | 成员身份 | SQL Server 角色或数据库角色 | 
| ---|---|---|---|
| SSO Administrators | 企业单一登录 (SSO) 服务的管理员。 [指定 SSO 管理员帐户和关联管理员帐户](../core/how-to-specify-sso-administrators-and-affiliate-administrators-accounts.md)提供了更多信息。 | 包含企业单一登录服务的服务帐户。 包含需要能够配置和管理 BizTalk Server 和 SSO 服务的用户/组。包含用于在配置 SSO 主密钥服务器时运行 BizTalk 配置管理器的帐户。 | **db_owner** sso 的 SQL Server 数据库角色 <br/><br/>**securityadmin** SSO 所在的 SQL server 的 SQL Server 角色。 |
| SSO Affiliate Administrators | 某些 SSO 关联应用程序的管理员。 他们能够创建/删除 SSO 关联应用程序，管理用户映射，以及为关联应用程序用户设置凭据。 | 不包含服务帐户。 包含 BizTalk Server 管理员使用的帐户。| |
|BizTalk Server Administrators | 具有执行管理任务所需的最少权限。 可以部署解决方案，管理应用程序并解决在消息处理过程中出现的问题。 若要执行关于适配器、接收处理程序、发送处理程序和接收位置的管理任务，则必须将 BizTalk Server Administrators 的成员添加到 Single Sign-On Affiliate Administrators 中。 请参阅[管理 BizTalk Server 安全性](../core/managing-biztalk-server-security.md)。 | 包含配置和管理 BizTalk Server 所需的用户/组。 | **BTS_ADMIN_USERS**以下数据库中的 SQL Server 数据库角色：<br/>BizTalkMgmtDb<br/>BizTalkMsgBoxDb<br/>BizTalkRuleEngineDb<br/>BizTalkDTADb<br/>BAMPrimaryImport<br/><br/>**db_owner**以下数据库的 SQL Server 数据库角色：<br/>BAMStarSchema<br/>BAMPrimaryImport<br/>BAMArchive<br/>BAMAlertsApplication<br/>BAMAlertsNSMain<br/><br/>**NSAdmin**以下数据库中的 SQL Server 数据库角色： <br/>BAMAlertsApplication<br/>BAMAlertsNSMain<br/><br/>以下数据库中的 SQL Server 数据库角色： <br/>BizTalkDTADb<br/>BizTalkMgmtDb。 <br/><br/>**OLAP 管理员**承载 BAMAnalysis OLAP 数据库的计算机上。 |
| BizTalk Server Operators | 具有低权限角色，仅有权监视和故障排除操作。 | 包含监视解决方案的用户/组。 不包含服务帐户。 | **BTS_OPERATORS**以下数据库中的 SQL Server 数据库角色： <br/>BizTalkDTADb<br/>BizTalkEDIDb<br/>BizTalkMgmtDb<br/>BizTalkMsgBoxDb<br/>BizTalkRuleEngineDb | 
| BizTalk Application Users | 由配置管理器创建的首个进程内 BizTalk 主机组的默认名称。 在你的环境中每个进程内主机将使用一个 BizTalk 主机组。 包含能够访问进程内 BizTalk 主机（BizTalk Server 中的主机进程 BTSNTSvc.exe）的帐户。 | 包含在进程内 BizTalk 主机实例和 BizTalk 主机组所属主机中的 BizTalk 规则引擎服务的服务帐户。  | **BTS_HOST_USERS**以下数据库中的 SQL Server 数据库角色：<br/>BizTalkMgmtDb<br/>BizTalkMsgBoxDb<br/>BizTalkRuleEngineDb<br/>BizTalkDTADb<br/>BAMPrimaryImport<br/><br/> **BAM_EVENT_WRITER** BAMPrimaryImport 中的 SQL Server 数据库角色。 | 
| BizTalk Isolated Host Users | 由配置管理器创建的首个独立 BizTalk 主机组的默认名称。 独立 BizTalk 主机指不在 BizTalk Server 上运行的 BizTalk 主机，例如 HTTP 和 SOAP。 在你的环境中每个独立主机将使用一个 BizTalk 独立主机组。 | 包含独立 BizTalk 主机组所属主机中，BizTalk 独立主机实例的服务帐户。 | **BTS_HOST_USERS**以下数据库中的 SQL Server 数据库角色：<br/>BizTalkMgmtDb<br/>BizTalkMsgBoxDb<br/>BizTalkRuleEngineDb<br/>BizTalkDTADb<br/>BAMPrimaryImport | 
| EDI Subsystem Users | 能够访问 EDI 数据库。 | 包含 BizTalk 基本 EDI 服务的服务帐户。 | **EDI_ADMIN_USERS** BizTalkEDIDb 中的 SQL Server 数据库角色。 | 
| BAM Portal Users | 有权访问 BAM 门户网站。 | 默认情况下，此角色使用 Everyone 组。 不包含服务帐户。 |  | 
| BizTalk SharePoint Adapter Enabled Hosts | 能够访问 Windows SharePoint Services 适配器 Web Services。 | 包含要使用 SharePoint 适配器的 BizTalk 主机实例的服务帐户。 |  | 
| BizTalk B2B Operators 组 | 减轻管理员执行所有参与方管理操作 BizTalk 角色。 使用此角色，与该角色关联的 Windows 用户可以执行所有参与方管理操作。 | 包含的用户/组必须能够配置和管理 BizTalk Server TPM 数据以及监视解决方案。 | **BTS_OPERATORS**以下数据库中的 SQL Server 数据库角色： <br/>BizTalkDTADb<br/>BizTalkMgmtDb<br/>BizTalkMsgBoxDb<br/>BizTalkRuleEngineDb<br/>BAMPrimaryImport |

### <a name="user-and-service-accounts"></a>用户帐户和服务帐户
下表列出了 BizTalk Server 所使用的 Windows 用户帐户或服务帐户以及组从属关系。 它还给出了这些帐户的 SQL Server 角色或数据库角色。


|                  用户                  |                                                                                                                   用户说明                                                                                                                   |                  组从属关系                   |                                                                                SQL Server 角色或数据库角色                                                                                |
|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   企业单一登录服务    |                                                                           用于运行企业单一登录服务，该服务会访问 SSO 数据库的服务帐户。                                                                            |                  SSO Administrators                  |                                                                                                                                                                                                  |
|     BizTalk 主机实例帐户      |                                                                                       用于运行 BizTalk 进程内主机实例 (BTNTSVC) 的服务帐户。                                                                                        |              BizTalk Application Users               |                                                                                                                                                                                                  |
| BizTalk 独立主机实例帐户 |                                                                                       用于运行 BizTalk 独立主机实例 (HTTP/SOAP) 的服务帐户。                                                                                        |          BizTalk Isolated Host UsersIIS_WPG          |                                                                                                                                                                                                  |
|       规则引擎更新服务       |                                               用于运行规则引擎更新服务（该服务从规则引擎数据库接收部署/取消部署策略的通知）的服务帐户。                                                |                                                      |                                                              **RE_HOST_USERS** BizTalkRuleEngineDb 中的 SQL Server 数据库角色。                                                              |
|     BAM Notification Services 用户     |                                                                               用于运行 BAM 通知服务，访问 BAM 数据库的服务帐户。                                                                               | SQLServer2005NotificationServicesUser $<ComputerName> | **NSRunService**以下数据库中的 SQL Server 数据库角色：<br/>BAMAlertsApplication<br/>BAMAlertsNSMain<br/><br/>**BAM_ManagementNSReader** BAMPrimaryImport 的 SQL Server 角色。 |
|    BAM 管理 Web Services 用户     | 访问各种 BAM 资源的 BAM 管理 Web Services (BAMManagementService) 的用户帐户。 BAM 门户调用 BAMManagementService（使用登录 BAM 门户的用户凭据）来管理警报、获取 BAM 定义 XML 和 BAM 视图。 |                       IIS_WPG                        | **NSSubscriberAdmin**以下数据库中的 SQL Server 数据库角色：<br/>BAMAlertsApplication<br/>BAMAlertsNSMain<br/><br/>**BAM_ManagementWS** BAMPrimaryImport 的 SQL Server 角色。  |
|      BAM 应用程序池帐户      |                                                                                     BAMAppPool，承载 BAM 门户网站的应用程序池帐户。                                                                                     |                       IIS_WPG                        |                                                                                                                                                                                                  |

> [!IMPORTANT]
> 有关 Windows 组和 BizTalk Server 中使用的服务帐户的详细信息，请参阅[Windows 组和 BizTalk Server 中的用户帐户](../core/windows-groups-and-user-accounts-in-biztalk-server.md)。

## <a name="databases-list"></a>数据库列表
下面是 BizTalk Server 中使用的 SQL Server 数据库的列表：

| 数据存储区名称 | 默认数据库名称 | 数据量 | 增长率 | Description | 
| ---|---|---|---|---|
| SSO 数据库 | SSODB | Low | Low | 此企业单一登录凭据数据库安全地存储了用户名和密码。| 
| BizTalk 管理数据库 | BizTalkMgmtDb | Low | Low | 此数据库是所有 BizTalk Server 实例的中央元信息存储区。| 
| BizTalk MessageBox 数据库 | BizTalkMsgBoxDb | High | Medium | BizTalk Server 引擎将此数据库用于路由、 排队、 实例管理和各种其他任务。<br/><br/>**注意**<br/>自动更新统计信息、 自动创建统计信息和并行度设置都被故意禁用承载 BizTalk Server BizTalkMsgBoxDB 数据库的 SQL Server 数据库实例中。 请勿启用这些设置。 | 
| BizTalk 跟踪数据库 | BizTalkDTADb | High | High | 此数据库存储 BizTalk Server 跟踪引擎所跟踪的业务数据和运行状况监视数据。 | 
| 规则引擎数据库 | BizTalkRuleEngineDb | Low | Low | 此数据库是策略库，策略是相关规则和词汇的集合。 词汇是用于在规则中进行数据引用的、特定于域的、用户友好名称集合。 | 
| BAM 主导入数据库 | BAMPrimaryImport | Medium | Medium | 此数据库收集原始 BAM 跟踪数据。 | 
| BAM 存档数据库 | BAMArchive | Medium | Medium | 此数据库存档旧的业务活动数据。 创建 BAM 存档数据库以最大程度减少 BAM 主导入数据库中的业务活动数据的累计。 | 
| BAM 星型架构数据库 | BAMStarSchema | Medium | Medium | 此数据库包含中间临时表、度量值表和维度表。 | 
| BAM 通知服务应用程序数据库 | BAMAlertsApplication | Medium | Medium | 此数据库包含用于 BAM 通知的警报信息。 例如，在创建警报使用 BAM 门户时，会将条目插入此数据库中指定与警报相关，以及其他支持的数据警报的条件和事件。 | 
| BAM 通知服务实例数据库 | BAMAlertsNSMain | Medium | Medium | 此数据库包含指定 notification services 如何连接到 BAM 正在监视系统的实例信息。 | 

#### <a name="sql-server-databases-used-by-sharepoint"></a>使用 SharePoint 的 SQL Server 数据库

| 数据存储区名称 | 默认数据库名称 | 数据量 | 增长率 | Description | 
|---|---|---|---|---|
| Windows SharePoint Services 配置数据库 | 用户定义 | Low | Low | 此数据库包含服务器的所有全局设置。 | 
| Windows SharePoint Services 内容数据库 | 用户定义 | Medium | Medium | 此数据库包含列表项和文档等所有站点内容。 | 

## <a name="install-biztalk-a-multi-server-environment"></a>安装 BizTalk 多服务器环境

1. **安装 Active Directory 域服务**-到多服务器环境中安装 BizTalk Server 所需的第一步是安装各种 BizTalk Server 组和帐户的 Active Directory 域服务。 若要创建 Active Directory 域，请参阅以下内容：

   - Windows Server 2012 及更高版本：[安装 Active Directory 域服务](https://docs.microsoft.com/windows-server/identity/ad-ds/deploy/install-active-directory-domain-services--level-100-)
   - Windows Server 2008 R2: [AD DS 安装和删除分步指南](https://technet.microsoft.com/library/cc755258(WS.10).aspx)

     > [!IMPORTANT]
     > BizTalk Server 组中所述**用户和服务帐户使用 BizTalk Server 中的**到多服务器环境中安装 BizTalk Server 之前，必须创建表 （在本主题中）。

2. **根据需要安装多个实例的 SQL Server** – 如果您的负载要求指示您需要多个 MessageBox 数据库或需要 BizTalk Server I/O 负载分散到多个 SQL Server 实例，然后安装更多 SQL Server所需的实例。 

    有关测试您的 BizTalk Server 环境和数据库优化性能的详细信息，请参阅[BizTalk Server 性能优化指南](../technical-guides/biztalk-server-2013-performance-optimization-guide.md)。 

3. **根据需要安装多个 BizTalk Server 计算机到在 BizTalk Server 组**– 如果您的负载要求指示您需要多个 BizTalk Server 计算机到 BizTalk Server 组，然后使用 BizTalk Server Enterprise Edition 到多个 BizTalk 服务器上进行横向扩展处理要求。 

    > [!IMPORTANT]
    > BizTalk Server 的许多企业级别的功能（如群集、向组中添加多个服务器以及本机 64 位处理）只能通过企业版本的 BizTalk Server 获得。

4. **安装累积更新**-Windows Update 中列出累积更新。 [KB article 2555976](http://support.microsoft.com/kb/2555976) 列出了可用的 Service Pack 和累积更新。

## <a name="cluster-considerations"></a>群集的注意事项

- **群集 MSDTC** – Microsoft 分布式事务处理协调器 (MSDTC) 是任何 BizTalk Server 环境的中心组件。 如果对 BizTalk Server 环境的其他组件进行了群集处理，建议也对 MSDTC 进行群集处理。 

- **安装 SQL Server 故障转移群集**– 若要为 BizTalk Server 数据库提供高可用性/容错能力建议 SQL Server 故障转移群集上是否安装了 BizTalk Server 数据库。 有关安装 SQL Server 故障转移群集的信息，请参阅： 

  * SQL Server 2016: [Alwayson 故障转移群集实例 (SQL Server)](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server)
  * SQL Server 2014: [Windows Server 故障转移群集 (WSFC) 与 SQL Server](https://msdn.microsoft.com/library/ms189134(v=sql.120).aspx)

    一次 SQL Server 配置为高可用性/容错能力，则 SQL Server 群集的实例，可以引用就像任何其他 SQL Server 实例的 BizTalk Server 配置。

- **将企业单一登录主密钥服务器配置为群集资源**– 企业单一登录主密钥服务器的故障可能会导致 BizTalk Server 环境的系统范围故障。 建议通过将主密钥服务器配置为群集资源来配置企业单一登录主密钥服务器的高可用性/容错能力。 由于主密钥服务器不是 BizTalk Server 环境的资源密集型组件，建议在 SQL Server 实例相同的群集节点上进行群集主密钥服务器。 有关企业单一登录主密钥服务器配置为群集资源的详细信息，请参阅[群集主密钥服务器](../core/how-to-cluster-the-master-secret-server1.md)。 

- **将 BizTalk 主机配置为群集资源**– 运行 BizTalk Server 主机的多个实例提供高可用性/容错能力。 因此，不建议将 BizTalk 主机配置为群集资源，特殊情况除外。 例如，你可以配置 BizTalk 主机作为群集资源时适应高可用性/容错能力，或者对于某些 BizTalk Server 适配器提供按序的送达。 有关何时适合将 BizTalk 主机配置为群集资源的详细信息，请参阅[群集主机内运行适配器处理程序的注意事项](../core/considerations-for-running-adapter-handlers-within-a-clustered-host1.md)。 另请参阅[如何将 BizTalk 主机配置为群集资源](../core/how-to-configure-a-biztalk-host-as-a-cluster-resource1.md)。 

- **群集消息队列**– 请参阅[安装和群集 MSMQ](https://blogs.msdn.microsoft.com/biztalknotes/2013/03/20/how-to-install-and-cluster-msmq-on-windows-server-2012/)。

- **群集文件系统**– 请参阅[如何群集文件系统](http://go.microsoft.com/fwlink/p/?LinkId=189517)。

## <a name="use-scom"></a>使用 SCOM
BizTalk Server 管理包为 Operations Manager 提供了全面发现和监视 BizTalk Server 组件和在多台计算机中运行的应用程序。 有关 BizTalk Server 管理包的详细信息，请参阅 http://www.microsoft.com/download/details.aspx?id=39617 。

## <a name="next"></a>Next  
[配置 BizTalk](configure-biztalk-server.md)
