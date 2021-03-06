---
title: 配置 FileAct 和 InterAct 适配器 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0d3876ff-e8e4-47f4-9ca8-d4dad419ed67
caps.latest.revision: 20
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 2d62e4cf0896e755a0ec8ece00d6a2140210b463
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36974598"
---
# <a name="configure-the-fileact-and-interact-adapter"></a>配置 FileAct 和 InterAct 适配器
配置使用的不同项目[!INCLUDE[swift_adapter](../../includes/swift-adapter-md.md)]运行时。 

  
## <a name="prerequisites"></a>必要條件  
   
- 安装 [!INCLUDE[swift_adapter](../../includes/swift-adapter-md.md)]
  
- 以的成员身份登录[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]Administrators 组
  
- 确认 SQL Server 正在运行
  
## <a name="step-1-configure-the-fileact-and-interact-adapter"></a>步骤 1： 配置 FileAct 和 InterAct 适配器  
  
1.  在中**Microsoft BizTalk FileAct 和交互适配器配置**向导中，转到**概述**。 在左窗格中，选择**运行时**配置适配器运行时组件。  
  
2.  在中**运行时配置**下**帐户**，选择省略号 [...] 输入 COM plus 存储和转发模式配置。  
  
3.  在中**用户凭据**，输入用户名称 (在*域 \ 用户名*格式) 和 COM plus 配置中使用的帐户的密码。 选择“确定”。  
  
    > [!NOTE]
    >  一个**用户凭据**如果您输入的帐户有建议的更高权限，将显示警告。 选择**是**以继续。
  
4.  选择**应用配置**将 COM plus 配置应用到 FileAct 和交互的适配器。  
  
5.  在中**摘要**，查看，然后选择**下一步**。  
  
6.  配置完成后，查看组件的列表。 一个对勾意味着该组件已成功配置。 "X"意味着该组件的问题。  
  
    > [!NOTE]
    >  使用**日志文件**链接来查看配置事件。  
  
7.  选择**完成**以完成配置。 **概述**显示运行时组件的当前配置状态。  

接下来，创建要运行这些适配器的主机和主机实例。

## <a name="step-2-create-the-host-and-host-instances"></a>步骤 2： 创建主机和主机实例

我们建议你创建的专用的主机的 FileAct 适配器和 InterAct 适配器的单独的专用的主机。 对于每个适配器，创建至少一个主机实例。  

[管理 BizTalk 主机和主机实例](../../core/managing-biztalk-hosts-and-host-instances.md)列出的步骤创建主机和主机实例。 

创建后下, 一步是添加发送处理程序，并使用客户端消息合作伙伴创建 SWIFT 联盟网关 （压降） 中。

## <a name="step-3-create-the-send-handler"></a>步骤 3： 创建的发送处理程序

使用 FileAct 和 InterAct 发送处理程序属性的发送端口配置值，如果在单个 FileAct 上未设置的属性或 InterAct 发送端口。 
  
1. 在中**BizTalk Server 管理**控制台中，展开**BizTalk Server 管理**，展开**BizTalk 组**，展开**平台设置**，然后展开**适配器**。  
  
2. 选择**FileAct**或**InterAct**适配器。 在右窗格中，双击发送处理程序。  
  
3. 在中**主机名**下拉列表中，选择在上一部分中创建的主机。 然后选择**属性**。  
  
4. 在中**传输属性**，选择**自变量**属性，并输入以下参数为：  
  
    `-SagMessagePartner <Client Message Partner created in SAG\>`
  
   > [!NOTE]
   >  替换 <`Client Message Partner created in SAG`> 客户端消息合作伙伴的名称。 保留默认值为加密模式、 FACrypto 模式和日志消息属性。  
  
5. 选择**确定**以保存所做的更改，然后关闭属性窗口。 
  
6. 下**平台设置**，选择**主机实例**。  
  
7. 重新启动主机实例： 

   - 右键单击 FileAct 主机实例，并**重新启动**
   - 右键单击交互主机实例，并**重新启动**。  

接下来，输入 SWIFTNet paramfile 中的服务器消息合作伙伴，若要启用 FileAct 和 InterAct 接收适配器。
  
## <a name="step-4-configure-the-swiftnet-param-file"></a>步骤 4： 配置 SWIFTNet 参数文件

若要启用 FileAct 和 InterAct 接收适配器初始化的值，必须在 SWIFTNet paramfile 中输入合作伙伴在压降中创建的服务器消息。 Paramfile 通常位于`c:\SWIFTAlliance\RA\<remote access instance name\>\cfg\paramfile`。 配置 paramfile 后，开始**SnlReceiver.exe**。  
  
