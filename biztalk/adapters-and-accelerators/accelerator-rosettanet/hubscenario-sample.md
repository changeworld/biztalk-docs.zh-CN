---
title: "HubScenario 示例 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eb6990ec-aea2-4362-8573-7f737a4fc7f1
caps.latest.revision: "15"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5b9b2770f1d14d716149025ac44cb3cdffbbb23b
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="hubscenario-sample"></a>HubScenario 示例
HubScenario 示例演示在网络集线器方案中如何管理消息传输。 该示例将发送到中间网络集线器的消息转换为发送到最终接收人的消息。  
  
 HubScenario 从服务内容中提取最终接收人的邓氏 (DUNS) 编码。 它管理签名证书、加密证书和目标 URL， 并为最终接收人生成一条新消息。  
  
 此示例处理 3A4 请求与响应消息以及 0C1 请求消息。 当你使用 HubScenario 创建用于个人目的的应用程序时，必须为每个消息合作伙伴接口流程 (PIP) 都生成例程。  
  
 HubScenario 示例包含 HubHelper.cs 项目和 HubScenario.odx 项目。  
  
 HubScenario 示例还包含一个绑定文件，可以用于导入接收端口 (MessagesToLOB_Receive_Port) 和接收位置 (MessagesToLOB_Receive_Location) 之间的绑定，以用于 HubScenario.odx 业务流程。 此绑定文件 (HubScenarioBinding.xml) 位于*\<驱动器 >*: \Program Files\\ [!INCLUDE[btsCoName](../../includes/btsconame-md.md)] Microsoft BizTalk\<版本 > Accelerator for RosettaNet \SDK\HubScenario。 使用 BTSTask 命令可以导入绑定。 有关详细信息，请参阅 [!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)] 帮助中的“ImportBindings 命令”主题。  
  
### <a name="to-build-and-initialize-this-sample"></a>构建和初始化此示例  
  
1.  在 Visual Studio 中，打开\<驱动器 >: files\microsoft Microsoft BizTalk\<版本 > RosettaNet\SDK\HubScenario\HubScenario.btproj 快捷键。 在解决方案资源管理器中，右键单击 HubScenario 项目，然后单击“属性”。 在为 HubScenario 项目的属性页中，在签名选项卡上选择**对程序集签名**复选框，然后选择**HubScenario.snk**中**选择强名称密钥文件**单击**确定**。  
  
2.  在解决方案资源管理器中，右键单击 HubHelper 项目，然后单击“属性”。 在 HubHelper 项目的“属性”页中，在“签名”选项卡中选中“为程序集签名”复选框。 在选择强名称密钥文件字段中，选择新类型**HubHelper.snk**作为密钥文件名称，然后单击**确定**。  
  
    > [!NOTE]
    >  如果没有在 HubScenario 和 HubHelper 项目中手动输入程序集密钥文件，则这些程序集将不会进行部署。  
  
3.  在命令提示符下，将移到*\<驱动器 >*: \Program Files\\ [!INCLUDE[btsCoName](../../includes/btsconame-md.md)] Microsoft BizTalk\<版本 > Accelerator for RosettaNet\SDK\HubScenario 文件夹。 运行文件 Setup.bat（如果在 64 位计算机上，则运行 Setupx64.bat）。  
  
## <a name="demonstrates"></a>演示  
 HubScenario.ods 业务流程演示如何执行以下任务：  
  
1.  从业务线应用程序接收消息。  
  
2.  删除服务内容中的 `CDATA` 元素，返回 XML 字符串。  
  
3.  检索最终消息的目标参与方名称、PIPCode、PIPInstanceID 和 PIPVersion。  
  
4.  检索最终接收人的邓氏 (DUNS) 编码。  
  
5.  确定消息的类别，向服务内容添加包含对适当架构的引用的 DOCTYPE 元素。  
  
6.  使用新的目标参与方名称、邓氏 (DUNS) 编码、PIP 代码信息和服务内容构造一条消息。  
  
7.  提交消息以供 [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] 进行处理。 这是对 `SubmitRNIF.SubmitMessage` 的一个调用。  
  
## <a name="see-also"></a>另请参阅  
 [示例基于中心的方案](../../adapters-and-accelerators/accelerator-rosettanet/sample-hub-based-scenario.md)   
 [业务流程示例](../../adapters-and-accelerators/accelerator-rosettanet/orchestration-samples.md)