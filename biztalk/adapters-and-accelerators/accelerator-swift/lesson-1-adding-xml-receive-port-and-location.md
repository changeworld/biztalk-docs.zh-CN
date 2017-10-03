---
title: "第 1 课： 将 XML 添加接收端口和位置 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- receive locations, creating
- creating, receive locations
- receive ports, creating
- creating, receive ports
ms.assetid: 252bc080-3820-44cc-8749-715869f3f684
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 186cbb4e021a281ab834f04097f005c2597fbd37
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="lesson-1-adding-xml-receive-port-and-location"></a>第 1 课： 添加 XML 接收端口和位置
接收端口是类似的接收位置的逻辑分组。 接收位置的传入消息和用于处理该消息管道定义特定地址 （例如 URL 或文件的位置）。  
  
### <a name="to-add-a-receive-port"></a>若要添加接收端口  
  
1.  启动**BizTalk Server 管理**控制台。  
  
    > [!NOTE]
    >  BizTalk Server 管理控制台也可以打开从 Visual Studio 中通过单击**BizTalk Server 管理**中**工具**菜单。  
  
2.  在 BizTalk Server 管理控制台中，展开**BizTalk Server 管理**节点，则**BizTalk 组**节点，则**应用程序**节点，然后**BizTalk 应用程序 1**节点。  
  
3.  右键单击**接收端口**，指向**新建**，然后单击**单向接收端口**。  
  
4.  在接收端口属性对话框中，在**名称**框中，键入**MT103_XML_ReceivePort**。  
  
5.  单击**应用**以绑定端口，然后单击**确定。**  
  
6.  右键单击**接收位置**，指向**新建**，然后单击**单向接收位置**。  
  
7.  在选择接收端口对话框中，单击**MT103_XML_ReceivePort**，然后单击**确定**。  
  
8.  在接收位置属性对话框中，在**名称**框中，键入**MT103_XML_ReceiveLocation**。  
  
9. 在**传输**部分中，为**类型**文本框中，单击下拉列表中，，然后选择**文件**。  
  
10. 单击**配置**类型下拉列表右侧的按钮。  
  
11. 在文件传输属性对话框中，单击**浏览**。 将移动到**\<驱动器 >: \Labs**文件夹，，然后单击**新建文件夹**。  
  
12. 在浏览文件夹对话框中，创建**入站**文件夹中的**\<驱动器 >: \Labs**，然后创建**XMLFile**文件夹中的 **\<驱动器 >: \Labs\Inbound**。 单击 **“确定”**。  
  
13. 在文件传输属性对话框中，确保 **\*.xml**中输入**文件掩码**框中，并依次**确定**。  
  
14. 在接收位置属性对话框中，确保**BizTalkServerApplication**为输入**接收处理程序**框。  
  
15. 有关**接收管道**框中，选择**XMLReceive**从下拉列表。  
  
16. 单击**应用**，然后单击**确定**。  
  
17. 在 BizTalk Server 管理控制台中，单击**接收位置**，右键单击**MT103_XML_ReceiveLocation**，然后单击**启用**。  
  
    > [!NOTE]
    >  启用接收位置后，BizTalk 主动轮询文件文件夹。  
  
 继续执行[第 2 课： 添加平面文件发送端口](../../adapters-and-accelerators/accelerator-swift/lesson-2-adding-a-flat-file-send-port.md)。