---
title: 连接系统 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4c4895e5-7272-415f-a0de-905256fa0a43
caps.latest.revision: 16
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a151fb5c6247b8630ab423054adef42e64efd06a
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36995590"
---
# <a name="connecting-systems"></a>连接系统
若要进行集成，必须在不同计算机上的不同软件之间进行有效的消息交换。 考虑到现有通信方式多种多样，BizTalk Server 必须支持各种协议和消息格式。 如后文所述，该引擎的一个重要部分专用于实现此通信。 但请注意，该引擎内部只使用 XML 文档。 不管消息以何种格式到达，在收到消息后都必须将其转换为 XML 文档。 同样，如果文档的收件人无法以 XML 格式接收文档，则引擎会将其转换为目标所需的格式。  
  
## <a name="sending-and-receiving-messages-adapters"></a>发送和接收消息： 适配器  
 BizTalk Server 必须与各种其他软件进行通信，因为它依赖适配器来实现此类。 适配器用于实现某种通信机制，例如特定的协议。 开发人员确定在给定情况下要使用的适配器。 他可能会选择 BizTalk Server 提供，例如，内置适配器之一或使用为诸如 Windows SharePoint Services 之类的常用产品创建的适配器或甚至可以创建自定义适配器。 在上述每一种情况下，适配器都是构建在称为“适配器框架”的标准结构之上的。 此框架为创建和运行适配器提供了常用方法，并且支持用于管理所有适配器类型的相同工具。  
  
 Microsoft BizTalk Server 包含以下本地适配器：  
  
- 文件适配器： 支持读取和写入到文件中的 Windows 文件系统。 由于业务流程中包含的应用程序可能会经常访问本地或网络中的同一文件系统，因此通过文件交换消息可能较为方便。  
  
- FTP 适配器： 支持发送和接收文件传输协议 (FTP) 服务器与 BizTalk Server 之间的信息。  
  
- HTTP 适配器： 支持发送和接收使用 HTTP 的信息。 BizTalk Server 公开一个或多个 Url，以便其他应用程序以将数据发送到它，并且它可以使用此适配器将数据发送到其他 Url。  
  
- MSMQ 适配器： 支持发送和接收消息使用 Microsoft 消息队列 (MSMQ)。  
  
- WebSphere MQ 适配器： 支持发送和接收消息使用 IBM 的 WebSphere MQ （以前称为 MQSeries）。  
  
- POP3 适配器： 支持接收电子邮件及其附件使用邮局协议 (POP3) 的第三版。  
  
- SMTP 适配器： 支持使用 SMTP 发送消息。 使用标准电子邮件地址标识参与方。  
  
- SOAP 适配器： 支持发送和接收 Web 服务请求，以使 BizTalk Server 要连接到 Web 服务。  
  
- WCF 适配器： 支持发送和接收使用 Windows Communication Foundation 的信息。  
  
- Windows SharePoint Services (WSS) 适配器： 支持访问和发布在 Microsoft Windows SharePoint 文档库中存储的文档。  
  
  Microsoft 还提供了用于常用商业软件的适配器，包括：  
  
- 用于 JD Edwards OneWorld 的 Microsoft BizTalk 适配器  
  
- 用于 JD Edwards EnterpriseOne 的 Microsoft BizTalk 适配器  
  
- 用于 PeopleSoft Enterprise 的 Microsoft BizTalk 适配器  
  
- 用于 TIBCO Rendezvous 的 Microsoft BizTalk 适配器  
  
- 用于 TIBCO Enterprise Message Service 的 Microsoft BizTalk 适配器  
  
  有关与这些适配器相关的详细信息，请参阅[BizTalk Server 中的适配器](../core/adapters-in-biztalk-server.md)。  
  
  无论使用哪一种适配器来接收数据，通常都必须对该适配器接收到的消息进行处理，然后业务流程才能访问这些消息。 同样，通常需要对业务流程生成的传出消息进行处理，然后适配器才能发送这些消息。  
  
## <a name="processing-messages-pipelines"></a>处理消息： 管道  
 业务流程中涉及的应用程序通过交换各种文档进行通信： 例如，采购订单和发票。 BizTalk Server 应用程序执行业务流程，它必须能够正确处理包含这些文档的消息。 此处理过程可能包含多个步骤，因此将通过消息管道来执行。 传入消息通过接收管道处理，而传出消息则通过发送管道处理。  
  
 例如，即使越来越多的应用程序已设计为可理解 XML 文档，但目前仍有许多（很可能是大多数）应用程序无法理解 XML 文档。 由于 BizTalk Server 内部只使用 XML 文档，它必须提供一种方法，以其他格式与 XML 之间相互转换。 此外，还可能需要其他服务，例如对消息发送方进行身份验证。 为了以模块化且可自定义的方式处理这些任务和其他任务，将分若干个阶段来构造管道，其中每个阶段均包含一个或多个启用 .NET 的组件或组件对象模型 (COM) 组件。 每个组件处理特定的消息处理部分。 BizTalk Server 提供了几个标准组件，用于解决最常见的情况。 如果这些组件无法满足需要，开发人员也可以为接收管道和发送管道创建自定义组件。  
  
 ![](../core/media/understandingbts-05-pipelinereceive.gif "UnderstandingBTS_05_PipelineReceive")  
  
 上图显示了接收管道中的各个阶段以及为每个阶段提供的标准组件。 这些阶段及其关联组件如下：  
  
