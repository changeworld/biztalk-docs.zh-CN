---
title: 如何恢复挂起的业务流程实例 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- instances, resuming [HAT]
- HAT, resuming orchestrations
- HAT, resuming pipelines
- orchestrations, resuming
- resuming, pipelines
- resuming, orchestrations
- HAT, debug mode
ms.assetid: da133183-68d9-48d1-9601-8f6d4d5b8898
caps.latest.revision: 18
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5f3243173f454d560515d1c3cbb9bef749fc17d6
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36991166"
---
# <a name="how-to-resume-suspended-orchestration-instances"></a>如何恢复挂起的业务流程实例
如果你已挂起被列为“可恢复的挂起”的业务流程实例，则可以尝试从查询结果或预览窗格中恢复该业务流程实例。 只有在导致业务流程实例挂起的根本问题也得到解决后，才能成功恢复该业务流程实例。  
  
## <a name="prerequisites"></a>必要條件  
 必须以 BizTalk Server Operators 组成员的身份登录，才能执行此过程。  
  
### <a name="to-resume-suspended-orchestration-instances"></a>恢复挂起的业务流程实例  
  
1. 单击**启动**，单击**程序**，单击[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]，然后单击**BizTalk Server 管理**。  
  
2. 在控制台树中，展开**BizTalk Server 管理**，然后单击 BizTalk 组。  
  
3. 在详细信息窗格中，单击**新查询**选项卡。  
  
4. 在中**查询表达式**组中，在**值**列中，选择**挂起服务实例**从下拉列表框。  
  
5. 执行以下操作之一：  
  
   - 若要恢复单个实例，在**字段名**列，星号旁边的空下拉列表框中 (**\\**<em>)，选择 **服务名称</em>* 筛选器，然后在**值**列中，指定服务名称。  
  
   - 若要恢复实例，请在**字段名**列，星号旁边的空下拉列表框中 (**\\**<em>)，选择 **结果分组依据</em>* ，然后在**值**列中，指定服务名称。  
  
6. 单击**运行查询**。  
  
7. 在查询结果列表中，右键单击你想要继续，然后单击该业务流程实例**恢复实例**或**恢复实例**。 这允许您选择要恢复哪些实例。  
  
    [服务实例状态](../core/service-instance-states.md)上提供了详细信息上挂起状态。  
  
## <a name="see-also"></a>请参阅  
 [调查业务流程、端口和消息失败](../core/investigating-orchestration-port-and-message-failures.md)
