---
title: "WCF 适配器属性架构和属性 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2093745e-86c0-4276-a7cc-a0187391ca4a
caps.latest.revision: "19"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 1fb5eaf23072ed1f3089b3838ee90b679fea4323
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="wcf-adapters-property-schema-and-properties"></a>WCF 适配器属性架构和属性
下表包含 WCF 适配器属性架构中的升级属性。 WCF 适配器对应用程序中可使用的属性进行赋值。 WCF 适配器还提供了一种用于将自定义属性写入 BizTalk 消息上下文但不进行升级的机制，以及一种用于将自定义属性升级到 BizTalk 消息上下文的机制。 有关更多详细信息，请参阅[发布 WCF 服务使用的 SOAP 标头](../core/soap-headers-with-published-wcf-services.md)。  

## <a name="promoted-properties"></a>提升的属性  
 **Namespace:** http://schemas.microsoft.com/BizTalk/2006/01/Adapters/WCF-properties  
  
|Name|类型|Description|适用的 WCF 适配器|  
|----------|----------|-----------------|----------------------------|  
|**操作**|字符串|指定**SOAPAction**传出消息的标头字段。 你可以通过两种方式指定此值： 单个操作格式和操作映射格式。 如果将此属性设置中的单个操作格式-例如，http://contoso.com/Svc/Op1- **SOAPAction**标头为传出消息始终设置为此属性中指定的值。<br /><br /> 如果在操作映射格式，传出中设置此属性**SOAPAction**标头由**BTS。操作**上下文属性。 例如，如果此属性设置为以下 XML 格式和**BTS。操作**属性设置为 Op1，为传出的 WCF 发送适配器使用 http://contoso.com/Svc/Op1 **SOAPAction**标头。<br /><br /> \<BtsActionMapping ><br /><br /> \<操作名称 ="Op1"操作 ="http://contoso.com/Svc/Op1"/ ><br /><br /> \<操作名称 ="Op2"操作 ="http://contoso.com/Svc/Op2"/ ><br /><br /> \</ BtsActionMapping ><br /><br /> 如果传出消息来自的业务流程端口时，动态设置业务流程实例**BTS。操作**与操作名称的端口的属性。 如果使用基于内容的路由路由传出消息，则可以设置**BTS。操作**管道组件中的属性。<br /><br /> 此属性将自动从传入消息以单一操作格式进行升级。<br /><br /> 默认值为空字符串。|所有 WCF 发送适配器|  
|**AffiliateApplicationName**|字符串|指定用于企业单一登录 (SSO) 的关联应用程序。 此属性是必需的如果**UseSSO**属性设置为**True**。<br /><br /> 默认值为空字符串。|除 WCF-NetNamedPipe 适配器外的所有 WCF 发送适配器|  
|**AlgorithmSuite**|字符串|指定消息加密和密钥包装算法。 这些算法与“安全策略语言”(WS-SecurityPolicy) 规范中指定的算法一致。<br /><br /> 默认值： **Basic256**<br /><br /> 有关详细信息有关的适用值**AlgorithmSuite**属性，请参阅**算法套件**中的属性**Wcf-nettcp 传输属性对话框中，发送，安全**选项卡[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。|WCF BasicHttp 适配器<br /><br /> WCF-NetMsmq 适配器<br /><br /> WCF-NetTcp 适配器<br /><br /> WCF-WSHttp 适配器|  
|**BindingConfiguration**|字符串|指定使用的 XML 字符串**\<绑定 >**元素来配置不同类型的预定义的绑定所提供的 Windows Communication Foundation (WCF)。 有关系统提供的绑定和自定义绑定的详细信息，请参阅“另请参见”部分中的相应主题。<br /><br /> 默认值为空字符串。<br /><br /> 例如：<br /><br /> \<绑定名称 ="wsHttpBinding"transactionFlow ="true">\<安全 >\<消息 clientCredentialType ="UserName"/ >\</安全 >\<绑定 >|WCF 自定义适配器<br /><br /> WCF CustomIsolated 适配器|  
|**BindingType**|字符串|指定要用于终结点的绑定类型。<br /><br /> 默认值为空字符串。<br /><br /> 有关详细信息有关的适用值**BindingType**属性，请参阅**绑定类型**中的属性**WCF 自定义传输属性对话框中，发送，绑定**选项卡[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。|WCF 自定义适配器<br /><br /> WCF CustomIsolated 适配器|  
|**ClientCertificate**|字符串|指定用于向服务验证此发送端口的 X.509 证书的指纹。 此属性是必需的如果**ClientCredentialsType**属性设置为**证书**。 此属性使用的证书必须安装到**我**将存储在**当前用户**位置。<br /><br /> 默认值为空字符串。|WCF-BasicHttp 发送适配器<br /><br /> WCF-WSHttp 发送适配器<br /><br /> WCF NetTcp 发送适配器<br /><br /> WCF NetMsmq 发送适配器|  
|**CloseTimeout**|字符串|指定一个时间跨度值来表示为完成信道关闭操作提供的时间间隔。<br /><br /> 默认值：00:01:00|所有 WCF 适配器除 WCF 自定义和 WCF CustomIsolated 适配器|  
|**CustomDeadLetterQueue**|字符串|指定完全限定的 URI 与**net.msmq**方案的每个应用程序死信队列，消息已过期或者传输或传递失败的存放位置。 例如 net.msmq://localhost/deadLetterQueueName。 死信队列是发送应用程序的队列管理器上的一种队列，用于未能送达的到期的消息。 此属性是必需的如果**DeadLetterQueue**属性设置为**自定义**。<br /><br /> 默认值为空字符串。|WCF NetMsmq 发送适配器|  
|**DeadLetterQueue**|字符串|指定死信队列，未能传输到应用程序的消息将传输到死信队列中。 有关传递到死信队列的消息的详细信息，请参阅**WCF NetMsmq 传输属性对话框中，发送，绑定**选项卡[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。<br /><br /> 默认值：**系统**|WCF NetMsmq 发送适配器|  
|**DisableLocationOnFailure**|Boolean|指定是否禁用由于接收管道故障或路由故障而导致入站处理失败的接收位置。<br /><br /> 你可能想要将此属性设置为**True**时接收位置可以被禁用，而且拒绝服务 (DoS) 并不是问题。<br /><br /> 例如：<br /><br /> WCF 的自定义适配器。 当**BindingType**属性设置为**netMsmqBinding**。<br />WCF 的自定义适配器。 当**BindingType**属性设置为**customBinding**，和**BindingConfiguration**属性配置为使用依赖于排队传输的自定义通道如 MSMQ。<br />-WCF CustomIsolated 适配器。 当**BindingType**属性设置为**customBinding**，和**BindingConfiguration**属性配置为使用依赖于排队传输的自定义通道如 MSMQ。<br />-WCF NetMsmq 适配器。<br /><br /> 默认值： **False**|WCF NetMsmq 接收适配器<br /><br /> WCF 自定义接收适配器<br /><br /> WCF-CustomIsolated 接收适配器|  
|**EnableTransaction**|Boolean|此属性的效果依 WCF 适配器的不同而变化。 有关此属性的详细信息，请参阅操作指南主题中的每个 WCF 适配器[WCF 适配器](../core/wcf-adapters.md)。|WCF-WSHttp 适配器<br /><br /> WCF-NetTcp 适配器<br /><br /> WCF NetNamedPipe 适配器<br /><br /> WCF-NetMsmq 适配器|  
|**EndpointBehaviorConfiguration**|字符串|指定使用的 XML 字符串**\<行为 >**元素 **\<endpointBehaviors >**元素来配置 WCF 终结点的行为设置。 有关详细信息 **\<endpointBehaviors >**元素，请参阅另请参阅中的相应主题。<br /><br /> 默认值为空字符串。<br /><br /> 例如：<br /><br /> \<行为名称 ="sampleBehavior">\<callbackTimeouts / >\</behavior >|WCF 自定义发送适配器|  
|**EstablishSecurityContext**|Boolean|指定安全通道是否建立安全会话。 安全会话在交换应用程序消息之前建立安全上下文标记 (SCT)。<br /><br /> 默认值： **True**|WCF-WSHttp 适配器|  
|**开始地址**|字符串|指示发送传入 WCF 消息的源终结点地址。 该属性将自动提升从传入消息。|除 WCF-NetMsmq 发送适配器外的所有 WCF 适配器|  
|**标头**|字符串|指定用于提供除 URI 外的其他寻址信息的终结点引用。 当使用此属性时，此属性必须具有\<**标头**> 元素作为根元素。 所有地址标头必须放置在\<**标头**> 元素。 该属性自动从传入消息进行升级。<br /><br /> 例如：<br /><br /> \<标头 >\<区域 xmlns ="Uri">"String"\<国家/地区 >\<成员 xmlns ="Uri">"String"\</Member > \</headers >|所有 WCF 适配器|  
|**标识**|字符串|指定接收位置提供或发送端口预期的服务的标识。 可以为指定的值**标识**属性而异的安全配置。 这些设置使客户端能够对服务进行身份验证。 在客户端与服务进行握手的过程中，Windows Communication Foundation (WCF) 基础结构将确保服务的标识与客户端的值保持一致。<br /><br /> 默认值为空字符串。<br /><br /> 例如：<br /><br /> \<标识 ><br /><br /> \<userPrincipalName 值 ="username@contoso.com"/ ><br /><br /> \</identity >|所有 WCF 适配器|  
|**InboundBodyLocation**|字符串|指定 SOAP 数据选择**正文**传入 WCF 消息的元素。 有关如何使用**InboundBodyLocation**属性，请参阅[为 WCF 适配器指定消息正文](../core/specifying-the-message-body-for-the-wcf-adapters.md)。<br /><br /> 默认值： **UseBodyElement**<br /><br /> 适用值包括：<br /><br /> -   **UseBodyElement** -使用 SOAP 的内容**正文**传入消息创建 BizTalk 消息正文部分的元素。 如果 **Body** 元素具有多个子元素，则只有第一个元素将成为 BizTalk 消息正文部分。<br />-   **UseEnvelope** -从整个 SOAP 创建 BizTalk 消息正文部分**信封**传入消息。<br />-   **UseBodyPath** -使用中的正文路径表达式**InboundBodyPathExpression**属性创建 BizTalk 消息正文部分。 针对传入消息的 SOAP **Body** 元素的直接子元素计算正文路径表达式。 此属性仅对要求-响应端口有效。|除 WCF-NetMsmq 发送适配器外的所有 WCF 适配器|  
|**InboundBodyPathExpression**|字符串|指定正文路径表达式以标识传入消息中用于创建 BizTalk 消息正文部分的特定部分。 此正文路径表达式针对 SOAP 的即时子元素进行评估**正文**传入消息的节点。 如果此正文路径表达式返回多个节点，则只选择第一个节点作为 BizTalk 消息正文部分。 此属性是必需的如果**InboundBodyLocation**属性设置为**UseBodyPath**。 有关如何使用**InboundBodyPathExpression**属性，请参阅[WCF 适配器属性架构和属性](../core/wcf-adapters-property-schema-and-properties.md)。<br /><br /> 默认值为空字符串。|除 WCF-NetMsmq 发送适配器外的所有 WCF 适配器|  
|**InboundHeaders**|字符串|使用**InboundHeaders**属性访问传入的 WCF 消息的 SOAP 标头。 WCF 适配器将入站消息中的所有 SOAP 标头值复制到此属性，其中包括 WCF 基础结构用于诸如 WS-Addressing、WS-Security 和 WS-AtomicTransaction 的自定义 SOAP 标头和标准 SOAP 标头。 上下文属性中包含的值是一个包含与 XML 数据字符串\<**标头**> 作为子元素的复制根元素，并传入的 SOAP 标头\<**标头**> 元素。 有关如何对访问 SOAP 标头与 WCF 适配器的详细信息，请参阅 SDK 示例中，使用自定义 SOAP 标头与 WCF 适配器中，从[http://go.microsoft.com/fwlink/?LinkId=79960](http://go.microsoft.com/fwlink/?LinkId=79960)。|除 WCF-NetMsmq 发送适配器外的所有 WCF 适配器|  
|**InboundNodeEncoding**|字符串|指定的编码 WCF 接收适配器使用要解码识别由正文路径表达式中指定的节点类型**InboundBodyPathExpression**。 此属性是必需的如果**InboundBodyLocation**属性设置为**UseBodyPath**。<br /><br /> 默认值： **XML**<br /><br /> 适用值包括：<br /><br /> -   **Base64** -Base64 编码。<br />-   **十六进制**-十六进制编码。<br />-   **字符串**编码文本的 utf-8。<br />-   **XML** -WCF 适配器使用由正文路径表达式中所选节点的外部 XML 创建 BizTalk 消息正文**InboundBodyPathExpression**。|除 WCF-NetMsmq 发送适配器外的所有 WCF 适配器|  
|**IsFault**|Boolean|指示是否接收 SOAP 错误消息。 该属性将自动提升从传入消息。 **注意：** **IsFault**属性不能用于检查收到的消息，例如 HTTP 404 （文件或找不到目录） 错误的传输错误。|除 WCF-NetMsmq 发送适配器外的所有 WCF 适配器|  
|**LeaseTimeout**|字符串|指定活动的池连接的最大生存期。 指定的时间过后，则连接将关闭后当前的请求已得到处理。<br /><br /> WCF NetTcp 适配器利用[NetTcpBinding](http://go.microsoft.com/fwlink/?LinkId=81087)类与终结点进行通信。 使用时[NetTcpBinding](http://go.microsoft.com/fwlink/?LinkId=81087)在负载平衡方案中，请考虑减少的默认租约超时值。有关负载平衡时使用的详细信息[NetTcpBinding](http://go.microsoft.com/fwlink/?LinkId=81087)，请参阅另请参阅中的相应主题。<br /><br /> 默认值：00:05:00|WCF-NetTcp 接收适配器|  
|**MaxConcurrentCalls**|Integer|指定针对单个服务实例的并发调用的数目。 超出此限制的调用将在队列中排队。 将该值设置为 0 等效于将它设置为 **Int32.MaxValue**。 **注意：**此属性在使用跟踪配置文件不能在 BAM 主导入数据库中进行跟踪。 <br /><br /> 默认值：200|除 WCF-Custom 和 WCF-CustomIsolated 适配器外的所有 WCF 接收适配器|  
|**MaxConnections**|Integer|指定监听程序可以拥有的等待应用程序接受的最大连接数。 在超过此配额值时，将删除新的传入连接，而不是等待接受这些连接。 **注意：**因为这是一个适配器处理程序属性，将管道组件和业务流程中它们配置此属性。 **注意：**此属性在使用跟踪配置文件不能在 BAM 主导入数据库中进行跟踪。 <br /><br /> 默认值为 10。|WCF NetNamedPipe 适配器<br /><br /> WCF-NetTcp 适配器|  
|**MaxReceivedMessageSize**|Integer|指定网络上可接收的消息的最大大小（包括标头），以字节为单位。 消息的大小受为每条消息分配的内存量的限制。 你可以使用此属性来降低受拒绝服务 (DoS) 攻击的可能性。<br /><br /> 默认值：65536|WCF BasicHttp 适配器<br /><br /> WCF-WSHttp 适配器<br /><br /> WCF-NetTcp 适配器<br /><br /> WCF NetNamedPipe 适配器<br /><br /> WCF NetMsmq 接收适配器|  
|**MessageClientCredentialType**|字符串|指定使用基于消息的安全性对客户端执行验证时所用的凭据类型。<br /><br /> 适用值因每个 WCF 适配器的不同而异。 有关详细信息**MessageClientCredentialType**属性，请参阅操作指南主题中的每个 WCF 适配器[WCF 适配器](../core/wcf-adapters.md)。|WCF BasicHttp 适配器<br /><br /> WCF-WSHttp 适配器<br /><br /> WCF-NetTcp 适配器<br /><br /> WCF NetNamedPipe 适配器|  
|**MessageEncoding**|字符串|指定用于对 SOAP 消息进行编码的编码器。<br /><br /> 默认值： 文本<br /><br /> 适用值包括：<br /><br /> -   **文本**-使用文本消息编码器。<br />-   **Mtom** -使用消息传输组织机制 1.0 (MTOM) 编码器。|WCF BasicHttp 适配器<br /><br /> WCF-WSHttp 适配器|  
|**MsmqAuthenticationMode**|字符串|指定如何通过 MSMQ 传输对消息进行验证。<br /><br /> 默认值： **WindowsDomain**<br /><br /> 有关详细信息有关的适用值**MsmqAuthenticationMode**属性，请参阅**MSMQ 身份验证模式**中的属性**WCF NetMsmq 传输属性对话框框中，发送，安全**选项卡[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。|WCF-NetMsmq 适配器|  
|**MsmqEncryptionAlgorithm**|字符串|指定在消息队列管理器之间传输消息时，将在网络上使用的消息加密算法。 此属性才可用才**而 MsmqProtectionLevel**属性设置为**EncryptAndSign**。<br /><br /> 默认值： **RC4Stream**<br /><br /> 适用值包括：<br /><br /> -   **RC4Stream**<br />-   **AES**|WCF-NetMsmq 适配器|  
|**而 MsmqProtectionLevel**|字符串|指定消息在 MSMQ 传输一级的保护方式。<br /><br /> 默认值：**登录**<br /><br /> 适用值包括：<br /><br /> -   **无**： 无保护。<br />-   **登录**： 对消息进行签名。<br />-   **EncryptAndSign**： 消息进行加密和签名。 若要使用此保护级别，必须启用**Active Directory 集成**为**MSMQ**。|WCF-NetMsmq 适配器|  
|**MsmqSecureHashAlgorithm**|字符串|指定使用哈希算法计算消息摘要。 此属性不可用如果**而 MsmqProtectionLevel**属性设置为**无**。<br /><br /> 默认值： **SHA1**<br /><br /> 适用值包括：<br /><br /> -   **MD5**<br />-   **SHA1**<br />-   **SHA25**<br />-   **SHA512**|WCF-NetMsmq 适配器|  
|**NegotiateServiceCredential**|Boolean|指定是在带外客户端提供服务凭据，还是通过协商过程从服务将服务凭据提供给客户端。 这种协商是正常消息交换开始前的准备过程。<br /><br /> 如果**MessageClientCredentialType**属性等于**无**，**用户名**，或**证书**，此属性设置为**False**意味着服务证书位于带外客户端和客户端需要指定服务证书。 此模式可与实现 WS-Trust 和 WS-SecureConversation 的 SOAP 堆栈交互操作。<br /><br /> 如果**MessageClientCredentialType**属性设置为**Windows**，此属性设置为**False**指定基于 Kerberos 的身份验证。 这意味着客户端和服务必须属于同一个 Kerberos 域。 此模式可与实现 Kerberos 标记配置文件（在 OASIS WSS TC 中定义）以及 WS-Trust 和 WS-SecureConversation 的 SOAP 堆栈交互操作。<br /><br /> 当此属性是**True**，会引起通过 SOAP 消息隧道 SPNego 交换的.NET SOAP 协商。<br /><br /> 默认值： **True**|WCF-WSHttp 适配器|  
|**OpenTimeout**|字符串|指定一个时间跨度值来表示为完成信道打开操作提供的时间间隔。 **注意：**此属性在使用跟踪配置文件不能在 BAM 主导入数据库中进行跟踪。 <br /><br /> 默认值：00:01:00|除 WCF-Custom 和 WCF-CustomIsolated 适配器外的所有 WCF 适配器|  
|**OrderedProcessing**|字符串|指定是否按顺序处理消息。 当选中此属性时，此接收位置与拥有的 BizTalk 消息传递或业务流程发送端口结合使用时的有序的消息传递**按序送达**选项设置为`True`。 有关详细信息**按序送达**选项，请参阅另请参阅中的相应主题。<br /><br /> 此属性适用于以下情况：<br /><br /> WCF 的自定义适配器。 当**BindingType**属性设置为**netMsmqBinding**。<br />WCF 的自定义适配器。 当**BindingType**属性设置为**customBinding**，和**BindingConfiguration**属性配置为使用依赖于传输的自定义通道支持如 MSMQ 的有序的传递。<br />-WCF CustomIsolated 适配器。 当**BindingType**属性设置为**customBinding**，和**BindingConfiguration**属性配置为使用依赖于传输的自定义通道支持有序的传递。<br />-WCF NetMsmq 适配器。<br /><br /> 默认值： **False**|WCF NetMsmq 接收适配器<br /><br /> WCF 自定义接收适配器<br /><br /> WCF-CustomIsolated 接收适配器|  
|**OutboundBodyLocation**|字符串|指定 SOAP 数据选择**正文**传出的 WCF 消息的元素。 有关如何使用**OutboundBodyLocation**属性，请参阅[为 WCF 适配器指定消息正文](../core/specifying-the-message-body-for-the-wcf-adapters.md)。<br /><br /> 默认值： **UseBodyElement**<br /><br /> 适用值包括：<br /><br /> -   **UseBodyElement** -BizTalk 消息正文部分用于创建的 SOAP 内容**正文**传出消息的元素。<br />-   **UseTemplate** -使用中提供的模板**OutboundXMLTemplate**属性来创建的内容 SOAP**正文**传出消息的元素。|除 WCF-NetMsmq 接收适配器外的所有 WCF 适配器|  
|**OutboundCustomHeaders**|字符串|指定传出消息的自定义 SOAP 标头。 当使用此属性时，该属性必须具有\<**标头**> 元素作为根元素。 所有自定义 SOAP 标头必须放置在\<**标头**> 元素。 如果自定义 SOAP 标头的值为空字符串，则必须分配\<**标头**>\</**标头**> 或\< **标头**/ > 此属性。 有关如何使用 WCF 适配器使用 SOAP 标头的详细信息，请参阅 SDK 示例中，使用自定义 SOAP 标头与 WCF 适配器中，从[http://go.microsoft.com/fwlink/?LinkId=79960](http://go.microsoft.com/fwlink/?LinkId=79960)|除 WCF-NetMsmq 接收适配器外的所有 WCF 适配器|  
|**OutboundXmlTemplate**|字符串|指定的 SOAP 内容的 XML 格式模板**正文**的传出消息的元素。 此属性是必需的如果**OutboundBodyLocation**属性设置为**UseTemplate**。 有关如何使用**OutboundXMLTemplate**属性，请参阅[为 WCF 适配器指定消息正文](../core/specifying-the-message-body-for-the-wcf-adapters.md)。<br /><br /> 默认值为空字符串。|除 WCF-NetMsmq 接收适配器外的所有 WCF 适配器|  
|**密码**|字符串|指定要用于目标服务器的身份验证的密码时**UseSSO**属性设置为**False**。<br /><br /> 默认值为空字符串。|除 WCF-NetNamedPipe 适配器外的所有 WCF 发送适配器|  
|**PropagateFaultMessage**|Boolean|指定是否路由或挂起出站处理中失败的消息。<br /><br /> 此属性仅对要求-响应端口有效。 **注意：**此属性在使用跟踪配置文件不能在 BAM 主导入数据库中进行跟踪。 <br /><br /> 默认值： **True**<br /><br /> 适用值包括：<br /><br /> -   **True** -失败对订阅应用程序的出站处理将消息路由 （如另一个接收端口或业务流程计划）。<br />-   **False** -挂起失败的消息并生成否定确认 (NACK)。|除 WCF-NetMsmq 适配器外的所有 WCF 发送适配器|  
|**ProxyAddress**|字符串|指定代理服务器的地址。 使用**https**或**http**根据安全配置的方案。 此地址后面可跟冒号和端口号。 该属性是必需的如果**ProxyToUse**属性设置为**UserSpecified**。<br /><br /> 例如，http://127.0.0.1:8080<br /><br /> 默认值为空字符串。|WCF-BasicHttp 发送适配器<br /><br /> WCF-WSHttp 发送适配器|  
|**代理**|字符串|指定要用于中指定的代理服务器密码**ProxyAddress**属性。<br /><br /> 默认值为空字符串。|WCF-BasicHttp 发送适配器<br /><br /> WCF-WSHttp 发送适配器|  
|**ProxyToUse**|字符串|指定要用于传出 HTTP 通信的代理服务器。<br /><br /> 默认值：**无**<br /><br /> 适用值包括：<br /><br /> -   **无**-为此发送端口不使用代理服务器。<br />-   **默认**-承载此发送端口的发送处理程序中使用的代理设置。<br />-   **UserSpecified** -使用中指定的代理服务器**ProxyAddress**属性。|WCF-BasicHttp 发送适配器<br /><br /> WCF-WSHttp 发送适配器|  
|**ProxyUserName**|字符串|指定要用于代理服务器中指定的用户名称**ProxyAddress**属性。 该属性是必需的如果**ProxyToUse**属性设置为**UserSpecified**。<br /><br /> 有关此属性的详细信息，请参阅[如何配置 WCF WSHttp 发送端口](../core/how-to-configure-a-wcf-wshttp-send-port.md)和[如何配置 WCF BasicHttp 发送端口](http://msdn.microsoft.com/library/acdb50fa-57fe-4657-9561-b6b2f4919c7f)。|WCF-BasicHttp 发送适配器<br /><br /> WCF-WSHttp 发送适配器|  
|**ReplyToAddress**|字符串|指示与通过请求响应接收位置接收的传入消息相对应的传出 WCF 消息的回复终结点地址。 该属性将自动提升从传入消息。<br /><br /> 默认值为空字符串。|除 WCF-NetMsmq 适配器外的所有 WCF 适配器|  
|**SecurityMode**|字符串|指定使用的安全类型。<br /><br /> 适用值因每个 WCF 适配器的不同而异。 有关详细信息**SecurityMode**属性，请参阅操作指南主题中的每个 WCF 适配器[WCF 适配器](../core/wcf-adapters.md)。 **注意：**此属性在使用跟踪配置文件不能在 BAM 主导入数据库中进行跟踪。|除 WCF-Custom 和 WCF-CustomIsolated 适配器外的所有 WCF 适配器|  
|**SendTimeout**|字符串|指定一个时间跨度值来表示为完成发送操作提供的时间间隔。 此值指定完成整个交互的时间跨度（即使响应方返回一条大消息）。<br /><br /> 默认值：00:01:00|除 WCF-Custom 和 WCF-CustomIsolated 适配器外的所有 WCF 适配器|  
|**ServiceBehaviorConfiguration**|字符串|指定使用的 XML 字符串**\<行为 >**元素 **\<serviceBehaviors >**元素来配置 WCF 服务的行为设置。 有关详细信息 **\<serviceBehaviors >**元素，请参阅另请参阅中的相应主题。<br /><br /> 默认值为空字符串。<br /><br /> 例如：<br /><br /> \<行为名称 ="SampleServiceBehavior">\<serviceAuthorization principalPermissionMode ="UseAspNetRoles"/ >\<serviceCredentials >\<serviceCertificate findValue ="539d9ab3089bb6dc187fa7dbb382cf01f8d78f5f"storeLocation ="CurrentUser"x509FindType ="FindByThumbprint"/ >\</serviceCredentials >\<serviceMetadata httpGetEnabled ="true"/ >\</behavior>|WCF 自定义接收适配器<br /><br /> WCF CustomIsolated 适配器|  
|**ServiceCertificate**|字符串|如果此属性用于接收位置，则为接收位置指定 X.509 证书的指纹，客户端利用该指纹验证服务。 此属性使用的证书必须安装到**我**将存储在**当前用户**位置。<br /><br /> 如果此属性用于发送端口，请指定 X.509 证书的指纹，用于验证此发送端口将消息发送到的服务。 此属性使用的证书必须安装到**其他人**将存储在**本地计算机**位置。<br /><br /> 默认值为空字符串。|WCF BasicHttp 适配器<br /><br /> WCF-NetMsmq 适配器<br /><br /> WCF-WSHttp 适配器<br /><br /> WCF-NetTcp 接收适配器|  
|**SuspendMessageOnFailure**|Boolean|指定是否将由于接收管道故障或路由故障而导致入站处理失败的请求消息挂起。<br /><br /> 默认值： **True**|所有 WCF 接收适配器|  
|**TextEncoding**|字符串|指定的字符集编码要用于在绑定上发出消息时**MessageEncoding**属性设置为**文本**。 **注意：**此属性在使用跟踪配置文件不能在 BAM 主导入数据库中进行跟踪。 <br /><br /> 默认值： **utf-8**<br /><br /> 适用值包括：<br /><br /> -   **unicodeFFF** -Unicode BigEndian 编码。<br />-   **utf-16** -16 位编码。<br />-   **utf-8** -8 位编码。|WCF BasicHttp 适配器<br /><br /> WCF-WSHttp 适配器|  
|**TimeToLive**|字符串|指定一个时间范围，在此范围内消息有效，一旦超出此范围，消息将到期并被置于死信队列。 设置此属性是为了确保时间敏感消息在被发送端口处理前不会变得陈旧。 队列中在指定的时间间隔内未由此发送端口使用的消息将被认为到期。 到期的消息将发送到称为死信队列的特殊队列。 死信队列的位置设置**DeadLetterQueue**属性。<br /><br /> 默认值： 1.00:00:00|WCF NetMsmq 发送适配器|  
|**若要**|字符串|为 WCF 发送端口发送的传出 WCF 消息指定目标终结点地址。<br /><br /> 默认值为空字符串。|所有 WCF 发送适配器|  
|**TransactionProtocol**|字符串|指定要与此绑定一起使用的事务协议。 此属性是必需的如果**EnableTransaction**属性设置为**True**。<br /><br /> 默认值： **OleTransaction**<br /><br /> 适用值包括：<br /><br /> -   **OleTransaction**<br />-   **Ws-atomictransaction**|WCF NetNamedPipe 适配器<br /><br /> WCF-NetTcp 适配器|  
|**TransportClientCredentialType**|字符串|指定执行发送端口验证时使用的凭据类型。<br /><br /> 适用值因每个 WCF 适配器的不同而异。 有关详细信息**TransportClientCredentialType**属性，请参阅操作指南主题中的每个 WCF 适配器[WCF 适配器](../core/wcf-adapters.md)。|WCF-Basic 适配器<br /><br /> WCF-NetTcp 适配器<br /><br /> WCF-WSHttp 适配器|  
|**TransportProtectionLevel**|字符串|指定 TCP 传输级别的安全性。 消息签名降低了在消息传输过程中第三方对消息进行篡改的风险。 加密为传输过程提供了数据级保密功能。<br /><br /> 默认值： **EncryptAndSign**<br /><br /> 适用值包括：<br /><br /> -   **无**-无保护。<br />-   **登录**-消息进行签名。<br />-   **EncryptAndSign** -消息进行加密和签名。|WCF-NetTcp 适配器<br /><br /> WCF NetNamedPipe 适配器|  
|**UserName**|字符串|指定要用于目标服务器的身份验证的用户名称时**UseSSO**属性设置为**False**。 不必采用“域\用户”格式设置此属性。<br /><br /> 默认值为空字符串。|除 WCF-NetNamedPipe 适配器外的所有 WCF 发送适配器|  
|**UseSourceJournal**|Boolean|指定是否应将此发送端口所处理的消息副本存储到源日记队列中。<br /><br /> 默认值： **False**|WCF NetMsmq 发送适配器|  
|**UseSSO**|Boolean|指定是否使用单一登录检索客户端凭据，以便在目标服务器上进行验证。 **注意：**此属性在使用跟踪配置文件不能在 BAM 主导入数据库中进行跟踪。 <br /><br /> 默认值： **False**|除 WCF-NetNamedPipe 适配器外的所有 WCF 发送适配器|  
|**ReferencedBindings**|字符串|指定引用的绑定配置**bindingConfiguration**属性**\<颁发者 >**元素**wsFederationHttpBinding**和**customBinding**，表示安全令牌服务 (STS) 颁发安全令牌。 有关详细信息**\<颁发者 >**元素，请参阅主题中，"\<颁发者 >"在[http://go.microsoft.com/fwlink/?LinkId=83476](http://go.microsoft.com/fwlink/?LinkId=83476)。<br /><br /> 绑定信息包括**\<颁发者 >**元素**wsFederationHttpBinding**和**customBinding**可通过配置**BindingConfiguration**的 WCF 自定义和 WCF CustomIsolated 适配器的属性。 此属性的引用的绑定配置的所有必须置于窗体的[\<绑定 >](http://go.microsoft.com/fwlink/?LinkID=80878)元素。 **注意：** **bindingConfiguration**属性**\<颁发者 >**元素必须引用此属性中的一个有效的绑定名称。 **注意：** **\<颁发者 >**如果此引用链不会进行一个循环依赖关系中的引用的绑定配置元素还可以引用到此属性中的不同绑定配置. <br /><br /> 默认值为空字符串。<br /><br /> 例如：<br /><br /> WCF。BindingConfiguration = @"\<wsFederationHttpBinding ><br /><br /> \<绑定名称 =""sampleBinding""><br /><br /> \<安全模式 =""消息""><br /><br /> \<消息 issuedKeyType =""AsymmetricKey""><br /><br /> \<颁发者地址 =""http://www.contoso.com/samplests""绑定 =""wsFederationHttpBinding""bindingConfiguration =""**contosoSTSBinding**""/ ><br /><br /> \</ 消息 ><br /><br /> \</ 安全 ><br /><br /> \<绑定 ><br /><br /> \</wsFederationHttpBinding >";<br /><br /> WCF。ReferencedBinding = @"\<绑定 ><br /><br /> \<wsFederationHttpBinding ><br /><br /> \<绑定名称 =""**contosoSTSBinding**""><br /><br /> \<安全模式 =""消息""><br /><br /> \<消息 negotiateServiceCredential =""false""><br /><br /> \<颁发者地址 =""http://northwind.com/samplests""bindingConfiguration =""**northwindBinding**""绑定 =""wsHttpBinding""><br /><br /> \</issuer ><br /><br /> \</ 消息 ><br /><br /> \</ 安全 ><br /><br /> \<绑定 ><br /><br /> \</wsFederationHttpBinding ><br /><br /> \<wsHttpBinding ><br /><br /> \<绑定名称 =""**northwindBinding**""><br /><br /> \<安全模式 =""消息""><br /><br /> \<消息 clientCredentialType =""Certificate""/ ><br /><br /> \</ 安全 ><br /><br /> \<绑定 ><br /><br /> \</wsHttpBinding ><br /><br /> \</bindings >";**注意：****ReferencedBinding**属性不能包含中使用的绑定配置**BindingConfiguration**属性。  |WCF 自定义适配器<br /><br /> WCF CustomIsolated 适配器|  
  
## <a name="see-also"></a>另请参阅  
 [WCF 适配器](../core/wcf-adapters.md)   
 [\<行为 > 的\<endpointBehaviors >](http://go.microsoft.com/fwlink/?LinkId=80879)   
 [\<绑定 >](http://go.microsoft.com/fwlink/?LinkId=80878)   
 [\<行为 > 的\<serviceBehaviors >](http://go.microsoft.com/fwlink/?LinkId=81095)   
 [有序的消息传送](../core/ordered-delivery-of-messages.md)   
 [负载平衡](http://go.microsoft.com/fwlink/?LinkId=81089)