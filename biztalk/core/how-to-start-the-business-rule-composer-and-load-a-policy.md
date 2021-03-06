---
title: 如何启动业务规则编辑器并加载策略 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- policies, loading
- opening, Busines Rule Composer
- Business Rule Composer, policies
- Business Rule Composer, opening
ms.assetid: 34a6034d-90b3-4ce0-9770-3790763affe3
caps.latest.revision: 15
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e56d3d2c1dde771d86f8de345d6e3b249ab394b8
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36977046"
---
# <a name="how-to-start-the-business-rule-composer-and-load-a-policy"></a>如何启动业务规则编辑器并加载策略
本部分将介绍如何启动业务规则编辑器和加载策略。  
  
### <a name="to-start-the-business-rule-composer"></a>启动业务规则编辑器  
  
- 上**启动**菜单，依次指向**所有程序**，指向 Microsoft [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]，然后单击**业务规则编辑器**。  
  
  > [!NOTE]
  >  在支持用户帐户控制 (UAC) 的系统上，可能需要具有管理权限才能运行该工具。 要执行此操作，右键单击该应用程序，并选择**以管理员身份运行**。  
  
### <a name="to-load-a-policy"></a>加载策略  
  
1.  在业务规则编辑器上**规则存储**菜单上，单击**负载**。  
  
2.  在中**规则存储**对话框中**SQL Server**下拉列表中，选择你想要连接的 SQL Server™ 计算机。  
  
3.  在中**数据库**下拉列表中，选择包含想要打开规则存储的数据库。  
  
> [!NOTE]
>  安装的规则存储的默认数据库[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]是**BizTalkRuleEngineDb**。  
> 
> [!NOTE]
>  如果你使用新创建的 SQL Server 帐户具有**强制密码过期**并**用户必须更改在下次登录密码**选项集，业务规则编辑器将无法连接到规则引擎数据库。