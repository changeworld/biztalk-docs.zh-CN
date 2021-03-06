---
title: 创建自定义管道来处理 JSON 消息 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b04faad1-b14b-4146-82c7-88a38d2a46a5
caps.latest.revision: 3
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e28f825b1f26f3c080a02fd9a2e2bf8960a816fd
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37005990"
---
# <a name="create-custom-pipelines-to-process-json-messages"></a>创建处理 JSON 消息的自定义管道
> [!NOTE]
>  本教程仅适用于 BizTalk Server。  
  
 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 提供了可用于处理 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 应用程序中的 JSON 消息的管道组件。 在此步骤中，我们使用这些管道组件来创建自定义管道，在配置 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 应用程序时使用。  
  
## <a name="create-a-custom-receive-pipeline"></a>创建自定义接收管道  
  
1. 在中[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]应用程序，从解决方案资源管理器，右键单击项目，然后指向**添加** > **新项** > **接收管道**. 管道命名为`JSONToXmlReceivePipeline.btp`，然后单击**添加**。  
  
2. 内**解码**阶段将添加新**JSON 解码器**。 在屏幕快照中所示的其他阶段以及其他管道组件中，保存更改。  
  
    ![自定义接收管道](../core/media/btsjson-receivepipeline.png "BTSJSON_ReceivePipeline")  
  
## <a name="create-a-custom-send-pipeline"></a>创建自定义发送管道  
  
1. 在中[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]应用程序，从解决方案资源管理器，右键单击项目，然后指向**添加** > **新项** > **发送管道**. 管道命名为`XmlToJSONSendPipeline.btp`，然后单击**添加**。  
  
2. 内**编码**阶段将添加新**JSON 编码器**。 在屏幕快照中所示的其他阶段以及其他管道组件中，保存更改。  
  
    ![自定义发送管道](../core/media/btsjson-sendpipeline.png "BTSJSON_SendPipeline")  
  
## <a name="see-also"></a>请参阅  
 [使用 BizTalk Server 处理 JSON 消息](../core/processing-json-messages-using-biztalk-server.md)