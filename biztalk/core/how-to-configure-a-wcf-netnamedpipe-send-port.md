---
title: "如何配置 WCF NetNamedPipe 发送端口 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 57684e09-1f72-4bde-976c-3fcec65dc182
caps.latest.revision: "13"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 297c962294042589ce3b9e7bc3303bcd9a55296e
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-configure-a-wcf-netnamedpipe-send-port"></a>如何配置 WCF-NetNamedPipe 发送端口
可以通过编程方式或使用 BizTalk 管理控制台来配置 WCF-NetNamedPipe 发送端口。  
  
## <a name="configuration-properties"></a>配置属性
  
 BizTalk 资源管理器对象模型公开了用于发送端口名为的特定于适配器的接口**ITransportInfo**具有**TransportTypeData**读/写属性。 此属性接受 XML 字符串的名称-值对形式的 WCF-NetNamedPipe 发送端口配置属性包。  
  
 **TransportTypeData**属性**ITransportInfo**界面不是必需。 如果未设置该属性，则适配器将使用 WCF-NetNamedPipe 发送端口配置的默认值，如下表所示。  
  
 下表列出了可在 BizTalk 浏览器对象模型中为 WCF-NetNamedPipe 发送端口设置的配置属性。  
  
|属性名称|类型|Description|  
|-------------------|----------|-----------------|  
|**标识**|XML Blob<br /><br /> 示例：<br /><br /> &lt;标识&gt;<br /><br /> &lt;userPrincipalName 值 ="username@contoso.com"/&gt;<br /><br /> &lt;/identity&gt;|指定此发送端口预期的服务标识。 这些设置支持此发送端口对服务进行验证。 在客户端与服务进行握手的过程中，Windows Communication Foundation (WCF) 基础结构将确保预期服务的标识与此元素的值保持一致。<br /><br /> 默认值为空字符串。|  
|**StaticAction**|字符串|指定**SOAPAction**传出消息的标头字段。 此外可以通过消息上下文属性设置此属性**WCF。操作**在管道或业务流程。 你可以通过两种方式指定此值： 单个操作格式和操作映射格式。 如果将此属性设置中的单个操作格式-例如，http://contoso.com/Svc/Op1- **SOAPAction**标头为传出消息始终设置为此属性中指定的值。<br /><br /> 如果在操作映射格式，传出中设置此属性**SOAPAction**标头由**BTS。操作**上下文属性。 例如，如果此属性设置为以下 XML 格式和**BTS。操作**属性设置为 Op1，为传出的 WCF 发送适配器使用 http://contoso.com/Svc/Op1 **SOAPAction**标头。<br /><br /> \<BtsActionMapping ><br /><br /> \<操作名称 ="Op1"操作 ="http://contoso.com/Svc/Op1"/ ><br /><br /> \<操作名称 ="Op2"操作 ="http://contoso.com/Svc/Op2"/ ><br /><br /> \</ BtsActionMapping ><br /><br /> 如果传出消息来自的业务流程端口时，动态设置业务流程实例**BTS。操作**与操作名称的端口的属性。 如果使用基于内容的路由路由传出消息，则可以设置**BTS。操作**管道组件中的属性。<br /><br /> 默认值为空字符串。|  
|**OpenTimeout**|**System.TimeSpan**|指定一个时间跨度值来表示为完成信道打开操作提供的时间间隔。<br /><br /> 默认值： 00:01:00|  
|**SendTimeout**|**System.TimeSpan**|指定一个时间跨度值来表示为完成发送操作提供的时间间隔。 如果使用要求-响应发送端口，则此值指定完成整个交互的时间跨度（即使服务返回一条大消息）。<br /><br /> 默认值：00:01:00|  
|**CloseTimeout**|**System.TimeSpan**|指定一个时间跨度值来表示为完成信道关闭操作提供的时间间隔。<br /><br /> 默认值：00:01:00|  
|**MaxReceivedMessageSize**|Integer|指定网络上可接收的消息的最大大小（包括标头），以字节为单位。 消息的大小受为每条消息分配的内存量的限制。 你可以使用此属性来降低受拒绝服务 (DoS) 攻击的可能性。<br /><br /> 默认值：65536|  
|**EnableTransaction**|Boolean|指定是否为传输到目标服务并从在事务上下文中使用的 MessageBox 数据库中删除一条消息**Ws-atomictransaction**协议。<br /><br /> 默认值： **False**|  
|**TransactionProtocol**|Enum<br /><br /> -   **OleTransaction**<br />-   **Ws-atomictransaction**|指定要与此绑定一起使用的事务协议。<br /><br /> 默认值： **OleTransaction**|  
|**SecurityMode**|Enum<br /><br /> -   **无**-禁用安全性。<br />-   **传输**:-使用基础的基于的传输安全提供安全性。 可以使用此模式控制保护级别。|指定使用的安全类型。<br /><br /> 默认值：**传输**|  
|**TransportProtectionLevel**|Enum<br /><br /> -   **无**-无保护。<br />-   **登录**-消息进行签名。<br />-   **EncryptAndSign** -消息进行加密和签名。|指定命名管道的保护级别。 消息签名降低了在消息传输过程中第三方对消息进行篡改的风险。 加密为传输过程提供了数据级保密功能。<br /><br /> 默认值： **EncryptAndSign**|  
|**OutboundBodyLocation**|Enum<br /><br /> -   **UseBodyElement** -BizTalk 消息正文部分用于创建的 SOAP 内容**正文**传出消息的元素。<br />-   **UseTemplate** -使用中提供的模板**OutboundXMLTemplate**属性来创建的内容 SOAP**正文**传出消息的元素。<br /><br /> 有关如何使用**OutboundBodyLocation**属性，请参阅[为 WCF 适配器指定消息正文](../core/specifying-the-message-body-for-the-wcf-adapters.md)。|指定 SOAP 数据选择**正文**传出的 WCF 消息的元素。<br /><br /> 默认值： **UseBodyElement**|  
|**OutboundXMLTemplate**|字符串<br /><br /> 有关如何使用**OutboundXMLTemplate**属性，请参阅[为 WCF 适配器指定消息正文](../core/specifying-the-message-body-for-the-wcf-adapters.md)。|指定的 SOAP 内容的 XML 格式模板**正文**的传出消息的元素。 此属性是必需的如果**OutboundBodyLocation**属性设置为**UseTemplate**。<br /><br /> 默认值为空字符串。|  
|**InboundBodyLocation**|Enum<br /><br /> -   **UseBodyElement** -使用 SOAP 的内容**正文**传入消息创建 BizTalk 消息正文部分的元素。 如果 **Body** 元素具有多个子元素，则只有第一个元素将成为 BizTalk 消息正文部分。 此属性仅对要求-响应端口有效。<br />-   **UseEnvelope** -从整个 SOAP 创建 BizTalk 消息正文部分**信封**传入消息。<br />-   **UseBodyPath** -使用中的正文路径表达式**InboundBodyPathExpression**属性创建 BizTalk 消息正文部分。 针对传入消息的 SOAP **Body** 元素的直接子元素计算正文路径表达式。 此属性仅对要求-响应端口有效。<br /><br /> 有关如何使用**InboundBodyLocation**属性，请参阅[为 WCF 适配器指定消息正文](../core/specifying-the-message-body-for-the-wcf-adapters.md)。|指定 SOAP 数据选择**正文**传入 WCF 消息的元素。<br /><br /> 默认值： **UseBodyElement**|  
|**InboundBodyPathExpression**|字符串<br /><br /> 有关如何使用**InboundBodyPathExpression**属性，请参阅[WCF 适配器属性架构和属性](../core/wcf-adapters-property-schema-and-properties.md)。|指定正文路径表达式以标识传入消息中用于创建 BizTalk 消息正文部分的特定部分。 此正文路径表达式针对 SOAP 的即时子元素进行评估**正文**传入消息的节点。 如果此正文路径表达式返回多个节点，则只选择第一个节点作为 BizTalk 消息正文部分。 此属性是必需的如果**InboundBodyLocation**属性设置为**UseBodyPath**。 此属性仅对要求-响应端口有效。<br /><br /> 默认值为空字符串。|  
|**InboundNodeEncoding**|Enum<br /><br /> -   **XML**<br />-   **Base64** -Base64 编码。<br />-   **十六进制**-十六进制编码。<br />-   **字符串**编码文本的 utf-8。<br />-   **XML** -WCF 适配器使用由正文路径表达式中所选节点的外部 XML 创建 BizTalk 消息正文**InboundBodyPathExpression**。|指定 WCF NetNamedPipe 发送适配器用于解码由中指定的正文路径标识的节点的编码类型**InboundBodyPathExpression**。 此属性是必需的如果**InboundBodyLocation**属性设置为**UseBodyPath**。 此属性仅对要求-响应端口有效。<br /><br /> 默认值： **XML**|  
|**PropagateFaultMessage**|Boolean<br /><br /> -   **True** -失败对订阅应用程序的出站处理将消息路由 （如另一个接收端口或业务流程计划）。<br />-   **False** -挂起失败的消息并生成否定确认 (NACK)。|指定是路由还是挂起在出站处理中失败的消息。<br /><br /> 此属性仅对要求-响应端口有效。<br /><br /> 默认值： **True**|  
  
