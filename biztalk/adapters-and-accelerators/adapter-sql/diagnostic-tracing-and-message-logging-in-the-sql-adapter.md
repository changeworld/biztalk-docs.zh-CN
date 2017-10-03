---
title: "诊断跟踪和消息日志记录中的 SQL 适配器 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d6599b4d-5650-4592-96af-ee43fb36357d
caps.latest.revision: "8"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: ff799af25c6ba74301eeab19eb793c2e84fd90e5
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="diagnostic-tracing-and-message-logging-in-the-sql-adapter"></a>诊断跟踪和消息日志记录中的 SQL 适配器
诊断跟踪有助于有效地诊断都使用适配器时可能遇到的问题。 适配器客户端可以激活两个级别的诊断跟踪：  
  
-   适配器客户端和适配器之间  
  
-   在该适配器  
  
 本部分提供有关激活这些级别的跟踪信息。  
  
## <a name="tracing-between-the-adapter-client-and-the-adapter"></a>适配器客户端和适配器之间的跟踪  
 适配器客户端可以启用 WCF 跟踪适配器客户端和适配器之间的跟踪问题。 WCF 跟踪用于跟踪的输入的 XML，来自适配器客户端，通过使用 WCF 服务模型，而在诊断序列化问题非常有用。 WCF 跟踪不用于 WCF 通道模型或从适配器到适配器客户端的输出消息。 可以通过将一段摘录添加到各自的配置文件来激活对 BizTalk 应用程序和 WCF 服务模型应用程序的 WCF 跟踪。 此外，你可以启用跟踪同时在设计时和运行时。  
  
-   **在设计时跟踪**。 对于设计时体验，你可能使用[!INCLUDE[addadapterservrefshort](../../includes/addadapterservrefshort-md.md)]， [!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]，或[!INCLUDE[addadapterwiz](../../includes/addadapterwiz-md.md)]。 所有这些工具可以从使用[!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]。 因此，若要启用跟踪的设计时体验，你必须添加摘录 devenv.exe.config 文件位于*\<安装驱动器 >*: files\microsoft Visual Studio * \<版本 >*\Common7\IDE。  
  
-   **在运行时跟踪**。 对于运行时跟踪，必须添加具体取决于你使用的应用程序的摘要。  
  
    -   有关[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]应用程序中，你必须添加到 BizTalk 配置文件，通常 BTSNTSvc.exe.config 摘录。有关[!INCLUDE[prague](../../includes/prague-md.md)]，此文件位于通常下\<安装驱动器 >: files\microsoft [!INCLUDE[prague](../../includes/prague-md.md)]。  
  
    -   WCF 服务模型.NET 应用程序，必须将摘录内容添加到你的项目的 app.config 文件。  
  
 若要启用 WCF 跟踪，添加以下摘录内容中的`<configuration>`标记。  
  
