---
title: 适配器宿主模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: cf9a8e6b-8c8d-47ec-b2a3-aed58206121d
caps.latest.revision: 14
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: d5576acf4251b9da420ac8747f4857c08064ed5b
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36978534"
---
# <a name="adapter-hosting-model"></a>适配器宿主模型
一般情况下 BizTalk 适配器的宿主 BizTalk 服务 Btsntsvc.exe。 这意味着，[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理适配器的生存期。 但也存在其他进程管理适配器的情况，如下所述。  
  
## <a name="in-process-adapters"></a>进程内适配器  
 由适配器[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]称为进程内适配器。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 执行以下操作适用于这些适配器：  
  
- 实例化适配器时[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]已启动  
  
- 初始化期间，将适配器的传输代理传递给适配器  
  
- 处理适配器的请求  
  
- 终止在关闭的适配器[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]服务  
  
  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 在运行时将处理程序配置和终结点配置信息传递给适配器。 还指定其他配置信息，例如服务时段，它定义启用适配器以处理请求的特定时间段。  
  
  可以使用 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理控制台或服务控制管理器手动关闭 BizTalk 服务。 如果连接到[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]数据库会自动丢失该服务将回收其自身。  
  
  在典型的宿主模型中，接收端适配器、发送端适配器与 BizTalk 服务及消息引擎和业务流程引擎的宿主均为同一进程。 宿主模型极其灵活，既允许将接收、发送和业务流程主机分开，也允许将它们合并。 下图中的主机在同一进程中执行这三种任务。  
  
  由于宿主模型富于变化，所以在开发适配器的过程中，一定要牢记发送适配器和接收适配器可能不会配置在同一主机中。 它们甚至可能配置为运行在不同的计算机上。  
  
  ![](../core/media/regularadapterhostingmodel.gif "RegularAdapterHostingModel")  
  进程内适配器宿主模型  
  
## <a name="isolated-adapters"></a>独立的适配器  
 有时接收适配器不可能驻留在 BizTalk 服务中。 例如，在某些 Internet 信息服务 (IIS) 进程模型中，ASP.NET 应用程序和 ISAPI 扩展的生存期是由 IIS 管理的。 BizTalk SOAP 适配器必须运行在同一进程空间中作为 IIS 中，从而使其不可能[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]来控制 SOAP 适配器的任何实例的生存期。  
  
 对于这些类型的适配器，有另一种宿主模型可供使用，即独立接收适配器，简称独立适配器。 没有独立发送适配器这一概念。  
  
 因为[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]不能创建一个独立的适配器，适配器必须获取其自己的传输代理并传输代理注册自身。  
  
 下图说明了[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]托管体系结构。 为了提升性能，独立主机结构尽量免除一切不必要的进程间通信。 由于独立适配器和 BizTalk 消息引擎堆栈位于同一进程中，因此该适配器调用消息引擎时没有进程间通信。 在此情况下，唯一的进程间通信发生在消息引擎和数据库之间，这是不可避免的。  
  
 ![](../core/media/isolatedadapters.gif "IsolatedAdapters")  
独立适配器宿主模型  
  
## <a name="see-also"></a>请参阅  
 [适配器框架概述](../core/what-is-the-adapter-framework.md)