---
title: 对 Oracle 数据库适配器的安装问题进行故障排除 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installation issues, troubleshooting
- troubleshooting, installation issues
ms.assetid: 2054b725-d657-4039-b83b-119571935f62
caps.latest.revision: 15
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 1fff4cc7948bd05043de9d9028b2c2a39bf940b4
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36975958"
---
# <a name="troubleshoot-installation-issues-with-the-oracle-database-adapter"></a>对 Oracle 数据库适配器的安装问题进行故障排除
安装 Microsoft[!INCLUDE[adapterpacknoversion](../../includes/adapterpacknoversion-md.md)]复制产品二进制文件的计算机上并注册每个适配器的绑定。 本部分讨论如何使用故障排除技术来解决安装错误，并还列出了一些已知的问题。  

## <a name="logging-messages-for-setup-actions"></a>安装程序操作的日志记录消息  
 [!INCLUDE[adapterpacknoversion](../../includes/adapterpacknoversion-md.md)]的安装程序进行安装的标准任务[!INCLUDE[adapterpacknoversion](../../includes/adapterpacknoversion-md.md)]。 此外，安装程序还执行某些自定义操作，例如注册适配器绑定。 你可以记录这两个的标准，以及自定义操作安装程序将执行的消息。  

- [!INCLUDE[adapterpacknoversion](../../includes/adapterpacknoversion-md.md)]安装程序将安装使用 MSI 的特定于适配器的文件。 因此，安装程序的日志记录是标准的 MSI 日志记录。 

- 安装程序执行的自定义操作的所有日志都位于 %temp%\adaptersetup.log。 如果跟踪日志文件失败，跟踪还提供了在事件日志。  

##  <a name="BKMK_OraDBBinding"></a> 安装程序无法注册适配器绑定  
 **问题**  

 Microsoft[!INCLUDE[adapterpacknoversion](../../includes/adapterpacknoversion-md.md)]安装向导无法注册适配器绑定，但将继续进行安装适配器。  

 **原因**  

 这可能会由于存在问题导致[!INCLUDE[firstref_btsWinCommFoundation](../../includes/firstref-btswincommfoundation-md.md)]安装，[!INCLUDE[afproductnamelong](../../includes/afproductnamelong-md.md)]安装或被损坏的 machine.config 文件。 适配器绑定写入到 machine.config 文件中。  

 **解决方法**  

手动注册[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]绑定： 

1. 导航到计算机上的 machine.config 文件。 例如，在 32 位平台上，在 machine.config 位于下\<系统驱动器\>: \WINDOWS\Microsoft.NET\Framework\\< 版本\>\CONFIG。  

    在此路径中，\<版本\>是.NET Framework 的版本。  

2. 使用文本编辑器打开该文件。  

3. 若要注册[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]绑定：  

   1. 搜索元素"的 system.serviceModel"并将其下的以下代码添加：  

      ```  
      <client>  
        <endpoint binding="oracleDBBinding" contract="IMetadataExchange" name="oracleDb" />  
      </client>  
      ```  

   2. 搜索"bindingElementExtensions"system.serviceModel\extensions 下的元素。  

   3. 查找缺失[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]绑定。 添加"bindingElementExtensions"节点下的以下部分。  

       有关[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]，添加：  

      ```  
      <add name="oracleDBAdapter" type="Microsoft.Adapters.OracleDB.OracleDBAdapterExtensionElement,Microsoft.Adapters.OracleDB, Version=<version>, Culture=neutral, PublicKeyToken=<public key>" />  
      ```  

   4. 搜索"bindingExtensions"system.serviceModel\extensions 下的元素。  

   5. 查找缺失[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]绑定。 添加"bindingExtensions"节点下的以下部分。  

       有关[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]，添加：  

      ```  
      <add name="oracleDBBinding" type="Microsoft.Adapters.OracleDB.OracleDBAdapterBindingSection,Microsoft.Adapters.OracleDB, Version=<version>, Culture=neutral, PublicKeyToken=<public key>" />  
      ```  

   > [!NOTE]
   >  有关如何确定公用密钥和版本信息，请参阅[确定公用密钥和版本](#BKMK_PubKey)。  

4. 保存并关闭 machine.config 文件。  

####  <a name="BKMK_PubKey"></a> 确定公用密钥和版本  
 执行以下步骤来确定的公钥[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]。  

1. 导航到 Windows 目录，通常 C:\WINDOWS\assembly。  

2. 右键单击的 DLL 为其也想公用密钥和版本，并选择**属性**。 下表列出了为 DLL 的名称[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]。  


   |                                  适配器                                  |       DLL 的名称       |
   |---------------------------------------------------------------------------|-----------------------------|
   | [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)] | Microsoft.Adapters.OracleDB |


3. 上**常规**选项卡上，针对值**公钥标记**标签指定 DLL 的公共密钥。 同样，针对值**版本**标签指定 dll 的版本号。  

