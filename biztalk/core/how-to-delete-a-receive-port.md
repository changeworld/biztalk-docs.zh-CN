---
title: 如何删除接收端口 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- managing [receive ports], deleting
- deleting, receive ports
- receive ports, deleting
ms.assetid: 69cd86f7-e3cc-4a50-8d15-5f978c94a6be
caps.latest.revision: 14
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 65f72ad5bfef99bca7474ea01f3d07ecbe9ef2b8
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36975150"
---
# <a name="how-to-delete-a-receive-port"></a>如何删除接收端口
本主题介绍如何使用 BizTalk Server 管理控制台从 BizTalk 应用程序中删除接收端口。 进行此操作时，还将删除该组的 BizTalk 管理数据库中的接收端口，与此同时此接收端口的所有接收位置也被删除。  
  
 为了使此操作成功，不能将接收端口绑定到业务流程。 有关删除接收端口的绑定的说明，请参阅[如何取消绑定业务流程](../core/how-to-unbind-an-orchestration.md)。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行本主题中的过程，必须是 BizTalk Server Administrators 组的成员的帐户登录。 有关详细的权限的信息，请参阅[用于部署和管理 BizTalk 应用程序所需权限](../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)。  
  
### <a name="to-delete-a-receive-port"></a>删除接收端口  
  
1. 单击**启动**，单击**所有程序**，单击[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]，然后单击**BizTalk Server 管理**。  
  
2. 在控制台树中，展开[!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]，展开 BizTalk 组，展开**应用程序**，然后展开包含你想要删除的接收端口的应用程序。  
  
3. 单击**接收端口**，右键单击接收端口，然后单击**删除**。  
  
## <a name="see-also"></a>请参阅  
 [管理接收端口](../core/managing-receive-ports.md)