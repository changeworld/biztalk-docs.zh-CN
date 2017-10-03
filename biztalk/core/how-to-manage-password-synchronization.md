---
title: "如何管理密码同步 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Password Synchronization [SSO], managing
- managing [SSO], disabling features
- managing [SSO], enabling features
- Password Synchronization [SSO], SSOMANAGE command line utility
- SSO database, SSOMANAGE command line utility
- managing, Password Synchronization [SSO]
- SSO database, database settings
- SSOMANAGE command line utility
ms.assetid: 033e63f2-e5b0-4400-99c3-145679d9b84e
caps.latest.revision: "7"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 2939fd0594c878e3a5f1416d0b1e871b78ba3858
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-manage-password-synchronization"></a>如何管理密码同步
使用 MMC 管理单元或 SSOMANAGE 命令行实用工具可以启用或禁用 SSO 功能，并显示当前 SSO 数据库设置。  
  
### <a name="to-manage-features-or-display-settings-using-the-mmc-snap-in"></a>使用 MMC 管理单元管理功能或显示设置  
  
1.  右键单击相应的功能或数据库。  
  
2.  单击相应的菜单项。  
  
### <a name="to-enable-sso-features-using-the-command-line"></a>使用命令行启用 SSO 功能  
  
1.  在 **“开始”** 菜单上，单击 **“运行”**。  
  
2.  在**运行**对话框中，键入**cmd**，然后单击**确定**。  
  
3.  在命令行上，转至企业单一登录安装目录。 默认值是\<驱动器 >: \program Files\Enterprise 单一登录。  
  
4.  类型**ssomanage-启用**，然后按 enter 键。  
  
### <a name="to-disable-sso-features-using-the-command-line"></a>使用命令行禁用 SSO 功能  
  
1.  在 **“开始”** 菜单上，单击 **“运行”**。  
  
2.  在**运行**对话框中，键入**cmd**，然后单击**确定**。  
  
3.  在命令行上，转至企业单一登录安装目录。 默认值是\<驱动器 >: \program Files\Enterprise 单一登录。  
  
4.  类型**ssomanage-禁用**，然后按 enter 键。  
  
### <a name="to-display-current-database-settings-using-the-command-line"></a>使用命令行显示当前数据库设置  
  
1.  在 **“开始”** 菜单上，单击 **“运行”**。  
  
2.  在**运行**对话框中，键入**cmd**，然后单击**确定**。  
  
3.  在命令行上，转至企业单一登录安装目录。 默认值是\<驱动器 >: \program Files\Enterprise 单一登录。  
  
4.  类型**ssomanage displaydb** ，然后按 enter 键。  
  
## <a name="see-also"></a>另请参阅  
 [密码同步](../core/password-synchronization2.md)