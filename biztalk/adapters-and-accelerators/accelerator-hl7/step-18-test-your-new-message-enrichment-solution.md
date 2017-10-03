---
title: "步骤 18： 测试您的新消息扩充解决方案 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: message enrichment tutorial, testing solution
ms.assetid: 233fbf79-0ab1-4064-b828-6bbbb56cbec2
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: ca2716a5d05292f105798cf394cd05bac1104c4b
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="step-18-test-your-new-message-enrichment-solution"></a>步骤 18： 测试您的新消息扩充解决方案
你可以在此步骤中，来测试使用 WSClient 应用程序将消息发送到你的解决方案[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]、 查看按预期方式，MLLPReceive 应用程序是否收到 HL7 格式的消息。  
  
### <a name="to-test-your-solution"></a>若要测试你的解决方案  
  
1.  打开命令提示符。  
  
    > [!NOTE]
    >  步骤 2 需要你已安装使用自定义安装过程 MLLP 测试工具。 如果你的计算机不存在包含 MllpReceive.exe 和 MllpSend.exe 目录 \MLLP 实用程序通过执行自定义安装中安装。 有关信息，请参阅[执行自定义安装](http://msdn.microsoft.com/library/e55c86e1-af63-49ba-8510-d177e1b96692)。  
  
2.  在命令提示符处，键入 **cd \<*驱动器*>: files\microsoft BizTalk\<版本 > 快捷键的 HL7\SDK\MLLP 实用工具 * * (其中\<*驱动器*> 是你安装驱动器号)，然后按**Enter**。  
  
3.  在命令提示符处，键入**mllpreceive/p 11000 /eb 11 /sb 28 /cr 13**，然后按**Enter**。 这运行 MLLP 侦听器应用程序侦听端口 11000 并指定 MLLP 消息中，默认 EB、 SB 和 CR 字符，并显示到屏幕接收任何消息。  
  
4.  打开第二个命令提示符。  
  
5.  在命令提示符处，键入 **cd \<*驱动器*>: \Tutorial\WSClient\bin\Debug**，，然后按**Enter**。  
  
6.  在命令提示符处，键入**wsclient john henry smith 123456789**，然后按**Enter**。 这将消息发送到包含示例身份证号的 123456789 和患者名称 John Henry Smith 的示例消息的 Web 服务。  
  
7.  片刻时间，MLLPReceive 应用程序将显示传入 MLLP 消息。 消息应类似于以下形式：  
  
    ```  
    MSH|^~\&|TestTrailing^Delimiters|srcFac^srcFacUid|dstApp^dstAppUid|dstFac^dstFacUid|200307092343|sec|ADT^A04|msgid2134|P|2.2PID|||123456789||smith^john  
    ```  
  
     如果在几分钟后未收到响应，你应该检查应用程序事件日志中有任何错误，并开始进行故障排除。  
  
## <a name="see-also"></a>另请参阅  
 [消息扩充教程](../../adapters-and-accelerators/accelerator-hl7/message-enrichment-tutorial.md)