- 解码： BizTalk Server 提供了一个标准组件为此阶段，即 MIME/SMIME 解码器。 此组件可以处理 MIME 或 Secure MIME (S/MIME) 格式的消息以及消息中包含的任何附件。 该组件可将这两种类型的消息转换为 XML，还可以对 S/MIME 消息进行解密并验证其数字签名。  
  
- 反汇编： 提供了三个标准组件。 平面文件拆装器组件可将平面文件转换为 XML 文档。 这些文件可以是位置文件，其中每条记录的长度和结构相同；也可以是分隔文件，这些文件使用指定字符来分隔文件中的记录。 第二个标准组件为 XML 拆装器，用于解析已使用 XML 进行说明的传入消息。 第三个标准组件为 BizTalk 框架拆装器，该组件如今已不常使用。 该组件使用 BizTalk 框架定义的可靠消息传送机制来接受所发送的消息， BizTalk 框架是在 BizTalk Server 2000 中实现的 。  
  
- 验证： 则 BizTalk Server 提供为此阶段的 XML 验证器组件。 顾名思义，此组件可根据指定的架构或架构组对拆装阶段生成的 XML 文档进行验证，如果文档与任一架构不符，则返回错误。  
  
- 解析参与方： 此阶段，参与方解析的唯一标准组件尝试确定此消息的发件人的标识。 如果已对消息进行数字签名，签名用于查找 BizTalk Server 中的管理数据库中的 Windows 标识。 （正如稍后部分中将介绍的一样，BizTalk Server 的管理工具也使用此数据库。）如果消息包含 Windows 用户的已验证安全标识符 (SID)，则使用此标识。 如果这两种机制都无法成功，则为消息发送方分配默认的匿名标识。  
  
  ![](../core/media/understandingbts-06-pipelinesend.gif "UnderstandingBTS_06_PipelineSend")  
  
  按照所使用的发送管道的定义，传出消息可能也要经历多个阶段。 上图显示了发送管道的各个阶段和标准组件。 它们分别是：  
  
- 预组装： 不提供了任何标准组件。 不过，可以根据需要在此处插入自定义组件。  
  
- 组装： 并行中的接收管道的拆装阶段，此阶段还具有三个标准组件。 平面文件组装器将 XML 消息转换为位置平面文件或分隔平面文件，XML 组装器则支持向传出 XML 消息添加信封以及对其进行其他更改。 第三个组件为 BizTalk 框架组装器，它使用 BizTalk 框架消息传送技术将消息打包以便进行可靠传输。  
  
- 进行编码： BizTalk Server 定义了一个标准组件为此阶段，即 MIME/SMIME 编码器。 此组件以 MIME 或 S/MIME 格式打包传出消息。 如果使用 S/MIME，则还可以对消息进行数字签名和/或加密。  
  
  BizTalk Server 定义了一些默认管道，其中包括可用于处理已经以 XML 表示的消息的简单接收/发送对。 开发人员还可以使用管道设计器来创建自定义管道。 运行在 [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] 内的此工具提供了一个图形界面，使用该界面，开发人员可以使用任何所需的操作来拖放组件以创建管道。  
  
## <a name="choosing-messages-subscriptions"></a>选择消息： 订阅  
 在消息已通过适配器和接收管道进行传递后，下一步是确定该消息要传递到的目标。 一条消息通常以业务流程中，目标但还可以直接转到发送管道，从而将 BizTalk Server 要用作纯粹的消息传送系统的消息。 无论在哪种情况下，均使用订阅来实现消息与其目标的匹配。  
  
 接收管道对消息进行处理后，将创建包含消息的各种属性的消息上下文。 业务流程或发送管道可以根据这些属性的值来订阅消息。 例如，业务流程可能会创建与类型"发票"的所有消息或从 QwickBank 公司接收到"发票"类型的所有消息或从 QwickBank 公司接收到"发票"类型的所有消息匹配的订阅是用于超过 10,000 美元。 但指定了它，则订阅其订阅服务器中返回与订阅定义的条件匹配的那些消息。 接收到的消息可以通过实例化某些业务流程来启动业务流程，也可以激活正在运行的业务流程中的其他步骤。 同样，当业务流程发送消息时，会根据发送管道已建立的订阅将消息与发送管道进行匹配。  
  
-   在 BizTalk Server 中，也很有可能订阅特定错误条件。 错误消息可以按特定方式进行处理，也可以路由到特定目标，例如 Windows SharePoint Services 文件夹。  
  
## <a name="see-also"></a>请参阅  
 [BizTalk Server 消息引擎](../core/the-biztalk-server-messaging-engine.md)   
 [发布和订阅体系结构](../core/publish-and-subscribe-architecture.md)   
 [适配器](../core/adapters.md)   
 [管道](../core/pipelines.md)