---
title: "WCF 适配器安全建议 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WCF adapters, security
- security, WCF adapters
ms.assetid: bbaaca56-9ad5-4122-a8e9-6e975d308230
caps.latest.revision: "13"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 77ea0334e2d6164091e54321de8e1dccab5c07bd
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="wcf-adapters-security-recommendations"></a>WCF 适配器的安全建议
[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 使用 WCF 适配器来发布（接收）和使用（发送）WCF 服务。 我们建议您按照这些准则来确保您环境中的 WCF 适配器的安全以及部署它们。  
  
 有关 WCF 适配器的详细信息，请参阅[WCF 适配器](../core/wcf-adapters.md)。 有关 WCF 服务的详细信息，请参阅[使用 WCF 服务](../core/using-wcf-services.md)s。  
  
## <a name="security-recommendations-for-all-wcf-adapters"></a>针对所有 WCF 适配器的安全建议  
  
-   如果需要将前端用户的内容映射到后端系统中的凭据，则可以使用企业单一登录 (SSO)。  
  
-   并不是所有的服务都必须发布元数据。 使元数据发布功能保留为禁用状态可减少服务遭受攻击的可能性，同时降低无意中泄露信息的危险。 与元数据相关的安全问题的详细信息，请参阅"安全注意事项与元数据"在[http://go.microsoft.com/fwlink/?LinkId=196671](http://go.microsoft.com/fwlink/?LinkId=196671)。  
  
-   并非所有的元数据终结点绑定和服务终结点绑定的组合都是有效的。 在某些情况下，元数据终结点的绑定配置必须与其服务终结点的绑定配置一致。 例如，从与接收位置相同的位置提供元数据时，如果接收位置使用依赖于 HTTPS 的安全模式，则元数据终结点不能配置为需要 HTTP 传输的安全模式。  
  
    > [!NOTE]
    >  发布通过具有相同的位置，但要求依赖于 HTTPS 传输，BizTalk WCF 发布向导生成时，Web.config 文件中的安全模式的服务终结点的 HTTP 传输的元数据时必须设置这两个**httpsGetEnabled**和**httpGetEnabled**特性以**true**。  
  
-   WCF 适配器利用 Windows Communication Foundation (WCF) 的安全功能进行通信。 了解 WCF 在安全方面的功能和限制很重要。 WCF 的安全功能的详细信息，请参阅"Windows Communication Foundation 安全性"网址[http://go.microsoft.com/fwlink/?LinkId=87806](http://go.microsoft.com/fwlink/?LinkId=87806)。  
  
## <a name="security-recommendations-for-the-isolated-wcf-adapters"></a>针对独立 WCF 适配器的安全建议  
  
-   有关用于发布 Web 服务的安全建议，请参阅[启用 Web 服务](../core/enabling-web-services.md)。  
  
-   如 WCF CustomIsolated、 WCF-BasicHttp 和 WCF WSHttp 适配器的隔离的 WCF 适配器利用超文本传输协议 (HTTP) 发送和接收消息，并从[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]。 因此，你必须遵循安全建议以确保 Internet 信息服务 (IIS) 的安全。  
  
-   为独立的 WCF 接收位置创建应用程序池，你必须将它配置为是的成员的帐户下运行[!INCLUDE[btsWinNoVersion](../includes/btswinnoversion-md.md)]组的独立主机运行 WCF 接收适配器和 Internet 信息服务工作线程进程组 （IIS_WPG 组）。 随后，必须将 WCF 接收适配器的主机实例配置为使用此帐户。 如果更改了 IIS_WPG 组的帐户，则必须确保将主机实例也更新为使用该新帐户运行。  
  
## <a name="security-recommendations-for-the-wcf-custom-adapter"></a>针对 WCF-Custom 适配器的安全建议  
  
-   如果 WCF 自定义接收位置碰巧使用 HTTP 内核模式驱动程序 (HTTP.sys)，如**httpsTransport**对于安全套接字层 (SSL) 通信，接收位置的绑定元素必须具有证书注册为每个套接字 （IP 地址/端口组合）。 使用 HttpCfg.exe 工具可将 SSL 证书绑定到计算机上的端口。 有关详细信息，请参阅"如何为:: 配置端口使用 SSL 证书" [http://go.microsoft.com/fwlink/?LinkId=86384](http://go.microsoft.com/fwlink/?LinkId=86384)。  
  
## <a name="security-recommendations-for-the-wcf-netmsmq-adapter"></a>针对 WCF-NetMsmq 适配器的安全建议  
  
-   若要使用 WCF NetMsmq 适配器，你必须配置 WCF NetMsmq 适配器的 MSMQ 安全设置同样适用于相同的方式[netMsmqBinding](http://go.microsoft.com/fwlink/?LinkId=87813)。 有关如何配置 MSMQ 安全设置的详细信息**netMsmqBinding**，请参阅"故障排除排队消息传递"在[http://go.microsoft.com/fwlink/?LinkId=87816](http://go.microsoft.com/fwlink/?LinkId=87816)。  
  
## <a name="wcf-adapters-use-the-chaintrust-mode-to-validate-certificates"></a>WCF 适配器使用 ChainTrust 模式来验证证书。  
  
-   由于标准 WCF 收到适配器使用[ChainTrust](http://go.microsoft.com/fwlink/?LinkId=88960)模式下，若要验证客户端和服务证书中，你必须安装用于验证的 X.509 证书的 CA 证书链。 你可以使用 WCF 自定义或 WCF CustomIsolated 适配器若要更改此默认行为。  
  
## <a name="security-auditing-for-the-wcf-adapters"></a>WCF 适配器的安全审核  
  
-   默认情况下，WCF 适配器不使用 WCF 安全审核功能。 为 WCF 适配器启用 WCF 安全审核功能有多种方式。 有关 WCF 安全审核功能的详细信息，请参阅"审核安全事件"在[http://go.microsoft.com/fwlink/?LinkId=88975](http://go.microsoft.com/fwlink/?LinkId=88975)。  
  
-   若要使用的 WCF 安全，与 WCF 自定义接收适配器审核功能，你可以配置**ServiceSecurityAuditBehavior**接收位置。  
  
-   对于进程内 WCF 适配器，可以通过 BTSNTSvc.exe.config 文件启用性能计数器。 对于独立的 WCF 适配器，请通过修改 BizTalk WCF 服务发布向导创建的 Web 应用程序文件夹中的 Web.config 文件来启用 WCF 跟踪。 若要修改 BTSNtSvc.exe.config 或 Web.config，请打开相应配置文件，然后配置 WCF 跟踪，如下面的配置示例所示：  
  
    > [!NOTE]
    >  BTSNTSvc.exe.config 文件始终与 BTSNTSvc.exe 文件位于同一目录中，所在目录通常为 [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]。  
  
    > [!NOTE]
    >  修改 BTSNTSvc.exe.config 文件之后，必须重新启动运行进程内 WCF 接收位置的主机实例。  
  
    ```  
    <configuration>  
        <system.serviceModel>  
          <diagnostics performanceCounters="All" />  
          <behaviors>  
            <serviceBehaviors>  
              <behavior name="ServiceBehaviorConfiguration">  
                <serviceSecurityAudit  
                          auditLogLocation="Application"  
                          suppressAuditFailure="true"  
                          serviceAuthorizationAuditLevel="SuccessOrFailure"  
    messageAuthenticationAuditLevel="SuccessOrFailure" />  
              </behavior>  
            </serviceBehaviors>  
          </behaviors>  
          <services>  
            <service name="Microsoft.BizTalk.Adapter.Wcf.Runtime.BizTalkServiceInstance" behaviorConfiguration="ServiceBehaviorConfiguration">  
            </service>  
          </services>        
        </system.serviceModel>  
    </configuration>  
    ```  
  
-   您还可以使用与安全相关的性能计数器（如 Security Calls Not Authorized）来监视 WCF 适配器。 有关如何启用对 WCF 性能计数器的详细信息，请参阅[WCF 适配器性能计数器](../core/wcf-adapters-performance-counters.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Planning for Security](../core/planning-for-security.md)