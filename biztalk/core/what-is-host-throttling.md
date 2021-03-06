---
title: 主机阻止概述 | Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- host throttling, outbound
- host throttling, inbound
- host throttling, about host throttling
ms.assetid: 36d1818b-c8a2-4f23-bfb3-c034ee242f69
caps.latest.revision: 29
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: be272ae705fa85af7e240b5c296dae8d9c304de2
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36983710"
---
# <a name="what-is-host-throttling"></a>主机阻止概述
在 BizTalk Server 上执行的大部分处理都在称为 BizTalk Server 主机实例的逻辑实体内进行，该逻辑实体是在 BizTalk Server 上以 Windows 服务或独立的主机进程运行的进程。 为了管理主机实例进程使用的资源，BizTalk Server 使用可调整的阻止机制控制消息在主机实例中的传输和处理。  
  
 该阻止机制对主机实例的负载进行调节，以确保负载没有超过主机实例或任何下游主机实例的处理能力。 该阻止机制还防止称为资源争用的情况发生，这种情况会降低主机实例进程或其他系统进程的整体性能。 一个或多个进程消耗有限的资源从而损害进程自身和/或其他进程时，便会出现资源争用的情况。 例如，消耗过量的内存或线程将导致内存分配失败或大量的线程上下文切换，这会影响进程的性能。 这样的资源争用会降低 BizTalk Server 的整体性能。  
  
 主机阻止机制还检测可用资源利用不足的时间。 如果可用的资源未得到充分利用，则阻止机制将允许主机实例处理更多的消息。 主机阻止机制不断监视可用资源是否过度利用或利用不足，并据以调整通过主机实例的消息流。  
  
 BizTalk Server 主机阻止机制有助于确保系统以最佳可持续水平运行。  
  
 在 BizTalk Server 管理控制台中基于每台主机对主机阻止配置参数进行设置。 请注意，为主机设置的阻止配置参数将应用于所有接收处理程序、发送处理程序或相应主机实例中的业务流程。 如果要设置仅应用于特定接收处理程序、发送处理程序或业务流程的阻止参数，则应执行以下操作：  
  
-   创建新主机并相应地设置阻止参数。  
  
-   配置要在此主机中运行的接收处理程序、发送处理程序或业务流程。  
  
-   创建要在 BizTalk Server 上运行的此主机的一个或多个实例。  
  
## <a name="inbound-host-throttling"></a>入站主机阻止  
 入站的主机阻止，也称为*消息发布阻止功能*在 BizTalk Server 中，应用于包含的主机实例接收适配器或业务流程的消息发布到 MessageBox 数据库。 以下情况可以触发入站主机阻止条件：  
  
- 的内存量、 线程数或主机实例使用的数据库连接数超过中定义了阻止阈值**设置仪表板**推出的 BizTalk 组和选择**设置**。 这些值是下可用的性能监视器计数器可测量**biztalk: Message Agent**性能对象类别。  
  
- 下游主机无法处理发布的消息。 这会增加的值**DB 中的消息数**参数。 阈值**DB 中的消息数**值的触发阻止条件是可在配置**主机**选项**设置仪表板**。 在数据库中的消息计数可度量**数据库大小**计数器下**biztalk: Message Agent**性能对象类别。  
  
- **消息发布传入速率**主机实例超出**消息发布传出速率\\*** 指定**加速因子**值。 **加速因子**中定义值**设置仪表板**，**主机**，然后**基于速率的阻止**。 消息发布传入速率和传出速率可通过下的相应性能监视器计数器进行度量**biztalk: Message Agent**性能对象类别。  
  
- 默认阻止行为已被修改。 [BizTalk Server 性能调整为使用设置仪表板](../core/using-settings-dashboard-for-biztalk-server-performance-tuning.md)描述了影响阻止行为的不同值。  
  
  根据阻止条件的严重性，将执行以下操作：  
  
- 实现主机实例处理逻辑中的渐进式延迟。 端点管理器 (EPM) 线程从传输适配器接收消息批时和/或 EPM 提交要发布到 MessageBox 数据库中的消息批时，实现该延迟。 处理延迟的持续时间和持续时间递增的速率都随阻止条件的严重性而变化。  
  
