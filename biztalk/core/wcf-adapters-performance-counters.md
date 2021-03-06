---
title: WCF 适配器性能计数器 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- performance, WCF adapters
- performance, performance counters
- WCF adapters, performance
ms.assetid: 9feb052f-5674-419f-84ab-9b5d312a04a5
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e5b916b6212da18dcf4aa48d4ca941e23413513d
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37016248"
---
# <a name="wcf-adapters-performance-counters"></a>WCF 适配器性能计数器
性能计数器可用于监视的系统的站点上的服务执行的工作的特定方面。 性能计数器能够帮助您标识和解决有关服务器性能的问题。 WCF 适配器不提供自己的性能计数器。 但是，您可以监控 Windows Communication Foundation (WCF) 性能计数器以衡量 WCF 接收位置的性能。 若要将 WCF 性能计数器用于 WCF 接收位置，则必须为运行接收位置的主机实例启用性能计数器。  
  
> [!NOTE]
>  WCF 性能计数器不可用于 WCF 发送端口。  
  
 对于进程内 WCF 适配器，可以通过 BTSNTSvc.exe.config 文件启用性能计数器。 对于独立 WCF 适配器，可以修改 Web.config 文件以启用性能计数器。 有关 WCF 性能计数器的详细信息，请参阅"WCF 性能计数器"处[ http://go.microsoft.com/fwlink/?LinkID=87245 ](http://go.microsoft.com/fwlink/?LinkID=87245)。  
  
## <a name="enabling-the-wcf-performance-counters-for-the-wcf-receive-locations"></a>为 WCF 接收位置启用 WCF 性能计数器  
 对于进程内 WCF 适配器，可以通过 BTSNTSvc.exe.config 文件启用性能计数器。  
  
 对于独立 WCF 适配器，可以通过修改 BizTalk WCF 服务发布向导在 Web 应用程序文件夹中创建的 Web.config 文件来启用 WCF 跟踪。  
  
 若要修改 BTSNtSvc.exe.config 或 Web.config，请打开相应配置文件，然后配置 WCF 跟踪，如下面的配置示例所示：  
  
> [!NOTE]
>  BTSNTSvc.exe.config 文件始终与 BTSNTSvc.exe 文件位于同一目录中，所在目录通常为 [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]。  
  
```  
<configuration>  
 <system.serviceModel>  
 <diagnostics performanceCounters="All" />  
 </system.serviceModel>  
 </configuration>  
```  
  
 **PerformanceCounters**属性可设置为启用特定类型的性能计数器。 有效值为  
  
- **所有**： 所有类别计数器 (**ServiceModelService**， **ServiceModelEndpoint**，并且**ServiceModelOperation**) 启用。  
  
- **ServiceOnly**： 仅**ServiceModelService**启用类别计数器。  
  
- **关闭**： 禁用 ServiceModel * 性能计数器。 这是默认值。  
  
  修改 BTSNTSvc.exe.config 文件之后，必须重新启动运行进程内 WCF 接收位置的主机实例。  
  
## <a name="types-of-performance-counters"></a>性能计数器的类型  
 WCF 性能计数器可分为三个不同级别： 服务、 终结点和操作。  
  
 **服务性能计数器**  
  
 服务性能计数器评估整个服务行为，可用于诊断整个服务的性能。 下可找到这些**ServiceModelService 3.0.0.0**性能对象时使用性能监视器查看。 实例使用以下模式进行命名：  
  
```  
biztalkserviceinstance@<URI of a receive location>  
```  
  
 因为 WCF 适配器为每个接收位置创建一个单独的服务主机，所以会为每个接收位置创建一个性能计数器实例。 有关实现 WCF 的服务类的详细信息的服务协定，请参阅**BizTalkServiceInstance 类** [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。 
  
 **终结点性能计数器**  
  
 使用终结点性能计数器可以查看反映终结点接受消息时所采用方式的数据。 下可找到这些**ServiceModelEndpoint 3.0.0.0**性能对象时使用性能监视器查看。 实例使用以下模式进行命名：  
  
```  
biztalkserviceinstance.<WCF service contract>@<URI of a receive location>  
```  
  
 对每个接收位置均会创建一个性能计数器实例。 在上面的模式中，WCF 服务约定的名称表示 WCF 适配器选择用于通过接收位置接收消息的服务约定。 有关 WCF 适配器如何选择服务协定从可用 WCF 服务协定，请参阅**WCF 适配器服务协定引用** [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。  
  
 **操作性能计数器**  
  
 下找到操作性能计数器**ServiceModelOperation 3.0.0.0**性能对象时使用性能监视器查看。 对每个接收位置会创建两个性能计数器实例。 其中一个对象实例使用以下模式进行命名：  
  
```  
biztalkserviceinstance.<WCF service contract>biztalksubmit@<URI of a receive location>  
```  
  
 在上面的模式中，WCF 服务约定的名称表示 WCF 适配器选择用于通过接收位置接收消息的服务约定。 **biztalksubmit**是服务协定中声明的操作名称，将导致运行时元数据中创建 WSDL 操作。  
  
> [!NOTE]
>  有关 WCF 适配器如何选择服务协定从可用 WCF 服务协定，请参阅**WCF 适配器服务协定引用** [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。
  
 另一个对象实例使用以下模式进行命名：  
  
```  
biztalkserviceinstance.<WCF service contract><twowaymethod|onewaymethod>@<URI of a receive location>  
```  
  
 此性能计数器实例表示异步处理通过接收位置传入的消息的操作。 此实例的操作名称部分可以是**twowaymethod**或**onewaymethod**根据 WCF 适配器的接收位置中使用的类型。 如果使用 Wcf-netmsmq 适配器，实例拥有**onewaymethod**创建操作名称。 对于其他适配器， **twowaymethod**用于操作名称部分。