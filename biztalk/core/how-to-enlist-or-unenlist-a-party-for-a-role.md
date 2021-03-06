---
title: 如何登记或取消登记角色参与方 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- managing [role links], enlisting
- enlisting, role links
- role links, unenlisting
- role links, enlisting
- managing [role links], unenlisting
ms.assetid: 06fc2a64-3add-400c-9f9d-fab22fdf5366
caps.latest.revision: 14
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 046e51424427973534d9e4defdbf6e8d58eb8b2f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36966246"
---
# <a name="how-to-enlist-or-unenlist-a-party-for-a-role"></a>如何登记或取消登记角色参与方
本主题将介绍如何使用 BizTalk Server 管理控制台来登记或取消登记角色参与方。 登记角色参与方将为参与方指定角色，而取消登记角色参与方将从角色中删除该参与方。  
  
 登记或取消登记角色参与方时，请切记以下几点：  
  
-   登记角色参与方前，必须先创建要登记的参与方。 有关说明，请参阅[如何创建参与方](http://msdn.microsoft.com/library/f6feca1d-bc83-4fb6-981d-26c9e0d53044)。  
  
-   可在不重启应用程序的情况下，登记或取消登记角色参与方。  
  
> [!NOTE]
>  应用程序开发人员可以登记或取消参与方登记在开发过程中，通过使用本主题中的过程。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行本主题中的过程，必须是 BizTalk Server Administrators 组的成员的帐户登录。 有关详细的权限的信息，请参阅[用于部署和管理 BizTalk 应用程序所需权限](../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)。  
  
### <a name="to-enlist-or-unenlist-a-party-for-a-role"></a>登记或取消登记角色参与方  
  
1. 单击**启动**，单击**所有程序**，单击[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]，然后单击**BizTalk Server 管理**。  
  
2. 在控制台树中，展开**BizTalk Server 管理**，展开 BizTalk 组，展开**应用程序**，然后展开包含要登记的角色链接的应用程序或取消登记参与方。  
  
3. 单击**角色链接**，右键单击你想要登记或取消登记参与方，然后单击该角色链接**属性**。  
  
4. 若要登记参与方，请执行以下操作：  
  
   -   单击**登记**单击要登记的参与方。  
  
   -   单击**绑定**，在**发送端口**下拉列表中，单击发送端口要用于此参与方，然后单击**确定**两次。  
  
5. 若要取消登记参与方，单击的参与方，单击**取消登记**，然后单击**确定**。  
  
## <a name="see-also"></a>请参阅  
 [管理角色链接](../core/managing-role-links.md)