- 限制可用于端点管理器 (EPM) 的线程数。 EPM 从适配器接收消息批，并将消息发布到 MessageBox 数据库。 默认情况下，EPM 配置为每 CPU 使用 20 个线程。 如果主机阻止机制检测到入站处理的任务繁忙，则可以暂时减少 EPM 可用的线程数，直到繁忙状况结束。 除非 EPM 线程可用于处理入站消息批，否则，EPM 不能处理来自传输适配器的消息或将消息批传送到 MessageBox 数据库。  
  
- 根据需要减少内存和其他资源的使用。 BizTalk Server 可以将指令发送到其他服务类来限制内存使用，通过冻结正在运行的调度、 缩小内存缓存大小和限制的占用大量内存的线程使用情况。  
  
  **从适配器到 MessageBox 的入站的消息流**  
  
  ![从适配器到 MessageBox 的消息流的入站](../core/media/inboundmsgflow.gif "InboundMsgFlow")  
  
## <a name="outbound-host-throttling"></a>出站主机阻止  
 出站主机阻止，也称为*消息处理阻止*在 BizTalk Server 中，应用于包含业务流程或发送适配器的接收和传送或处理消息，已进行的主机实例发布到 MessageBox。 以下情况可以触发出站主机阻止条件：  
  
- 的内存量、 线程数或主机实例使用的数据库连接数超过中定义了阻止阈值**基于资源的阻止**中**设置仪表板**. 这些值是下可用的性能监视器计数器可测量**biztalk: Message Agent**性能对象类别。  
  
- **消息送达传入速率**主机实例超出**消息送达传出速率**\*指定**加速因子**值. **加速因子**上定义值**基于速率的阻止**选项卡中**设置仪表板**。 消息送达传入速率和传出速率可测量的相应性能监视器计数器下**biztalk: Message Agent**性能对象类别。  
  
- 主机实例同时处理的消息数超过**进程内消息数每个 CPU** \*框上可用的 Cpu 数。 **进程内消息数**上定义的阈值**基于资源的阻止**选项卡中**设置仪表板**。 可以使用测量的主机实例同时处理的消息数**进程内消息计数**下的性能计数器**biztalk: Message Agent**性能对象类别。  
  
- 默认阻止行为已被修改。 [BizTalk Server 性能调整为使用设置仪表板](../core/using-settings-dashboard-for-biztalk-server-performance-tuning.md)描述了影响阻止行为的不同值。  
  
  根据阻止条件的严重性，将执行以下操作：  
  
- 在将消息送达到出站传输适配器或业务流程引擎以便进行消息处理之前，实现主机实例处理逻辑中的渐进式延迟。 处理逻辑延迟的持续时间和持续时间递增的速率都随阻止条件的严重性而变化。  
  
- 限制内存中队列可以保留的消息数。 内存中队列充当临时占位符，用于将消息从 MessageBox 送达到消息代理，消息代理接着将消息送达到 XLANG 和发送适配器。 默认情况下，内存中队列设置为每 CPU 保留 100 个消息。 队列已满时，不会再有消息从 MessageBox 中出列，直到内存中队列得到释放。  
  
- 限制消息代理线程池的大小。 通过限制消息代理线程池的大小，主机阻止机制有效地减少送达到 XLANG 和适配器的消息数。  
  
   可以通过更改修改默认消息代理线程池大小**最大引擎线程**值**常规**选项卡中**设置仪表板**。 有关修改此值的详细信息，请参阅[如何修改常规设置](../core/how-to-modify-general-settings.md)。  
  
- 根据需要减少内存和其他资源的使用。 BizTalk Server 可以向其他服务类别发送指令，通过冻结正在运行的调度、缩小内存缓存大小以及限制使用内存占用量大的线程，来限制内存使用。  
  
  **从 MessageBox 到适配器和 XLANG 的出站消息流**  
  
  ![到适配器和 XLANG 的出站消息流](../core/media/outboundmsgflow.gif "OutboundMsgFlow")  
  
## <a name="see-also"></a>请参阅  
 [BizTalk Server 如何实现主机阻止](../core/how-biztalk-server-implements-host-throttling.md)   
 [使用设置仪表板进行 BizTalk Server 性能调整](../core/using-settings-dashboard-for-biztalk-server-performance-tuning.md)