```  
\<system.diagnostics>  
    <sources>  
      <source name ="System.ServiceModel" switchValue="Verbose">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
      <source name ="System.ServiceModel.MessageLogging"   
              switchValue="Verbose, ActivityTracing">          
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
      <source name ="System.Runtime.Serialization" switchValue="Verbose">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
   </sources>  
   <sharedListeners>  
      <add name="xml" type="System.Diagnostics.XmlWriterTraceListener"                
           traceOutputOptions="LogicalOperationStack"   
           initializeData="C:\log\WCFTrace.svclog" />  
   </sharedListeners>  
   <trace autoflush="true" />  
  \</system.diagnostics>  
  \<system.serviceModel>  
    <diagnostics>  
      <messageLogging   
           logEntireMessage="true"   
           logMalformedMessages="false"  
           logMessagesAtServiceLevel="true"   
           logMessagesAtTransportLevel="false"/>  
    </diagnostics>      
  \</system.serviceModel>  
```  
  
 这将 WCF 跟踪保存到 C:\log\WCFTrace.svclog。 有关 WCF 跟踪的详细信息，请参阅[跟踪](https://msdn.microsoft.com/library/ms730342.aspx)。  
  
> [!IMPORTANT]
>  请确保减轻暴露敏感业务数据通过启用跟踪的潜在安全威胁。 有关建议，请参阅[最佳做法来保护 SQL 适配器](../../adapters-and-accelerators/adapter-sql/best-practices-to-secure-the-sql-adapter.md)。
  
## <a name="tracing-within-the-adapter"></a>跟踪中的适配器  
 适配器登录到跟踪文件，如错误、 警告和信息性消息的不同类别的有用信息。 此类信息可用于了解在适配器中的处理流程和与适配器诊断问题。 你可以激活[!INCLUDE[afproductnameshort](../../includes/afproductnameshort-md.md)]和适配器跟踪，BizTalk 应用程序和 WCF 服务模型应用程序通过将一段摘录添加到各自的配置文件。 此外，你可以启用跟踪同时在设计时和运行时。  
  
-   **在设计时跟踪**。 对于设计时体验，你可能使用[!INCLUDE[addadapterservrefshort](../../includes/addadapterservrefshort-md.md)]， [!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]，或[!INCLUDE[addadapterwiz](../../includes/addadapterwiz-md.md)]。 所有这些工具可以从使用[!INCLUDE[btsVStudioNoVersion](../../includes/btsvstudionoversion-md.md)]。 因此，若要启用跟踪的设计时体验，你必须添加摘录 devenv.exe.config 文件位于*\<安装驱动器 >*: files\microsoft Visual Studio * \<版本 >*\Common7\IDE。  
  
-   **在运行时跟踪**。 对于运行时跟踪，必须添加具体取决于你使用的应用程序的摘要。  
  
    -   有关[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]应用程序中，你必须添加到 BizTalk 配置文件，通常 BTSNTSvc.exe.config 摘录。有关[!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)]，此文件位于通常下\<安装驱动器 >: files\microsoft [!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)]。  
  
    -   WCF 服务模型.NET 应用程序，必须将摘录内容添加到你的项目的 app.config 文件。  
  
 若要启用[!INCLUDE[afproductnameshort](../../includes/afproductnameshort-md.md)]和适配器跟踪，添加以下摘录内容中的`<configuration>`标记。  
  
```  
\<system.diagnostics>  
    <sources>  
      <source name="Microsoft.ServiceModel.Channels" switchValue="Error">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
      <source name="Microsoft.Adapters.Sql" switchValue="Information">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add name="xml" type="System.Diagnostics.XmlWriterTraceListener"   
   traceOutputOptions="LogicalOperationStack"   
          initializeData="C:\log\AdapterTrace.svclog" />  
    </sharedListeners>  
    <trace autoflush="true" />  
  \</system.diagnostics>  
```  
  
 这将 WCF 跟踪保存到 C:\log\AdapterTrace.svclog。  
  
## <a name="viewing-the-traces"></a>查看跟踪内容  
 Windows Communication Foundation (WCF) 服务跟踪查看器工具可用于查看跟踪。 有关工具的详细信息，请参阅[使用服务跟踪查看器查看相关跟踪和问题](https://msdn.microsoft.com/library/aa751795.aspx)。
  
## <a name="configuring-tracking-for-biztalk-applications"></a>配置 BizTalk 应用程序的跟踪  
 BizTalk Server 管理控制台允许你配置的项目例如发送端口的各种跟踪选项，并接收端口。 跟踪配置设置，您可以跟踪入站和出站事件数据、 消息属性，消息正文和业务流程。 有关配置 BizTalk 应用程序的跟踪的详细信息，请参阅[管理项目](../../core/managing-artifacts.md)。
  
 你可以使用运行状况和活动跟踪 (HAT) 来查看历史记录或跟踪数据。 有关详细信息，请参阅[查看历史记录和跟踪数据](../../core/viewing-historical-and-tracked-data.md)。
  
## <a name="see-also"></a>另请参阅  
 [解决 SQL 适配器](../../adapters-and-accelerators/adapter-sql/troubleshoot-the-sql-adapter.md)