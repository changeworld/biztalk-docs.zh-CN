---
title: 如何从一个组中删除服务器 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- groups, servers
- managing [groups], deleting servers
- servers, deleting
- deleting, groups
- servers
- managing [servers], deleting from groups
- groups, deleting
- servers, groups
- deleting, servers
ms.assetid: 85596e18-fa17-4f44-bc20-2e4cb578e109
caps.latest.revision: 22
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 19c4381f7ca011698aa647f0d7a4a7ccf9ca91a4
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37017624"
---
# <a name="how-to-remove-a-server-from-a-group"></a>如何从一个组中删除服务器
一台服务器只能与一个 BizTalk 组相关联。 如果某个服务器已属于其他组，则必须首先从其当前组中删除该服务器，然后才可以将该服务器添加到新的组。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程，则必须以 Windows Administrators 组成员的身份登录。  
  
### <a name="to-remove-a-server-from-a-group"></a>从组中删除服务器  
  
1. 在你想要从 BizTalk Server 组中删除的计算机，单击**启动**，单击**所有程序**，单击[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]，然后单击**BizTalk Server 配置**.  
  
2. 在菜单栏上，单击**取消对功能**。  
  
3. 在中**取消对功能**对话框中，选择**组**，然后单击**确定**。  
  
   > [!CAUTION]
   >  取消组配置还将取消配置该计算机上已配置的所有依存功能。  
  
4. 单击 **“是”**。  
  
5. 在 Microsoft BizTalk Server 配置向导中，单击**下一步**。  
  
    该组及其依赖功能的配置都将被取消。  
  
6. 单击 **“完成”**。  
  
## <a name="see-also"></a>请参阅  
 [管理组](../core/managing-groups.md)   
 [BizTalk 组](../core/biztalk-groups.md)   
 [如何将服务器添加到组](../core/how-to-add-a-server-to-a-group.md)   
 [如何将服务器从一个组移到另一个](../core/how-to-move-a-server-from-one-group-to-another.md)   
 [如何修改组属性](../core/how-to-modify-group-properties.md)   
 [管理服务器](../core/managing-servers.md)