---
title: "清单： 监视与 Operations Manager 2007 的 BizTalk Server |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2e1f7f57-1501-473f-af5f-15f3e1ddaf8e
caps.latest.revision: "2"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 810ede830f7142181c4bec1f727cbc496049ce03
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="checklist-monitoring-biztalk-server-with-operations-manager-2007"></a>清单： 监视与 Operations Manager 2007 的 BizTalk Server
本主题列出了你可以按照时准备监视的高级步骤你[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]环境。  
  
|步骤|参考|  
|----------|---------------|  
|确保你具有适当的权限来安装和配置软件上你[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]计算机。|[最低安全用户权限](http://go.microsoft.com/fwlink/?LinkID=154374)(http://go.microsoft.com/fwlink/?LinkID=154374)|  
|在每上安装 Operations Manager 2007 代理[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]你想要监视并使其指向 Operations Manager 2007 服务器的计算机。|请参阅[部署 Operations Manager 2007](http://go.microsoft.com/fwlink/?LinkId=110030) (http://go.microsoft.com/fwlink/?LinkId=110030)|  
|下载并导入以下管理包的适当版本：<br /><br /> -   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]（必需）<br />-企业单一登录 （必需）<br />Windows 基本操作系统 （服务器） （可选）<br />Microsoft Windows Server 群集 （如果群集使用，可选）<br />SQL Server 2008 中，SQL Server 2005 （可选）<br />-Internet 信息服务 (IIS) 2008，IIS 2003 （可选）<br />消息队列 (MSMQ) 3.0 （可选）|-下载中的管理包[System Center 管理包目录](http://go.microsoft.com/fwlink/?LinkId=203227)(http://go.microsoft.com/fwlink/?LinkId=203227)。<br />-导入管理包在按照说明[如何导入 Operations Manager 2007 中的管理包](http://go.microsoft.com/fwlink/?LinkID=98348)(http://go.microsoft.com/fwlink/?LinkID=98348)。|  
|阅读有关使用 Operations Manager 2010 来监视最佳实践[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]。|[使用 Operations Manager 2007 监视的最佳做法](../technical-guides/best-practices-for-monitoring-with-operations-manager-2007.md)|  
|启用或禁用[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理包规则根据。|[使用 Operations Manager 2007 监视的最佳做法](../technical-guides/best-practices-for-monitoring-with-operations-manager-2007.md)|  
|将独立企业单一登录 (SSO) 的任何计算机添加到要由 BizTalk Server 管理包监视的计算机的列表。|[如何将企业单一登录计算机添加到由 BizTalk Server 管理包监视的计算机的列表](http://go.microsoft.com/fwlink/?LinkId=157263)(http://go.microsoft.com/fwlink/?LinkId=157263)。|  
  
## <a name="see-also"></a>另请参阅  
 [监视与 System Center Operations Manager 2007 的 BizTalk Server](../technical-guides/monitoring-biztalk-server-with-system-center-operations-manager-2007.md)