## <a name="configure-a-wcf-netnamedpipe-send-port-with-the-biztalk-administration-console"></a>使用 BizTalk 管理控制台中配置 WCF NetNamedPipe 发送端口
  
 可以在 BizTalk 管理控制台中设置 WCF-NetNamedPipe 发送端口适配器变量。 如果没有为发送端口设置属性，将使用 WCF-NetNamedPipe 发送端口配置的默认值，如前表所示。  
  
## <a name="configure-variables-for-a-wcf-netnamedpipe-send-port"></a>配置变量 WCF NetNamedPipe 发送端口  
  
1.  在 BizTalk 管理控制台中，创建一个新的发送端口或双击某个现有发送端口以对其进行修改。 有关详细信息，请参阅[如何创建发送端口](../core/how-to-create-a-send-port2.md)。 配置所有发送端口选项并指定**WCF NetNamedPipe**为**类型**选项**传输**部分**常规**选项卡。  
  
2.  上**常规**选项卡上，在**传输**部分中，单击**配置**按钮旁边**类型**。  
  
3.  在**WCF NetNamedPipe 传输属性**对话框中，在**常规**选项卡上配置的终结点地址，服务标识，与**SOAPAction**标头WCF NetNamedPipe 发送端口。 有关详细信息**常规**选项卡中**WCF NetNamedPipe 传输属性**对话框中，请参阅**WCF NetNamedPipe 传输属性对话框中，发送，常规**选项卡[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。
  
4.  在**WCF NetNamedPipe 传输属性**对话框中，在**绑定**选项卡上配置的超时和事务的属性。 有关详细信息**绑定**选项卡中**WCF NetNamedPipe 传输属性**对话框中，请参阅**WCF NetNamedPipe 传输属性对话框中，发送，绑定**选项卡[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。
  
5.  在**WCF NetNamedPipe 传输属性**对话框中，在**安全**选项卡上，定义 WCF NetNamedPipe 发送端口的安全功能。 有关详细信息**安全**选项卡中**WCF NetNamedPipe 传输属性**对话框中，请参阅**WCF NetNamedPipe 传输属性对话框中，发送，安全**选项卡[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。
  
6.  在**WCF NetNamedPipe 传输属性**对话框中，在**消息**选项卡上，指定 SOAP 数据选择**正文**元素。 有关详细信息**消息**选项卡中**WCF NetNamedPipe 传输属性**对话框中，请参阅**WCF NetNamedPipe 传输属性对话框中，发送消息**选项卡[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。
  
## <a name="configure-a-wcf-netnamedpipe-send-port-programmatically"></a>以编程方式配置 WCF NetNamedPipe 发送端口
  
 可使用以下格式设置属性：  
  
```  
<CustomProps>  
  <TransportProtectionLevel vt="8">EncryptAndSign</TransportProtectionLevel>  
  <TransactionProtocol vt="8">OleTransactions</TransactionProtocol>  
  <InboundBodyPathExpression vt="8" />  
  <PropagateFaultMessage vt="11">-1</PropagateFaultMessage>  
  <CloseTimeout vt="8">00:01:00</CloseTimeout>  
  <OutboundBodyLocation vt="8">UseBodyElement</OutboundBodyLocation>  
  <StaticAction vt="8">http://www.northwindtraders.com/Service/Operation</StaticAction>  
  <SendTimeout vt="8">00:01:00</SendTimeout>  
  <InboundNodeEncoding vt="8">Xml</InboundNodeEncoding>  
  <EnableTransaction vt="11">0</EnableTransaction>  
  <SecurityMode vt="8">Transport</SecurityMode>  
  <InboundBodyLocation vt="8">UseBodyElement</InboundBodyLocation>  
  <OpenTimeout vt="8">00:01:00</OpenTimeout>  
  <OutboundXmlTemplate vt="8"><bts-msg-body xmlns="http://www.microsoft.com/schemas/bts2007" encoding="xml"/></OutboundXmlTemplate>  
  <MaxReceivedMessageSize vt="3">2097152</MaxReceivedMessageSize>  
</CustomProps>  
  
```  
  
 下面的代码段说明了如何创建 WCF-NetNamedPipe 发送端口：  
  
```  
// Use BizTalk Explorer object model to create new WCF-NetNamedPipe send port.  
string server = System.Environment.MachineName;  
string database = "BizTalkMgmtDb";  
string connectionString = string.Format("Server={0};Database={1};Integrated Security=true", server, database);  
string transportConfigData = @"<CustomProps>  
                                 <StaticAction vt=""8"">http://www.northwindtraders.com/Service/Operation</StaticAction>  
                                 <OpenTimeout vt=""8"">00:01:00</OpenTimeout>  
                               </CustomProps>";  
//requires project reference to \Program Files\Microsoft BizTalk Server 2009\Developer Tools\Microsoft.BizTalk.ExplorerOM.dll  
BtsCatalogExplorer explorer = new Microsoft.BizTalk.ExplorerOM.BtsCatalogExplorer();  
explorer.ConnectionString = connectionString;  
// Add a new BizTalk application  
Application application = explorer.AddNewApplication();  
application.Name = "SampleBizTalkApplication";  
// Save  
explorer.SaveChanges();  
  
// Add a new static one-way send port  
SendPort sendPort = application.AddNewSendPort(false, false);   
sendPort.Name = "SampleSendPort";  
sendPort.PrimaryTransport.TransportType = explorer.ProtocolTypes["WCF-NetNamedPipe"];  
sendPort.PrimaryTransport.Address = "net.pipe://mycomputer/private/samplequeue";  
sendPort.PrimaryTransport.TransportTypeData = transportConfigData; // propertyData; // need to change  
sendPort.SendPipeline = explorer.Pipelines["Microsoft.BizTalk.DefaultPipelines.PassThruTransmit"];  
// Save  
explorer.SaveChanges();  
```  
  
## <a name="see-also"></a>另请参阅  
 [WCF 适配器属性架构和属性](../core/wcf-adapters-property-schema-and-properties.md)   
 [为 WCF 适配器指定消息正文](../core/specifying-the-message-body-for-the-wcf-adapters.md)   
 [将证书安装适用于这些 WCF 适配器](../core/installing-certificates-for-the-wcf-adapters.md)   
 [配置 WCF NetNamedPipe 适配器](../core/configuring-the-wcf-netnamedpipe-adapter.md)   
 [配置动态发送端口使用 WCF 适配器上下文属性](../core/configuring-dynamic-send-ports-using-wcf-adapters-context-properties.md)