---
title: "备份数据库 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0524a8f0-15a3-4731-a7bd-c0c935fff6c8
caps.latest.revision: "2"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: d6a4b40be0a9a7d4846dd965a4d9f934e69690e7
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="backing-up-databases"></a><span data-ttu-id="ced1a-102">备份数据库</span><span class="sxs-lookup"><span data-stu-id="ced1a-102">Backing Up Databases</span></span>
<span data-ttu-id="ced1a-103">因为[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]使用分布式事务跨多个数据库，备份 BizTalk Server 作业创建的所有同步的备份[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]数据库。</span><span class="sxs-lookup"><span data-stu-id="ced1a-103">Because[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] uses distributed transactions across multiple databases, the Backup BizTalk Server job creates synchronized backups of all [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] databases.</span></span> <span data-ttu-id="ced1a-104">这可以通过使用"完整"数据库恢复模式的事务进行标记。</span><span class="sxs-lookup"><span data-stu-id="ced1a-104">This is accomplished by using marked transactions with the “Full” database recovery model.</span></span> <span data-ttu-id="ced1a-105">这是必需的可以跨数据库事务上一致的备份。</span><span class="sxs-lookup"><span data-stu-id="ced1a-105">This is required for the backups to be transactionally consistent across databases.</span></span> <span data-ttu-id="ced1a-106">有关详细信息，请参阅["标记的事务，完整备份和日志备份"](http://go.microsoft.com/fwlink/?LinkId=151565) (http://go.microsoft.com/fwlink/?LinkId=151565) BizTalk Server 文档中。</span><span class="sxs-lookup"><span data-stu-id="ced1a-106">For more information, see ["Marked Transactions, Full Backups, and Log Backups"](http://go.microsoft.com/fwlink/?LinkId=151565) (http://go.microsoft.com/fwlink/?LinkId=151565) in the BizTalk Server documentation.</span></span>  
  
## <a name="advantages-of-the-backup-biztalk-server-job"></a><span data-ttu-id="ced1a-107">备份 BizTalk Server 作业的优点</span><span class="sxs-lookup"><span data-stu-id="ced1a-107">Advantages of the Backup BizTalk Server Job</span></span>  
 <span data-ttu-id="ced1a-108">备份 BizTalk Server 作业是唯一受支持的备份方法[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]数据库。</span><span class="sxs-lookup"><span data-stu-id="ced1a-108">The Backup BizTalk Server job is the only supported method for backing up the [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] databases.</span></span> <span data-ttu-id="ced1a-109">利用[!INCLUDE[btsSQLServerNoVersion](../includes/btssqlservernoversion-md.md)]作业，以备份[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]不支持在生产环境中的数据库。</span><span class="sxs-lookup"><span data-stu-id="ced1a-109">Use of [!INCLUDE[btsSQLServerNoVersion](../includes/btssqlservernoversion-md.md)] jobs to back up the [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] databases in a production environment is not supported.</span></span>  
  
 <span data-ttu-id="ced1a-110">如果备份[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]不运行作业时，[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]数据库事务日志将会增长不受限制。</span><span class="sxs-lookup"><span data-stu-id="ced1a-110">If the Backup [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] job is not run, the [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] database transaction logs will grow unbounded.</span></span> <span data-ttu-id="ced1a-111">备份作业将截断事务日志，这使它们保持无限增长。</span><span class="sxs-lookup"><span data-stu-id="ced1a-111">The backup job truncates the transaction logs, which keep them from growing unbounded.</span></span> <span data-ttu-id="ced1a-112">如果[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]数据库事务日志不断增长，它们无法在某一时刻填它们驻留在该磁盘。</span><span class="sxs-lookup"><span data-stu-id="ced1a-112">If the [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] database transaction logs continue to grow, they could at some point fill the disk they are housed on.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="ced1a-113">使用这两个备份[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]作业和日志传送是当前唯一完全记录和支持方法执行[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]数据库备份和还原。</span><span class="sxs-lookup"><span data-stu-id="ced1a-113">Using both the Backup [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] job and log shipping is currently the only fully documented and supported method for performing [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] database backup and restore.</span></span>  
  
## <a name="guidelines-for-the-backup-biztalk-server-job"></a><span data-ttu-id="ced1a-114">备份 BizTalk 服务器作业的准则</span><span class="sxs-lookup"><span data-stu-id="ced1a-114">Guidelines for the Backup BizTalk Server Job</span></span>  
 <span data-ttu-id="ced1a-115">你应还原整个[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]定期的环境。</span><span class="sxs-lookup"><span data-stu-id="ced1a-115">You should restore the entire [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] environment on a regular basis.</span></span> <span data-ttu-id="ced1a-116">这包括不仅的 SQL server 和[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]数据库，但还运行的计算机[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]。</span><span class="sxs-lookup"><span data-stu-id="ced1a-116">This includes not only the SQL server(s) and the [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] databases, but also the computers running [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)].</span></span> <span data-ttu-id="ced1a-117">你应记录并实际发生故障之前执行这些过程。</span><span class="sxs-lookup"><span data-stu-id="ced1a-117">You should document and practice these procedures before a failure actually occurs.</span></span>  
  