1. 打开**SWIFTNet paramfile**。 中的位置标记为"***"将以下代码添加。 请注意，`AdapterType`值可以是`Interact`或`Fileact`。  
  
     ```spawn "snlreceiver -SagMessagePartner <Server MessagePartnerName\> -AdapterMode <AdapterType\>"```  
       
  
   ```  
    username:snlowner  
    subsystem_name:SampleSubsystem  
    #subsystem_group: SampleSubsystem  
    #subsystem_dependency:Support,Swarm  
    subsystem_nature:critical  
    subsystem_start:  
    ***  
    *END  
    subsystem_stop:  
    *KILL9:snlreceiver  
    *END  
    subsystem_status:  
    *NB:1:snlreceiver  
    *END  
    start_event:SNL001:subsystem SampleSubsystem is up  
    stop_event:SNL002:subsystem SampleSubsystem is down  
   ```  
  
> [!NOTE]
>  在开始 SNLreceiver 之前，启用接收端口的适配器使用 （FileAct 或交互）。  
  
2. 启动和停止 SnlReceiver.exe:

    1.  在桌面上，选择**远程 API**图标以打开远程 API 的命令提示符。  
  
    2.  在命令提示符处，键入`Swiftnet start`。 选择 enter 键以启动 SnlReceiver.exe。  
  
    3.  在命令提示符处，键入`Swiftnet stop`。 选择 ENTER 以停止 SnlReceiver.exe。  

  
接下来，更新文件**autoexec.bat**来设置环境变量的 SWIFT。

## <a name="step-5-update-autoexecbat-to-configure-the-receive-adapters"></a>步骤 5： 更新 autoexec.bat 若要配置的接收适配器

更新**autoexec.bat**文件以将 SWIFT 环境变量设置的计算机上的安装位置[!INCLUDE[swift_adapter](../../includes/swift-adapter-md.md)]接收适配器。 从已安装在路径中的接收适配器的系统生成的环境变量`c:\SWIFTAlliance`与名为的接收适配器的实例**Ra1**。 更新你的配置适当的 SWIFT 环境变量。  
  
 下面是 autoexe.bat 文件的一个示例：
  
```  
SET COMPUTERNAME=<Machine Name>  
SET GENLOG_DIR=C:\SWIFTAlliance\RA\Ra1\log  
SET GENUTIL_DIR=C:\SWIFTAlliance\RA\bin  
SET HOMEDRIVE=C:  
SET LOGONSERVER=\\SERVERNAME  
SET OSA_DIR=C:\SWIFTAlliance\RA\Ra1\log  
SET OSA_INSTANCE=Ra1  
SET PKIEXECDIR=C:\SWIFTAlliance\RA  
SET SAGRA_HOME=C:\SWIFTAlliance\RA  
SET SESSIONNAME=RDP-Tcp#1  
SET SLP_ENV=DEFAULT  
SET SLP_FILE=server.slp  
SET SNL_DOMAIN_NAME=Ra1  
SET SPK_DATA_DIR=C:\SWIFTAlliance\RA\data\pki  
SET SWNET_BIN_PATH=C:\SWIFTAlliance\RA\Ra1\bin  
SET SWNET_CFG_PATH=C:\SWIFTAlliance\RA\Ra1\cfg  
SET SWNET_HOME=C:\SWIFTAlliance\RA  
SET SWNET_HOST=HOSTNAME  
SET SWNET_INST=Ra1  
SET SWNET_LOG_PATH=C:\SWIFTAlliance\RA\Ra1\log  
SET SWNET_SLP_PATH=C:\SWIFTAlliance\RA\data\  
SET SWNET_VERSION=5.0.20  
SET SWTRACE=C:\SWIFTAlliance\RA\Ra1\log  
SET Path=%PATH%;C:\SWIFTAlliance\RA\bin  
SET Path=%PATH%;C:\SWIFTAlliance\RA\lib  
  
```  
  
## <a name="see-some-examples"></a>查看一些示例
FileAct 和 InterAct 消息的示例，请参阅[示例进行交互和 FileAct 消息](../../adapters-and-accelerators/fileact-interact/sample-interact-and-fileact-messages.md)。  
  
## <a name="see-also"></a>请参阅  

[安装 FileAct 和 InterAct 适配器](../../adapters-and-accelerators/fileact-interact/install-the-fileact-and-interact-adapter.md)  
[卸载或修复 FileAct 和 InterAct 适配器](../../adapters-and-accelerators/fileact-interact/uninstall-or-repair-the-fileact-and-interact-adapter.md)  
[阅读安装过程中的已知问题](../../adapters-and-accelerators/fileact-interact/read-the-installation-known-issues.md)
