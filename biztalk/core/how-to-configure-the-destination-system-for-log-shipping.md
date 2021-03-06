---
title: 如何配置日志传送目标系统 |Microsoft Docs
ms.custom: ''
ms.date: 2015-12-03
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- backing up, log shipping
- system failures, preventing
- log shipping
- databases, backing up
- backing up, databases
- system failures, backing up
- backing up, system failures
ms.assetid: 7b4425f5-b105-4fb2-a503-94ca1e75ad55
caps.latest.revision: 54
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9ee5c7a5d59ce60923fa4ad3ba015f60bc30a0c8
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36971462"
---
# <a name="how-to-configure-the-destination-system-for-log-shipping"></a>如何配置日志传送的目标系统
日志传送具有备用服务器功能，用以缩短出现系统故障时的停机时间。 使用日志传送可以自动从源系统向目标系统发送事务日志。 在目标系统中，事务日志还原到[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]数据库; 它们与源数据库紧密同步。  
  
 日志传送既可以在单服务器环境下工作，也可以在分布式服务器环境下工作。 包含实时数据的服务器或服务器组称作源系统（或主系统）。 用来还原由源系统（或主系统）生成的数据库备份的服务器或服务器组称作目标系统（或辅助系统）。  
  
 [有关日志传送](https://docs.microsoft.com/sql/database-engine/log-shipping/about-log-shipping-sql-server)中的 SQL 文档提供了特定的详细信息。  
  
 你可以运用以下步骤为单个源系统创建由一个服务器组成的目标系统。 如果目标系统包含多个服务器，则在每个目标服务器上重复执行以下步骤即可。  
  
> [!IMPORTANT]
>  请总是在某个安全位置保留备份文件的一个副本。 即使你进行了日志备份，在没有备份文件的情况下也无法还原数据库。  
  
## <a name="prerequisites"></a>必要條件  
* 以的成员身份登录[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]Administrators 组。  
  
* 在源和目标系统上使用相同版本的 SQL Server。 SQL Server 必须安装在源和目标系统上的同一相对位置。  
  
* 源系统上的 SQL 事务日志（.LDF 文件）目录在目标系统上也必须存在。 如果该目录在目标系统上不存在，请使用与源系统上的目录相同的名称和权限创建该目录。  
  
### <a name="configure-the-destination-system-for-log-shipping"></a>配置日志传送的目标系统  
  
1. 在目标系统上，打开**SQL Server Management Studio**，并连接到 SQL Server。 选择**主**从可用数据库。  
  
2. 上**文件**菜单中，**打开**以下 SQL 脚本：  
  
   ```    
   %SystemDrive%\Program Files\Microsoft BizTalk Server <version>\Schema\LogShipping_Destination_Schema.sql  
   ```  
  
3. 上**查询**菜单中，选择**Execute**。  
  
    *Logshipping_destination_schema 将*删除并重新创建用于还原目标系统上的源数据库的表。 这些表存储了以下信息：要恢复的数据库的列表、从源系统的 BizTalkMgmtDb 数据库导入的备份历史记录的副本、有关 SQL Server 代理作业（配置为针对源数据库运行）的信息。  
  
4. 上**文件**菜单中，**打开**以下 SQL 脚本：  
  
   ```    
   %SystemDrive%\Program Files\Microsoft BizTalk Server <version>\Schema\LogShipping_Destination_Logic.sql  
   ```  
  
5. 上**查询**菜单中，选择**Execute**。  
  
6. 在计算机或计算机已标识为目标系统中，打开**SQL Server Management Studio**并连接到 SQL Server。  
  
7. 选择**新查询**。 在查询窗口中粘贴以下命令：  
  
   ```  
   exec bts_ConfigureBizTalkLogShipping @nvcDescription = '<MyLogShippingSolution>',  
   @nvcMgmtDatabaseName = '<BizTalkServerManagementDatabaseName>',  
   @nvcMgmtServerName = '<BizTalkServerManagementDatabaseServer>',  
   @SourceServerName = null, -- null indicates that this destination server restores all databases  
   @fLinkServers = 1 -- 1 automatically links the server to the management database  
   ```  
  
    然后：  
  
   1.  在目标系统上启用 **[Ad Hoc Distributed Queries](https://docs.microsoft.com/sql/database-engine/configure-windows/server-configuration-options-sql-server)**。  
  
   2.  在查询窗口中，替换*\<MyLogShippingSolution\>* 的有意义的说明，用单引号引起。  
  
   3.  在查询窗口中，替换*\<BizTalkServerManagementDatabaseName\>* 并*\<BizTalkServerManagementDatabaseServer\>* 与名称和源 BizTalk 管理数据库，用单引号引起的位置。  
  
   > [!NOTE]
   >  如果有多个源服务器，则可将每个源服务器还原到它自己的目标服务器。 每个目标服务器上，在 **@SourceServerName = null**参数，替换*null*具有适当的源服务器的名称，用单引号引起 (例如，  **@SourceServerName = 'MySourceServer'**)。  
  
8. 上**查询**菜单中，选择**Execute**。  
  
   > [!IMPORTANT]
   >  如果查询失败，则解决该问题与查询后，您必须重新开始此过程来重新配置目标系统的步骤 1 中。  
  
   > [!NOTE]
   >  目标系统上的还原作业将尝试重新创建每个还原的数据库的日志和数据文件，这些文件的创建位置与它们在源数据库服务器上的位置相同。  
  
9. 在目标系统上**SQL Server Management Studio**，展开**SQL Server 代理**，然后展开**作业**。  
  
     在“详细信息”窗格中，有三个新作业：  
  
   - **BTS 日志传送获取备份历史记录**  
  
      此 BizTalk 作业将备份历史记录从源移到目标。 默认情况下，安排该作业每分钟运行一次。 应尽可能频繁地运行此作业，以便将备份历史记录从源系统移到目标系统。 如果源系统出现故障，则已标识为目标系统的服务器会继续处理已导入的历史记录。  
  
   - **BTS 服务器日志传送还原数据库**  
  
      此 BizTalk 作业可将源服务器中给定数据库的备份文件还原到目标服务器。 默认情况下，安排该作业每分钟运行一次。 只要存在要还原的备份文件，则该作业将一直运行下去，而不会完成。 为了安全起见，你可多运行该作业一次，以确保已经没有要还原的备份文件。  
  
   - **BTS 日志传送还原到标记**  
  
      此 BizTalk 作业可将所有数据库还原到上次日志备份中的一个标记。 这可确保所有数据库在事务性上处于一致状态。 此外，该作业还将在目标系统上重新创建源系统上的所有 SQL Server 代理作业。  
  
     > [!IMPORTANT]
     >  应监视这些作业，以确保它们不会失败。  
  
10. 在 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 上，转到以下文件夹：  
  
     32 位计算机： %SystemDrive%\Program Files\Microsoft BizTalk Server\<版本\>\Schema\Restore  
  
     64 位计算机： %SystemDrive%\Program 文件 (x86) \Microsoft BizTalk Server\<版本\>\Bins32\Schema\Restore  
  
11. 右键单击**SampleUpdateInfo.xml**，然后选择**编辑**。 请执行以下操作：  
  
    -   所有实例替换都为**SourceServer**与源系统的名称。  
  
    -   所有实例替换都为**DestinationServer**与目标系统的名称。  
  
    > [!IMPORTANT]
    >  用引号将源系统和目标系统的名称括起来。  
    > 
    > [!NOTE]
    >  如果对任何 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 数据库进行了重命名，则还必须更新 XML 文件中的数据库名称。  
    > 
    > [!NOTE]
    >  如果已配置 BAM，则必须添加以下行中的**OtherDatabases**一部分**SampleUpdateInfo.xml** BAMAlertsApplication 和 BAMAlertsNSMain 数据库的文件：   
    > `<Database Name="BAM Alerts Application DB" oldDBName="BAMAlertsApplication" oldDBServer="SourceServer" newDBName=" BAMAlertsApplication" newDBServer="DestinationServer"/>`  
    > `<Database Name="BAM Alerts Instance DB" oldDBName="BAMAlertsNSMain" oldDBServer="SourceServer" newDBName="BAMAlertsNSMain" newDBServer="DestinationServer"/>`  
    > 
    >  如果更改了这两个数据库的默认名称，请使用实际的数据库名称。  
  
12. 如果您有多个 MessageBox 数据库您[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]系统中，到列表中，添加其他 MessageBoxDB 行，然后设置**IsMaster ="0"** 为非主数据库。  
  
13. 如果使用 BAM 或规则引擎，请相应地取消这些行的注释。  
  
14. 如果有任何自定义数据库，将其下添加**\<OtherDatabases\>** 部分。 请参阅[如何备份自定义数据库](../core/how-to-back-up-custom-databases.md)。  
  
15. 在完成编辑文件，请保存该文件，并退出。  
  
## <a name="next-steps"></a>后续步骤  
 [如何还原数据库](../core/how-to-restore-your-databases.md)  
  
## <a name="see-also"></a>请参阅  
 [如何配置备份 BizTalk Server 作业](../core/how-to-configure-the-backup-biztalk-server-job.md)   
 [如何安排备份 BizTalk Server 作业](../core/how-to-schedule-the-backup-biztalk-server-job.md)   
 [如何备份自定义数据库](../core/how-to-back-up-custom-databases.md)