> [!NOTE]  
>  <span data-ttu-id="ced1a-118">备份[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]作业不会删除旧的备份文件。</span><span class="sxs-lookup"><span data-stu-id="ced1a-118">The Backup [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] job does not delete old backup files.</span></span> <span data-ttu-id="ced1a-119">必须定义并将进程来存档旧的备份文件，并将它们从备份作业使用的备份目录移动。</span><span class="sxs-lookup"><span data-stu-id="ced1a-119">You must define and put processes in place to archive the old backup files and move them from the backup directory that the backup job uses.</span></span>  
  
## <a name="additional-resources"></a><span data-ttu-id="ced1a-120">其他资源</span><span class="sxs-lookup"><span data-stu-id="ced1a-120">Additional Resources</span></span>  
 <span data-ttu-id="ced1a-121">请参阅中的以下主题[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]文档：</span><span class="sxs-lookup"><span data-stu-id="ced1a-121">See the following topics in the [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] documentation:</span></span>  
  
-   <span data-ttu-id="ced1a-122">有关特定详细信息[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]备份和还原任务，请参阅["清单:: 备份和还原"](http://go.microsoft.com/fwlink/?LinkId=154070) (http://go.microsoft.com/fwlink/?LinkId=154070)。</span><span class="sxs-lookup"><span data-stu-id="ced1a-122">For more information about specific [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] backup and restore tasks, see ["Checklist: Backup and Restore"](http://go.microsoft.com/fwlink/?LinkId=154070) (http://go.microsoft.com/fwlink/?LinkId=154070).</span></span>  
  
-   <span data-ttu-id="ced1a-123">有关备份和还原的概述[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]，请参阅["Backing Up 和还原 BizTalk Server"](http://go.microsoft.com/fwlink/?LinkId=154071) (http://go.microsoft.com/fwlink/?LinkId=154071)。</span><span class="sxs-lookup"><span data-stu-id="ced1a-123">For an overview of Backing up and restoring [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)], see ["Backing Up and Restoring BizTalk Server"](http://go.microsoft.com/fwlink/?LinkId=154071) (http://go.microsoft.com/fwlink/?LinkId=154071).</span></span>  
  
-   <span data-ttu-id="ced1a-124">有关配置 BizTalk Server 中备份作业的详细信息，请参阅["如何为配置备份 BizTalk Server 作业"](http://go.microsoft.com/fwlink/?LinkId=154072) (http://go.microsoft.com/fwlink/?LinkId=154072)。</span><span class="sxs-lookup"><span data-stu-id="ced1a-124">For more information about configuring the Backup BizTalk Server job, see ["How to Configure the Backup BizTalk Server Job"](http://go.microsoft.com/fwlink/?LinkId=154072) (http://go.microsoft.com/fwlink/?LinkId=154072).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="ced1a-125">另请参阅</span><span class="sxs-lookup"><span data-stu-id="ced1a-125">See Also</span></span>  
 [<span data-ttu-id="ced1a-126">使用 BizTalk Server 日志传送以实现灾难恢复</span><span class="sxs-lookup"><span data-stu-id="ced1a-126">Using BizTalk Server Log Shipping for Disaster Recovery</span></span>](../technical-guides/using-biztalk-server-log-shipping-for-disaster-recovery.md)