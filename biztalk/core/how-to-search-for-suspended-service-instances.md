---
title: 如何搜索挂起的服务实例 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- service instances, viewing
- service instances, Query tab [Administration Console]
- Query tab [Administration Console], service instances
- service instances, suspended
- Query tab [Administration Console], searching
- instances, suspended
- instances, services
ms.assetid: f91b1151-d879-4aa7-afc8-4cf13d928158
caps.latest.revision: 19
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9a2ed50337f45a158614755a10beb8f2be15f2c4
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36971750"
---
# <a name="how-to-search-for-suspended-service-instances"></a>如何搜索挂起的服务实例
可以使用**查询**搜索挂起的服务实例在 BizTalk Server 管理控制台中的选项卡。 您可以搜索消息的特定子集，以查找与服务名、类型、主机等相关联的特定消息。  

> [!NOTE]
>  对于有关的挂起服务实例，已终止且带有未使用的消息实例显示为错误代码（“已终止且带有未使用的消息”）。 这些实例是不可恢复的。  

> [!NOTE]
>  在按 URI 或错误适配器名称进行分组和筛选时，结果中将仅显示发送端口和接收端口。 对于所显示的结果中未包含的业务流程，将不能按 URI 进行分组和筛选。  

## <a name="prerequisites"></a>必要條件  
 若要执行此过程，则必须以 BizTalk Server Operators 组成员的身份登录。  

### <a name="to-search-for-suspended-service-instances"></a>搜索挂起的服务实例  

1. 单击**启动**，单击**所有程序**，单击**Microsoft**[!INCLUDE[btsBizTalkServer2006r3ui](../includes/btsbiztalkserver2006r3ui-md.md)]，然后单击**BizTalk Server 管理**。  

2. 在控制台树中，展开**BizTalk Server 管理**，然后单击 BizTalk 组。  

3. 在详细信息窗格中，单击**新查询**选项卡。  

4. 在中**查询表达式**组中，在**值**列中，选择**挂起服务实例**从下拉列表框。  

5. 在中**字段名**列，星号旁边的空下拉列表框中 (* *\\* * *)，选择一个或多项操作：  


   |         项          |                                                                                                                                                                                                                   Description                                                                                                                                                                                                                   |
   |-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   | **应用程序名称**  |                                                                                                                                                                                                   BizTalk Server 应用程序的名称。                                                                                                                                                                                                   |
   |   **创建时间**   |                                                                                                                                                                                  查找在指定日期之前或之后创建的挂起的服务实例。                                                                                                                                                                                   |
   |   **适配器错误**   | 可以按适配器类型对挂起的服务实例进行分组或筛选。 例如： 文件、 FTP、 HTTP、 MQSeries、 MSMQ、 POP3、 SMTP、 SOAP、 或 Windows SharePoint Services。 **注意：** 在查询结果中，适配器仅填充字段时使用指定的适配器时 BizTalk Server 运行时遇到错误。 如果运行时未找到适配器错误，则在查询结果中“适配器错误”字段为空。 |
   |    **错误代码**     |                                                                                                                                                 可以按照错误代码对挂起的服务实例进行分组或筛选，以显示具有该错误代码的所有已挂起的服务实例。                                                                                                                                                  |
   | **错误说明** |                                                                                                                                                                            可以对具有指定错误说明的挂起的服务实例进行分组或筛选。                                                                                                                                                                            |
   | **按结果进行分组**  |                                                                                                                                        可以按照适配器、应用程序、错误代码、错误说明、主机名称、服务级别、服务实例状态、服务名或 URI 对结果进行分组或筛选。                                                                                                                                         |
   |     **Host Name**     |                                                                                                                                                                                            按主机名称对挂起的服务实例进行分组或筛选。                                                                                                                                                                                            |
   |  **实例状态**  |                                                                                                                                                                         您可以搜索已挂起但不可恢复的实例，也可以搜索已挂起并可恢复的实例。                                                                                                                                                                         |
   |  **最大匹配数**  |                                                                                                                                                                                                        要显示的匹配数。                                                                                                                                                                                                        |
   |   **服务类**   |                                                                                                                                                       可以搜索以下内容：独立适配器；消息传送；消息传送和独立适配器；MSMQT；业务流程；或路由故障报告。                                                                                                                                                       |
   |   **服务名称**    |                                                                                                                                                                                      可以按服务名对挂起的服务实例进行分组或筛选。                                                                                                                                                                                       |
   |  **服务类型 ID**  |                                                                                                                                                                                     可以按服务类型 ID 对挂起的服务实例进行分组或筛选。                                                                                                                                                                                     |
   |  **挂起时间**  |                                                                                                                                                                        可以对在指定日期之前或之后挂起的服务实例进行分组或筛选。                                                                                                                                                                        |
   |        **URI**        |                                              可以按 URI 对挂起的服务实例进行分组或筛选。 **注意：** 在查询结果中，URI 仅填充时 BizTalk Server 运行时发送到指定的 URI 时遇到错误。 如果运行时在发送至 URI 时未找到错误，则在查询结果中，URI 字段为空或显示“URI 不可用”。                                              |


6. 完成**值**根据需要将所选内容中所做的列**字段名**列。  

7. 继续将其他行添加到查询根据需要，通过完成**字段名**，**运算符**，并**值**列，并单击**运行查询**。  

## <a name="see-also"></a>请参阅  
 [使用管理控制台的“查询”选项卡](../core/using-the-administration-console-query-tab.md)