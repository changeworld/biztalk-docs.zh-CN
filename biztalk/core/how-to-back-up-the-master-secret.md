---
title: 如何备份主密钥 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- managing [Master Secret server], backing up
- backing up, Master Secret server
- Master Secret server, backing up
ms.assetid: 22c23f66-b7df-4379-8a9f-065406ba8aa8
caps.latest.revision: 14
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: ec9faad19d695d43476e60e87acbd067d7e66896
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37008150"
---
# <a name="how-to-back-up-the-master-secret"></a>如何备份主密钥
您可以将主密钥服务器中的主密钥备份到 NTFS 文件系统或可移动媒体（如软盘）上。  
  
 只有单一登录管理员和 Windows 管理员才能执行此任务。 SSO 系统将提示您输入密码。 以后若要还原该密钥，则必须提供同一密码。  
  
> [!CAUTION]
>  如果主密钥服务器出现故障而且密钥丢失，或者密钥损坏，则将无法检索存储在 SSO 数据库中的数据。 因此必须备份主密钥，否则将面临丢失 SSO 数据库中数据的风险。  
  
### <a name="to-back-up-the-master-secret-using-the-mmc-snap-in"></a>使用 MMC 管理单元备份主密钥  
  
1.  在“开始”  菜单上，依次单击“所有程序” 、“Microsoft Enterprise Single Sign-On” 和“SSO 管理” 。  
  
2.  在 ENTSSO MMC 管理单元的作用域窗格中，展开“企业单一登录”  节点。  
  
3.  右键单击**系统**，然后单击**备份密钥**。  
  
### <a name="to-back-up-the-master-secret-using-the-command-line"></a>使用命令行备份主密钥  
  
1. 上**启动**菜单上，单击**所有程序**，然后单击**附件**。 右键单击**命令提示符**，然后单击**运行方式...**.  
  
2. 选择合适的管理员，然后单击**确定**。  
  
3. 在命令行上，转至企业单一登录安装目录。 默认安装目录*\<驱动器\>*: \Program Files\Common Files\Enterprise Single Sign-on。  
  
4. 类型 * * ssoconfig-backupSecret *\<备份文件\>**<em>，其中 *\<备份文件\></em>是路径和要备份主密钥的文件的名称。 例如，A:\ssobackup.bak。  
  
   > [!NOTE]
   >  在支持用户帐户控制 (UAC) 的系统上，可能需要具有管理权限才能运行该工具。  
  
5. 提供密码以保护此文件。 然后，将提示您确认该密码并提供密码提示以帮助您记起此密码。  
  
> [!IMPORTANT]
>  您必须将该备份文件保存到安全的位置。  
  
## <a name="see-also"></a>请参阅  
 [如何生成主密钥](../core/how-to-generate-the-master-secret.md)   
 [如何还原主密钥](../core/how-to-restore-the-master-secret.md)   
 [主密钥服务器](../core/master-secret-server.md)   
 [管理主密钥](../core/managing-the-master-secret.md)