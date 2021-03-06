---
title: 如何从应用程序删除预处理或后处理脚本 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- managing [scripts], deleting
- deleting, scripts
- managing [applications], scripts
- scripts, deleting
- applications, scripts
ms.assetid: 7911f098-97f2-4a5d-87fe-20b55231113e
caps.latest.revision: 14
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 3c9742b6c523f193a8670c1171f38949ef5dd1cc
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37010006"
---
# <a name="how-to-remove-a-pre--or-post-processing-script-from-an-application"></a>如何从应用程序中删除预处理脚本和后处理脚本
本主题描述如何使用 BizTalk Server 管理控制台或命令行从应用程序删除预处理脚本或后处理脚本。 这将从 BizTalk 管理数据库删除脚本，以便它将不会导出到应用程序的 .msi 文件中。 如果本地文件系统中存在脚本，该方法并不会从那里删除该脚本。  
  
 如果包含该脚本的应用程序已安装在本地文件系统上，并且该脚本设计为在卸载期间运行，则必须从文件系统中删除该脚本，以便避免该脚本在卸载应用程序时运行。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行本主题中的过程，必须是 BizTalk Server Administrators 组的成员的帐户登录。 有关详细的权限的信息，请参阅[用于部署和管理 BizTalk 应用程序所需权限](../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)。  
  
## <a name="to-remove-a-script-from-an-application"></a>从应用程序中删除脚本  
  
#### <a name="using-the-biztalk-server-administration-console"></a>使用 BizTalk Server 管理控制台  
  
1. 单击**启动**，单击**所有程序**，单击[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]，然后单击**BizTalk Server 管理**。  
  
2. 在控制台树中，展开 [!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]，然后展开包含要删除的脚本的 BizTalk 组，接着展开包含该脚本的应用程序。  
  
3. 单击**资源**文件夹中，右键单击脚本，然后依次**删除**。  
  
#### <a name="using-the-command-line"></a>使用命令行  
  
1. 按如下所示打开命令提示符： 单击**启动**，单击**运行**，类型`cmd`，然后单击**确定**。  
  
2. 键入以下命令，替换适当的值下, 表中所述：  
  
    **BTSTask RemoveResource** [**/ApplicationName:**<em>值</em>] **/Luid:**<em>值</em>[**/Server:** <em>值</em>] [**/database:**<em>值</em>]  
  
    例如：  
  
    **BTSTask RemoveResource /ApplicationName:MyApplication /Luid:"MyApplication:MyScript.vbs"**  
  
   |参数|Description|  
   |---------------|-----------------|  
   |**/ 应用程序名称**|包含要删除的 BizTalk 脚本的 BizTalk 应用程序的名称。 如果名称中包含空格，则必须将其括在双引号 (") 中。 如果未指定此参数，则使用默认的应用程序。|  
   |**/ Luid**|脚本的本地唯一标识符 (LUID)。 可通过获得 LUID [ListApp 命令](../core/listapp-command.md)。|  
   |**/ 服务器**|BizTalk 管理数据库的宿主 SQL Server 实例的名称，格式为“服务器名称\实例名称,端口”。<br /><br /> 只在实例名称与服务器名称不相同时才需要指定实例名称。 只在 SQL Server 不使用默认端口号 (1433) 时才需要指定端口。<br /><br /> 示例：<br /><br /> Server=MyServer<br /><br /> Server=MyServer\MySQLServer,1533<br /><br /> 如果未提供，则使用本地计算机上运行的 SQL Server 实例的名称。|  
   |**/ 数据库**|BizTalk 管理数据库的名称。 如果未指定，则使用在本地 SQL Server 实例中运行的 BizTalk 管理数据库。|  
  
## <a name="see-also"></a>请参阅  
 [管理预处理和后处理脚本](../core/managing-pre-and-post-processing-scripts.md)   
 [RemoveResource 命令](../core/removeresource-command.md)