4. 复制公钥，，然后单击**取消**。  

##  <a name="BKMK_ConsumeBinding"></a> 在 64 位安装上使用使用适配器服务外接程序或添加适配器服务引用插件时出错  
 **问题**  

 使用[!INCLUDE[addadapterservreflong](../../includes/addadapterservreflong-md.md)]或[!INCLUDE[consumeadapterservlong](../../includes/consumeadapterservlong-md.md)]从[!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]运行的 64 位版本的 64 位计算机上[!INCLUDE[adapterpacknoversion](../../includes/adapterpacknoversion-md.md)]会导致以下错误：  

```  
No valid adapters are installed on this machine  
```  

 **原因**  

 [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]是 WCF 自定义绑定，后者在 machine.config 文件中的 System.ServiceModel 下注册。 64 位平台都有两个 machine.config 文件、 一个 32 位应用程序使用，另一个 64 位应用程序使用。 因此，当你安装 64 位版本的[!INCLUDE[adapterpacknoversion](../../includes/adapterpacknoversion-md.md)]，安装向导在 machine.config 文件的 64 位版本中注册绑定。 但是，[!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]作为 32 位进程运行，因此启动[!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]从[!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]，该插件检查 machine.config 文件的 32 位版本中的绑定并失败错误。  

 **解决方法**  

- 安装的 32 位和 64 位版本[!INCLUDE[adapterpacknoversion](../../includes/adapterpacknoversion-md.md)]64 位上[!INCLUDE[afproductnameshort](../../includes/afproductnameshort-md.md)]安装。  

  > [!IMPORTANT]
  >  必须只有 64 位[!INCLUDE[afproductnameshort](../../includes/afproductnameshort-md.md)]安装。 通过并行安装 32 位和 64 位的[!INCLUDE[afproductnameshort](../../includes/afproductnameshort-md.md)]不支持在一台计算机上。  

- 安装修补程序集 11.1.0.7 的 Oracle 客户端 11.1.0.6 Oracle 数据访问组件的 32 位和 64 位版本。  

  > [!NOTE]
  >  若要确保你的应用程序处理 ODP.NET 的最新版本，必须具有策略的"Dll"的计算机上安装和在 GAC 中注册。 有关详细信息，请参阅[适用于.NET 的 Oracle 数据提供程序](http://go.microsoft.com/fwlink/p/?LinkId=92834)Oracle 的网站上。  

##  <a name="BKMK_InvalidBinding"></a> 无效的绑定上的 64 位安装 BizTalk Server 管理控制台中配置 Oracle 数据库适配器端口时的错误  
 **问题**  

 当您尝试为中的适配器配置端口[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理控制台中，则会收到以下错误：  

```  
"Unable to create binding configuration element for editing. Check the values of the BindingType and BindingConfiguration properties.  
(Microsoft.Biztalk.Adapter.Wcf.Converters.CreateBindingException) Unable to get binding type for binding extension "oracleDBBinding".  
Verify the binding extension is registered in machine.config."  
```  

 **原因**  

 [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]是 WCF 自定义绑定，后者在 machine.config 文件中的 System.ServiceModel 下注册。 64 位平台都有两个 machine.config 文件、 一个 32 位应用程序使用，另一个 64 位应用程序使用。 因此，当你安装 64 位版本的[!INCLUDE[adapterpacknoversion](../../includes/adapterpacknoversion-md.md)]，安装向导在 machine.config 文件的 64 位版本中注册绑定。 但是，[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]作为 32 位进程运行管理控制台，因此在配置适配器的端口时，它会检查 32 位版本的 machine.config 文件中的绑定和失败错误。  

 **解决方法**  

- 安装的 32 位和 64 位版本[!INCLUDE[adapterpacknoversion](../../includes/adapterpacknoversion-md.md)]64 位上[!INCLUDE[afproductnameshort](../../includes/afproductnameshort-md.md)]安装。  

  > [!IMPORTANT]
  >  必须只有 64 位[!INCLUDE[afproductnameshort](../../includes/afproductnameshort-md.md)]安装。 通过并行安装 32 位和 64 位的[!INCLUDE[afproductnameshort](../../includes/afproductnameshort-md.md)]不支持在一台计算机上。  

- 安装修补程序集 11.1.0.7 的 Oracle 客户端 11.1.0.6 Oracle 数据访问组件的 32 位和 64 位版本。  

  > [!NOTE]
  >  若要确保你的应用程序处理 ODP.NET 的最新版本，必须具有策略的"Dll"的计算机上安装和在 GAC 中注册。 有关详细信息，请参阅[适用于.NET 的 Oracle 数据提供程序](http://go.microsoft.com/fwlink/p/?LinkId=92834)Oracle 网站上。 

## <a name="see-also"></a>请参阅  
[Oracle 数据库适配器疑难解答](../../adapters-and-accelerators/adapter-oracle-database/troubleshoot-the-oracle-database-adapter.md)