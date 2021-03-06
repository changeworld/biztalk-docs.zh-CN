---
title: 如何配置 Wcf-nettcp 接收处理程序 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- WCF-NetTcp adapters, global variables
- receive handlers, WCF-NetTcp adapters
- configuring [WCF-NetTcp adapters], global variables
- configuring [WCF-NetTcp adapters], receive handlers
ms.assetid: a4a283d1-21de-4d6b-9cb5-f2f9f823903b
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c8d7e68e4df5a729aae7f84932b53d319fea0114
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37009942"
---
# <a name="how-to-configure-a-wcf-nettcp-receive-handler"></a>如何配置 WCF-NetTcp 接收处理程序
可使用以下过程配置 WCF-NetTcp 接收处理程序。  

### <a name="to-change-global-variables-for-a-wcf-nettcp-receive-handler"></a>更改 WCF-NetTcp 接收处理程序的全局变量  

1. 在 BizTalk 管理控制台中，展开[!INCLUDE[btsBizTalkServer2006r3ui](../includes/btsbiztalkserver2006r3ui-md.md)]**管理**，展开**BizTalk 组**，展开**平台设置**，然后展开**适配器**。  

2. 在展开的适配器列表中，单击**WCF NetTcp**，在右窗格中，右键单击你想要配置，接收处理程序，再单击**属性**。  

3. 在中**适配器处理程序属性**对话框中，在**常规**选项卡上，在**主机名**列表中，选择接收处理程序将关联的主机。  

4. 在中**常规**选项卡上，单击**属性**，然后在**接收处理程序**选项卡上，执行以下操作。  


   |        使用此选项         |                                                                                                                         执行的操作                                                                                                                         |
   |-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | **最大连接数** | 指定监听程序可以拥有的等待应用程序接受的最大连接数。 在超过此配额值时，将删除新的传入连接，而不是等待接受这些连接。<br /><br /> 默认值为 10。 |


5. 单击“确定” 。  

## <a name="see-also"></a>请参阅  
 [配置 Wcf-nettcp 适配器](../core/configuring-the-wcf-nettcp-adapter.md)   
 [发布 WCF 服务](../core/publishing-wcf-services.md)