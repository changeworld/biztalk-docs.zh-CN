---
title: "WCF BasicHttpRelay 适配器 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 22eefde6-80f5-4d45-80cf-55f743ff9d45
caps.latest.revision: "5"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 621a36173677b3bf6a2221316e4c03aee8de84fa
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="wcf-basichttprelay-adapter"></a>WCF-BasicHttpRelay 适配器
[!INCLUDE[btsCoName](../includes/btsconame-md.md)][!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]使用**WCF BasicHttpRelay**适配器接收和发送通过 WCF 服务请求[BasicHttpRelayBinding 类](https://msdn.microsoft.com/library/azure/microsoft.servicebus.basichttprelaybinding.aspx)。 **WCF BasicHttpRelay**适配器使用 Service Bus 中继终结点使用**BasicHttpRelayBinding**。  

## <a name="before-you-begin"></a>开始之前

从开始[!INCLUDE[bts2016_md](../includes/bts2016-md.md)]，此适配器可以用于服务总线使用访问控制服务 (ACS) 或共享访问签名 (SAS) 到 athenticate。 我们建议使用服务总线进行身份验证时使用共享访问签名 (SAS)。 

当你创建了服务总线命名空间时，不自动创建 Access Control (ACS) 命名空间。 如果使用 ACS 进行身份验证，你可能需要创建一个新的 ACS 命名空间。 请参阅[SB 消息适配器](../core/sb-messaging-adapter.md)更多详细信息，包括检索 ACS 密钥值的步骤。
  
## <a name="create-the-receive-location"></a>创建接收位置
  
> [!NOTE]
>  之前完成以下过程，你必须已添加单向接收端口。 请参阅[如何创建接收端口](../core/how-to-create-a-receive-port.md)。  
  
1.  在 BizTalk Server 管理控制台中，展开[!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]，展开**BizTalk 组**，展开**应用程序**，然后展开应用程序在你想要创建接收位置。  
  
2.  在左窗格中，单击“接收端口”  节点，在右窗格中，右键单击你希望将新的接收位置与其关联的接收端口，然后单击“属性” 。  
  
3.  在“接收端口属性”  对话框的左窗格中，选择“接收位置” ，然后在右窗格中单击“新建”  以创建新的接收位置。  
  
4.  在**接收位置属性**对话框中，在**传输**部分中，选择**WCF BasicHttpRelay**从**类型**下拉列表，然后单击**配置**若要配置接收位置的传输属性。  
  
5.  在**WCF BasicHttpRelay 传输属性**对话框中，在**常规**选项卡上，配置终结点地址的服务总线中继终结点的托管位置和的服务标识WCF BasicHttpRelay 接收位置。  
  
    |使用此选项|执行的操作|  
    |--------------|----------------|  
    |**地址 (URI)**|必需的。 指定在其中部署 Service Bus 中继终结点的 URI。|  
    |**终结点标识**|可选。 指定终结点标识。 通过这些设置，终结点可对此接收位置进行验证。 在终结点与接收位置进行握手的过程中，Windows Communication Foundation (WCF) 基础结构将确保预期服务的标识与此元素的值保持一致。<br /><br /> 默认值为空字符串。|  
  
6.  在**WCF BasicHttpRelay 传输属性**对话框中，在**绑定**选项卡上配置的超时和编码相关的属性。  
  
    |使用此选项|执行的操作|  
    |--------------|----------------|  
    |**打开超时 (hh:mmss)**|指定一个时间跨度值来表示为完成信道打开操作提供的时间间隔。 此值应大于或等于 **System.TimeSpan.Zero**。<br /><br /> 默认值：00:01:00<br /><br /> 最大值：23:59:59|  
    |**发送超时时 (hh:mmss)**|指定一个时间跨度值来表示为完成发送操作提供的时间间隔。 此值应大于或等于 **System.TimeSpan.Zero**。 如果使用请求-响应接收端口，则此值指定完成整个交互的时间跨度（即使客户端返回一条大消息）。<br /><br /> 默认值：00:01:00<br /><br /> 最大值：23:59:59|  
    |**关闭超时 (hh:mmss)**|指定一个时间跨度值来表示为完成信道关闭操作提供的时间间隔。 此值应大于或等于 **System.TimeSpan.Zero**。<br /><br /> 默认值：00:01:00<br /><br /> 最大值：23:59:59|  
    |**收到的最大消息大小 （字节）**|指定网络上可接收的消息的最大大小（包括标头），以字节表示。 消息的大小受为每条消息分配的内存量的限制。 你可以使用此属性来降低受拒绝服务 (DoS) 攻击的可能性。<br /><br /> WCF BasicHttpRelay 适配器利用[BasicHttpRelayBinding](http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.basichttprelaybinding.aspx)在缓冲的传输模式中与终结点进行通信的类。 对于缓冲的传输模式中， [BasicHttpRelayBinding.MaxBufferSize](http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.basichttprelaybinding.maxbuffersize.aspx)属性也始终等于此属性的值。<br /><br /> 默认值：65536<br /><br /> 最大值：2147483647|  
    |**消息编码**|指定用于对 SOAP 消息进行编码的编码器。 有效值包括：<br /><br /> -   **文本**： 使用文本消息编码器。<br />-   **Mtom**： 使用消息传输组织机制 1.0 (MTOM) 编码器。<br /><br /> 默认值是**文本**。|  
    |**文本编码**|指定的字符集编码要用于在绑定上发出消息时**消息编码**属性设置为**文本**。 有效值包括：<br /><br /> -   **utf 16BE (unicodeFFFE)**: Unicode BigEndian 编码。<br />-   **utf-16**: 16 位编码。<br />-   **utf-8**: 8 位编码<br /><br /> 默认值是**utf-8**。|  
    |**最大并发调用**|指定针对单个服务实例的并发调用的数目。 超出此限制的调用将在队列中排队。 将该值设置为 0 等效于将它设置为 **Int32.MaxValue**。<br /><br /> 默认值为 200。|  
  
7.  在**WCF BasicHttpRelay 传输属性**对话框中，在**安全**选项卡上，定义安全性功能 WCF BasicHttpRelay 接收位置。  
  
    |使用此选项|执行的操作|  
    |--------------|----------------|  
    |**安全模式**|指定使用的安全类型。 有效值包括：<br /><br /> -   **无**： 在传输过程不保护消息。<br />-   **传输**： 使用 HTTPS 传输提供安全性。 使用 HTTPS 对 SOAP 消息进行保护。 若要使用此模式，你必须在 Microsoft Internet 信息服务 (IIS) 中设置安全套接字层 (SSL)。<br />-   **消息**： 使用 HTTP 传输的 SOAP 消息安全提供安全性。 默认情况下，SOAP“正文”  已加密和签名。 仅有的有效**消息客户端凭据类型**对于 WCF Basic 适配器是**证书**。 此模式需要 HTTP 传输。 使用此安全模式时，此服务证书接收位置需要通过提供**服务证书的指纹**属性。<br />-   **TransportWithMessageCredential**： 由 HTTPS 传输提供完整性、 保密性和服务身份验证。 若要使用此模式，你必须在 Microsoft Internet 信息服务 (IIS) 中设置安全套接字层 (SSL)。<br /><br /> 默认值为“传输” 。|  
    |**消息客户端凭据类型**|指定的消息级安全选项，仅当你设置**安全模式**上面到**消息**或**TransportWithMessageCredential**。 有效值包括：<br /><br /> -   **用户名**： 启用此接收位置需要客户端进行身份验证使用**用户名**凭据。 你必须创建的域或本地用户帐户对应的客户端凭据。<br />-   **证书**： 客户端进行身份验证到此接收位置使用客户端证书。 必须将用于客户端 X.509 证书的 CA 证书链安装到此计算机的“受信任根证书颁发机构”证书存储中，以便可以针对此接收位置验证客户端。<br /><br /> 默认值是**用户名**。|  
    |**算法套件**|指定的消息加密和密钥换行算法，仅当你设置**安全模式**到上面的模式**消息**或**TransportWithMessageCredential**。 这不是适用于你设置的情况**安全模式**到**无**或**传输**。<br /><br /> 这些算法与“安全策略语言”(WS-SecurityPolicy) 规范中指定的算法一致。 可能的值有：<br /><br /> -   **Basic128**： 使用 Aes128 加密，对消息摘要的 Sha1，对密钥包装的 Rsa-oaep-mgf1p。<br />-   **Basic128Rsa15**： 对消息加密使用 Aes128，对消息摘要的 Sha1，对密钥包装使用 Rsa15。<br />-   **Basic128Sha256**： 对消息加密使用 Aes256，对消息摘要的 Sha256，对密钥包装的 Rsa-oaep-mgf1p。<br />-   **Basic128Sha256Rsa15**： 对消息加密使用 Aes128，对消息摘要的 Sha256，对密钥包装使用 Rsa15。<br />-   **Basic192**： 使用 Aes192 加密，对消息摘要的 Sha1，对密钥包装的 Rsa-oaep-mgf1p。<br />-   **Basic192Rsa15**： 对消息加密使用 Aes192，对消息摘要的 Sha1，对密钥包装使用 Rsa15。<br />-   **Basic192Sha256**： 对消息加密使用 Aes192，对消息摘要的 Sha256，对密钥包装的 Rsa-oaep-mgf1p。<br />-   **Basic192Sha256Rsa15**： 对消息加密使用 Aes192，对消息摘要的 Sha256，对密钥包装使用 Rsa15。<br />-   **Basic256**： 使用 Aes256 加密，对消息摘要的 Sha1，对密钥包装的 Rsa-oaep-mgf1p。<br />-   **Basic256Rsa15**： 对消息加密使用 Aes256，对消息摘要的 Sha1，对密钥包装使用 Rsa15。<br />-   **Basic256Sha256**： 对消息加密使用 Aes256，对消息摘要的 Sha256，对密钥包装的 Rsa-oaep-mgf1p。<br />-   **Basic256Sha256Rsa15**： 对消息加密使用 Aes256，对消息摘要的 Sha256，对密钥包装使用 Rsa15。<br />-   **TripleDes**： 使用 TripleDes 加密，对消息摘要，Rsa oaep-mgf1p 对密钥包装 Sha1。<br />-   **TripleDesRsa15**： 使用 TripleDes 加密，对消息摘要的 Sha1，对密钥包装使用 Rsa15。<br />-   **TripleDesSha256**： 对消息加密使用 TripleDes，对消息摘要的 Sha256，对密钥包装的 Rsa-oaep-mgf1p。<br />-   **TripleDesSha256Rsa15**： 对消息加密使用 TripleDes，对消息摘要的 Sha256，对密钥包装使用 Rsa15。<br /><br /> 默认值为“Basic256” 。|  
    |**服务证书的指纹**|为此接收位置指定 X.509 证书的指纹，客户端利用该指纹验证服务。 使用“浏览”  按钮，导航到“当前用户”  位置中“我的”  存储，然后即可选择指纹。 **注意：**必须设置此属性，仅当你设置**安全模式**到上面的模式**消息**或**TransportWithMessageCredential**。 这不是适用于你设置的情况**安全模式**到**无**或**传输**。 **注意：**必须安装到的服务证书**当前用户**承载此接收位置接收处理程序的用户帐户的位置。 <br /><br /> 最小长度：0<br /><br /> 最大长度：40<br /><br /> 默认值为空字符串。|  
    |**中继客户端身份验证类型**|指定对 Service Bus 中继终结点（可通过其接收消息）进行身份验证的选项。 有效值包括：<br /><br /> -   **无**： 无身份验证是必需的。<br />-   **RelayAccessToken**： 指定此选项可使用的安全令牌以授权与 Service Bus 中继终结点。<br /><br /> 默认值为“RelayAccessToken” 。|  
    |**启用服务发现**|选中此复选框可指定是否在服务注册表中发布服务的行为。<br /><br /> -   **显示名称**– 指定与该服务发布到服务注册表的名称。<br />-   **发现模式**– 设置在服务注册表中发布的服务的发现模式。 有关发现模式的详细信息，请参阅 [http://msdn.microsoft.com/library/microsoft.servicebus.discoverytype.aspx](http://msdn.microsoft.com/library/microsoft.servicebus.discoverytype.aspx)。|  
    |**访问控制服务**|适用于[!INCLUDE[bts2013r2_md](../includes/bts2013r2-md.md)]和[!INCLUDE[btsBizTalkServerNoVersion_md](../includes/btsbiztalkservernoversion-md.md)]2013年。<br/><br/>如果将“中继客户端身份验证类型”  设置为“RelayAccessToken” ，请单击“编辑”  按钮，然后指定以下详细信息：<br /><br /> -   **访问控制服务 STS Uri** – 设置为`https://<Namespace>-sb.accesscontrol.windows.net/`，其中\<命名空间 > 是你的服务总线命名空间。<br />-   **颁发者名称**– 指定的颁发者名称。 通常将此值设置为 owner。<br />-   **颁发者密钥**– 指定的颁发者密钥。|  
    |**服务总线连接信息** | 新开头[!INCLUDE[bts2016_md](../includes/bts2016-md.md)]。<br/><br/>选择使用共享访问签名 (SAS) 或 Service Bus 命名空间的访问控制服务 (ACS)。 <br/><br/>选择一个选项，然后选择**编辑**输入的密钥信息：<br/><br/> - **共享访问签名**： 输入访问密钥名称和访问密钥。 这两个值中列出[Azure 门户](https://portal.azure.com)。<br/> - **访问控制服务**： 输入 STS URI (`https://<yourNamespace>-sb.accesscontrol.windows.net/`)，颁发者名称和颁发者密钥。 使用 Windows PowerShell 检索这些值中所述[SB 消息适配器](../core/sb-messaging-adapter.md)。 |
  
8.  在**WCF BasicHttpRelay 传输属性**对话框中，在**消息**选项卡上，指定 SOAP 数据选择**正文**元素。  
  
    |使用此选项|执行的操作|  
    |--------------|----------------|  
    |**信封--完整\<soap： 信封 >**|从传入消息的整个 SOAP **Envelope** 创建 BizTalk 消息正文部分。<br /><br /> 默认值为清除此复选框。|  
    |**正文--内容\<soap： 正文 > 元素**|使用传入消息的 SOAP **Body** 元素的内容创建 BizTalk 消息正文部分。 如果 **Body** 元素具有多个子元素，则只有第一个元素将成为 BizTalk 消息正文部分。<br /><br /> 这是默认设置。|  
    |**路径--由正文路径定位的内容**|使用“正文路径表达式”  文本框中的正文路径表达式创建 BizTalk 消息正文部分。 针对传入消息的 SOAP **Body** 元素的直接子元素计算正文路径表达式。<br /><br /> 默认值为清除此复选框。|  
    |**正文路径表达式**|键入正文路径表达式以标识传入消息中用于创建 BizTalk 消息正文部分的特定部分。 针对传入消息的 SOAP **Body** 元素的直接子元素计算此正文路径表达式。 如果此正文路径表达式返回多个节点，则只选择第一个节点作为 BizTalk 消息正文部分。 如果选择了“路径 -- 按正文路径定位内容”  选项，则此属性是必需的。<br /><br /> 类型：字符串<br /><br /> 最小长度：0<br /><br /> 最大长度：32767<br /><br /> 默认值为空字符串。|  
    |**节点编码**|指定的编码，WCF BasicHttpRelay 接收适配器使用要解码识别由正文路径表达式中的节点类型**正文路径表达式**文本框。<br /><br /> 如果选择了“路径 -- 按正文路径定位内容”  选项，则此属性是必需的。 有效值包括：<br /><br /> -   **Base64**: Base64 编码。<br />-   **十六进制**： 十六进制编码。<br />-   **字符串**： 文本编码的 utf-8<br />-   **XML**: WCF 适配器使用由正文路径表达式中所选节点的外部 XML 创建 BizTalk 消息正文**正文路径表达式**文本框。<br /><br /> 默认值为“XML” 。|  
    |**正文--BizTalk 响应消息正文**|使用 BizTalk 消息正文部分创建传出响应消息的 SOAP **Body** 元素的内容。 此属性仅对请求响应接收位置有效。<br /><br /> 这是默认设置。|  
    |**指定模板的模板--内容**|使用在“XML”  文本框中提供的模板创建传出消息的 SOAP **Body** 元素的内容。 此属性仅对请求响应接收位置有效。<br /><br /> 默认值为清除此复选框。|  
    |**XML**|为传出消息的 SOAP **Body** 元素的内容键入 XML 格式的模板。 如果选择了“模板 -- BizTalk 响应消息正文”  选项，则此属性是必需的。 此属性仅对请求响应接收位置有效。<br /><br /> 类型：字符串<br /><br /> 最小长度：0<br /><br /> 最大长度：32767<br /><br /> 默认值是 **\<bts 消息正文 xmlns ="http://www.microsoft.com/schemas/bts2007"编码 ="xml"/ >**。|  
    |**挂起失败的请求消息**|指定是否将由于接收管道故障或路由故障而导致入站处理失败的请求消息挂起。<br /><br /> 默认值为清除此复选框。|  
    |**错误中包括异常详细信息**|指定发生错误时是否返回 SOAP 错误以方便进行调试。<br /><br /> 默认值为清除此复选框。|  
  
9. 单击 **“确定”**。  
  
10. 在“接收位置属性”  对话框中输入相应的值，完成对接收位置的配置，然后单击“确定”  保存设置。 璝惠**接收位置属性**对话框中，请参阅[如何创建接收位置](../core/how-to-create-a-receive-location.md)。  

## <a name="create-the-send-port"></a>创建发送端口

1.  在 BizTalk 管理控制台中，创建一个新的发送端口或双击某个现有发送端口以对其进行修改。 请参阅[如何创建发送端口](../core/how-to-create-a-send-port2.md)。 配置所有发送端口选项并指定**WCF BasicHttpRelay**为**类型**选项**传输**部分**常规**选项卡。  
  
2.  上**常规**选项卡上，在**传输**部分中，单击**配置**按钮。  
  
3.  在**WCF BasicHttpRelay 传输属性**对话框中，在**常规**选项卡上，指定下列各项：  
  
    |使用此选项|执行的操作|  
    |--------------|----------------|  
    |**地址 (URI)**|必需的。 指定在 Service Bus 上部署中继终结点的 URL。 通常此 URL 的格式如下：<br /><br /> `https://<namespace>.servicebus.windows.net/`|  
    |**终结点标识**|可选。 指定终结点标识。 这些设置支持此发送端口对终结点进行验证。 在终结点与发送端口进行握手的过程中，Windows Communication Foundation (WCF) 基础结构将确保终结点的标识与此元素的值匹配。<br /><br /> 默认值为清除此复选框。|  
    |**操作**|指定**SOAPAction**传出消息的 HTTP 标头字段。 此外可以通过消息上下文属性设置此属性**WCF。操作**在管道或业务流程。 你可以通过两种方式指定此值： 单个操作格式和操作映射格式。 如果将此属性设置中的单个操作格式-例如， `http://contoso.com/Svc/Op1`- **SOAPAction**标头为传出消息始终设置为此属性中指定的值。<br /><br /> 如果在操作映射格式，传出中设置此属性**SOAPAction**标头由**BTS。操作**上下文属性。 例如，如果此属性设置为以下 XML 格式和**BTS。操作**属性设置为 Op1，WCF 发送适配器使用`http://contoso.com/Svc/Op1`为传出**SOAPAction**标头。<br /><br /> `<BtsActionMapping> <Operation Name="Op1" Action="http://contoso.com/Svc/Op1" /> <Operation Name="Op2" Action="http://contoso.com/Svc/Op2" /> </BtsActionMapping>`<br /><br /> 如果传出消息来自于业务流程端口，动态设置业务流程实例**BTS。操作**与操作名称的端口的属性。 如果使用基于内容的路由路由传出消息，则可以设置**BTS。操作**管道组件中的属性。<br /><br /> 重要事项：<br /><br /> [!INCLUDE[sb](../includes/sb-md.md)] 要求在向中继终结点发送消息时设置 SOAP 操作。<br /><br /> 最小长度：0<br /><br /> 最大长度：32767<br /><br /> 默认值为空字符串。|  
  
4.  在**WCF BasicHttpRelay 传输属性**对话框中，在**绑定**选项卡上，配置的超时和编码属性。  
  
    |使用此选项|执行的操作|  
    |--------------|----------------|  
    |**打开超时 (hh:mmss)**|指定一个时间跨度值来表示为完成信道打开操作提供的时间间隔。 此值应大于或等于 **System.TimeSpan.Zero**。<br /><br /> 默认值：00:01:00<br /><br /> 最大值：23:59:59|  
    |**发送超时时 (hh:mmss)**|指定一个时间跨度值来表示为完成发送操作提供的时间间隔。 此值应大于或等于 **System.TimeSpan.Zero**。 如果使用要求-响应发送端口，则此值指定完成整个交互的时间跨度（即使服务返回一条大消息）。<br /><br /> 默认值：00:01:00<br /><br /> 最大值：23:59:59|  
    |**关闭超时 (hh:mmss)**|指定一个时间跨度值来表示为完成信道关闭操作提供的时间间隔。 此值应大于或等于**System.TimeSpan.Zero**。<br /><br /> 默认值：00:01:00<br /><br /> 最大值：23:59:59|  
    |**收到的最大消息大小 （字节）**|指定网络上可接收的消息的最大大小（包括标头），以字节表示。 消息的大小受为每条消息分配的内存量的限制。 你可以使用此属性来降低受拒绝服务 (DoS) 攻击的可能性。<br /><br /> WCF BasicHttpRelay 适配器利用[BasicHttpBinding](http://go.microsoft.com/fwlink/?LinkId=81086)在缓冲的传输模式中与终结点进行通信的类。 对于缓冲的传输模式中， [BasicHttpBinding.MaxBufferSize](http://go.microsoft.com/fwlink/?LinkId=80659)属性也始终等于此属性的值。<br /><br /> 默认值：65536<br /><br /> 最大值：2147483647|  
    |**消息编码**|指定用于对 SOAP 消息进行编码的编码器。 有效值包括：<br /><br /> -                         **文本**： 使用文本消息编码器。<br /><br /> -                         **Mtom**： 使用消息传输组织机制 1.0 (MTOM) 编码器。<br /><br /> 默认值：**文本**|  
    |**文本编码**|指定的字符集编码要用于在绑定上发出消息时**消息编码**属性设置为**文本**。 有效值包括：<br /><br /> -                         **utf 16BE (unicodeFFFE)**: Unicode BigEndian 编码。<br /><br /> -                         **utf-16**: 16 位编码。<br /><br /> -                         **utf-8**: 8 位编码<br /><br /> 默认值： **utf-8**|  
  
5.  在**WCF BasicHttpRelay 传输属性**对话框中，在**安全**选项卡上，定义 WCF BasicHttpRelay 发送端口的安全功能。  
  
    |使用此选项|执行的操作|  
    |--------------|----------------|  
    |**安全模式**|指定使用的安全类型。 有效值包括：<br /><br /> -                         **无**： 在传输过程不保护消息。<br /><br /> -                         **传输**： 使用 HTTPS 传输提供安全性。 使用 HTTPS 对 SOAP 消息进行保护。 服务的 X.509 证书的 CA 证书链必须安装到此计算机的“受信任根证书颁发机构”证书存储区中，以便可以使用该服务的证书向发送端口验证该服务。<br /><br /> -                         **消息**： 使用 SOAP 消息安全提供安全性。 默认情况下，SOAP**正文**元素进行加密和签名。 仅有的有效**消息客户端凭据类型**对于 WCF BasicHttpRelay 发送适配器是**证书**。 此模式需要 HTTP 传输。<br /><br /> -                         **TransportWithMessageCredential**： 由 HTTPS 传输提供完整性、 保密性和服务身份验证。 服务的 X.509 证书的 CA 证书链必须安装到此计算机的“受信任根证书颁发机构”证书存储区中，以便使用服务证书向发送端口验证该服务。 发送端口验证由 SOAP 消息安全性提供。<br /><br /> 默认值是**无**。|  
    |**消息客户端凭据类型**|指定的消息级安全选项，仅当你设置**安全模式**上面到**消息**或**TransportWithMessageCredential**。 有效值包括：<br /><br /> -                         **用户名**： 此发送端口进行身份验证的端点到**用户名**凭据。 对于 WCF-BasicHttpRelay 发送适配器，不支持此功能。<br /><br /> -                         **证书**： 此发送端口到终结点使用通过指定的客户端证书进行身份验证**客户端证书的指纹**属性。 此外，当使用此凭据类型，则需要通过提供服务证书**服务证书的指纹**属性。<br /><br /> 默认值是**用户名**。|  
    |**算法套件**|指定消息加密和密钥包装算法。 这些算法与“安全策略语言”(WS-SecurityPolicy) 规范中指定的算法一致。 可能的值有：<br /><br /> -                         **Basic128**： 使用 Aes128 加密，对消息摘要的 Sha1，对密钥包装的 Rsa-oaep-mgf1p。<br /><br /> -                         **Basic128Rsa15**： 对消息加密使用 Aes128，对消息摘要的 Sha1，对密钥包装使用 Rsa15。<br /><br /> -                         **Basic128Sha256**： 对消息加密使用 Aes256，对消息摘要的 Sha256，对密钥包装的 Rsa-oaep-mgf1p。<br /><br /> -                         **Basic128Sha256Rsa15**： 对消息加密使用 Aes128，对消息摘要的 Sha256，对密钥包装使用 Rsa15。<br /><br /> -                         **Basic192**： 使用 Aes192 加密，对消息摘要的 Sha1，对密钥包装的 Rsa-oaep-mgf1p。<br /><br /> -                         **Basic192Rsa15**： 对消息加密使用 Aes192，对消息摘要的 Sha1，对密钥包装使用 Rsa15。<br /><br /> -                         **Basic192Sha256**： 对消息加密使用 Aes192，对消息摘要的 Sha256，对密钥包装的 Rsa-oaep-mgf1p。<br /><br /> -                         **Basic192Sha256Rsa15**： 对消息加密使用 Aes192，对消息摘要的 Sha256，对密钥包装使用 Rsa15。<br /><br /> -                         **Basic256**： 使用 Aes256 加密，对消息摘要的 Sha1，对密钥包装的 Rsa-oaep-mgf1p。<br /><br /> -                         **Basic256Rsa15**： 对消息加密使用 Aes256，对消息摘要的 Sha1，对密钥包装使用 Rsa15。<br /><br /> -                         **Basic256Sha256**： 对消息加密使用 Aes256，对消息摘要的 Sha256，对密钥包装的 Rsa-oaep-mgf1p。<br /><br /> -                         **Basic256Sha256Rsa15**： 对消息加密使用 Aes256，对消息摘要的 Sha256，对密钥包装使用 Rsa15。<br /><br /> -                         **TripleDes**： 使用 TripleDes 加密，对消息摘要，Rsa oaep-mgf1p 对密钥包装 Sha1。<br /><br /> -                         **TripleDesRsa15**： 使用 TripleDes 加密，对消息摘要的 Sha1，对密钥包装使用 Rsa15。<br /><br /> -                         **TripleDesSha256**： 对消息加密使用 TripleDes，对消息摘要的 Sha256，对密钥包装的 Rsa-oaep-mgf1p。<br /><br /> -                         **TripleDesSha256Rsa15**： 对消息加密使用 TripleDes，对消息摘要的 Sha256，对密钥包装使用 Rsa15。<br /><br /> 默认值为“Basic256” 。|  
    |**客户端证书的指纹**|指定用于向终结点验证此发送端口的 X.509 证书的指纹。 你可以通过导航到选择指纹**我**将存储在**当前用户**位置与**浏览**按钮。<br /><br /> 注意：<br /><br /> 你必须安装到客户端证书**当前用户**承载该发送处理程序的用户帐户的位置发送端口。<br /><br /> 最小长度：0<br /><br /> 最大长度：40<br /><br /> 默认值为空字符串。|  
    |**服务证书的指纹**|指定用于验证终结点（此发送端口要将消息发送到的终结点）的 X.509 证书的指纹。 你可以选择导航到的指纹**其他人**将存储在**本地计算机**位置与**浏览**按钮。<br /><br /> 最小长度：0<br /><br /> 最大长度：40<br /><br /> 默认值为空字符串。|  
    |**用户名凭据**|指定用于发送消息的凭据。 你可以通过单击指定属性**编辑**按钮。 你必须设置凭据，如果你选择**用户名**选项**消息客户端凭据类型**。<br /><br /> 默认值是**不使用单一登录**。|  
    |**使用 ACS 服务标识**|适用于[!INCLUDE[bts2013r2_md](../includes/bts2013r2-md.md)]和[!INCLUDE[btsBizTalkServerNoVersion_md](../includes/btsbiztalkservernoversion-md.md)]2013年。<br/><br/>选择此复选框，然后单击**编辑**并提供以下值，以使用 Service Bus 进行身份验证。<br /><br /> -                         **访问控制服务 STS Uri** – 设置为`https://<Namespace>-sb.accesscontrol.windows.net/`，其中\<命名空间 > 是你的服务总线命名空间。<br /><br /> -                         **颁发者名称**– 指定的颁发者名称。 通常将此值设置为 owner。<br /><br /> -                         **颁发者密钥**– 指定的颁发者密钥。|  
    |**服务总线连接信息** | 新开头[!INCLUDE[bts2016_md](../includes/bts2016-md.md)]。<br/><br/>选择使用共享访问签名 (SAS) 或 Service Bus 命名空间的访问控制服务 (ACS)。 <br/><br/>选择一个选项，然后选择**编辑**输入的密钥信息：<br/><br/> - **共享访问签名**： 输入访问密钥名称和访问密钥。 这两个值中列出[Azure 门户](https://portal.azure.com)。<br/> - **访问控制服务**： 输入 STS URI (`https://<yourNamespace>-sb.accesscontrol.windows.net/`)，颁发者名称和颁发者密钥。 使用 Windows PowerShell 检索这些值中所述[SB 消息适配器](../core/sb-messaging-adapter.md)。 |
  
6.  在**WCF BasicHttpRelay 传输属性**对话框中，在**代理**选项卡上配置的代理设置 WCF BasicHttpRelay 发送端口。  
  
    |使用此选项|执行的操作|  
    |--------------|----------------|  
    |**使用发送处理程序代理设置**|指定此发送端口是否使用承载此发送端口的发送处理程序中的代理设置。<br /><br /> 这是默认设置。|  
    |**不使用代理服务器**|指示此发送端口是否使用代理服务器。<br /><br /> 默认值为清除此复选框。|  
    |**使用代理**|指示此发送端口使用中指定的代理服务器**地址**属性。<br /><br /> 默认值为清除此复选框。|  
    |**Address**|指定代理服务器的地址。 使用**https**或**http**根据安全配置的方案。 此地址后面可跟冒号和端口号。 例如，http://127.0.0.1:8080。<br /><br /> 此属性，则需要值才**使用代理**选择。<br /><br /> 类型：字符串<br /><br /> 最大长度：256<br /><br /> 默认值为空字符串。|  
    |**用户名**|指定用于身份验证的用户名。 如果使用集成身份验证，则用户名将包括域，即采用“域\用户名”格式。 如果使用基本或摘要式身份验证，则用户名不包括域\\。 此属性，则需要值才**使用代理**选择。<br /><br /> 注意：<br /><br /> WCF-BasicHttpRelay 发送适配器对代理使用基本身份验证。<br /><br /> 类型：字符串<br /><br /> 最小长度：0<br /><br /> 最大长度：256<br /><br /> 默认值为空字符串。|  
    |**密码**|指定用于身份验证的密码。<br /><br /> 此属性，则需要值才**使用代理**选择。<br /><br /> 类型：字符串<br /><br /> 最小长度：0<br /><br /> 最大长度：256<br /><br /> 默认值为空字符串。|  
  
7.  在**WCF BasicHttpRelay 传输属性**对话框中，在**消息**选项卡上，指定 SOAP 数据选择**正文**元素。  
  
    |使用此选项|执行的操作|  
    |--------------|----------------|  
    |**正文--BizTalk 请求消息正文**|使用 BizTalk 消息正文部分创建的 SOAP 内容**正文**传出消息的元素。<br /><br /> 这是默认设置。|  
    |**指定模板的模板--内容**|使用在“XML”  文本框中提供的模板创建传出消息的 SOAP **Body** 元素的内容。<br /><br /> 默认值为清除此复选框。|  
    |**XML**|键入 SOAP 的内容的 XML 格式模板**正文**的传出消息的元素。 如果选择了“模板 -- BizTalk 响应消息正文”  选项，则此属性是必需的。<br /><br /> 类型：字符串<br /><br /> 最小长度：0<br /><br /> 最大长度：32767<br /><br /> 默认值为 `<bts-msg-body xmlns="http://www.microsoft.com/schemas/bts2007" encoding="xml"/>`。|  
    |**信封--完整\<soap： 信封 >**|从传入消息的整个 SOAP **Envelope** 创建 BizTalk 消息正文部分。 此属性仅对要求-响应端口有效。<br /><br /> 默认值为清除此复选框。|  
    |**正文--内容\<soap： 正文 > 元素**|使用传入消息的 SOAP **Body** 元素的内容创建 BizTalk 消息正文部分。 如果 **Body** 元素具有多个子元素，则只有第一个元素将成为 BizTalk 消息正文部分。 此属性仅对要求-响应端口有效。<br /><br /> 这是默认设置。|  
    |**路径--由正文路径定位的内容**|使用“正文路径表达式”  文本框中的正文路径表达式创建 BizTalk 消息正文部分。 针对传入消息的 SOAP **Body** 元素的直接子元素计算正文路径表达式。 此属性仅对要求-响应端口有效。<br /><br /> 默认值为清除此复选框。|  
    |**正文路径表达式**|键入正文路径表达式以标识传入消息中用于创建 BizTalk 消息正文部分的特定部分。 此正文路径表达式针对 SOAP 的即时子元素进行评估**正文**传入消息的节点。 如果此正文路径表达式返回多个节点，则只选择第一个节点作为 BizTalk 消息正文部分。 如果选择了“路径 -- 按正文路径定位内容”  选项，则此属性是必需的。 此属性仅对要求-响应端口有效。<br /><br /> 类型：字符串<br /><br /> 最小长度：0<br /><br /> 最大长度：32767<br /><br /> 默认值为空字符串。|  
    |**节点编码**|指定 WCF BasicHttpRelay 发送适配器用于解码识别由正文路径表达式中的节点的编码类型**正文路径表达式**文本框。 如果选择了“路径 -- 按正文路径定位内容”  选项，则此属性是必需的。 此属性仅对要求-响应端口有效。 有效值包括：<br /><br /> - **Base64**: Base64 编码。<br /><br /> -                         **十六进制**： 十六进制编码。<br /><br /> -                         **字符串**： 文本编码的 utf-8<br /><br /> -                         **XML**: WCF 适配器使用由正文路径表达式中所选节点的外部 XML 创建 BizTalk 消息正文**正文路径表达式**文本框。<br /><br /> 默认值为“XML” 。|  
    |**传播故障消息**|选中此复选框可将无法执行出站处理的消息路由至某个订阅应用程序（例如其他接收端口或业务流程计划）。 清除此复选框可挂起失败的消息，并生成一个否定确认 (NACK)。 此属性仅对要求-响应端口有效。<br /><br /> 默认值为选中此复选框。|  
  
8.  单击**确定**和**确定**再次以保存设置。  
  
## <a name="add-a-proxy-to-the-send-handler"></a>将代理添加到发送处理程序

可以将代理添加到发送端口中或发送处理程序。 如果要在发送端口添加代理，则跳过此部分。

1.  在[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理控制台中，展开[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理，展开**BizTalk 组**，展开**平台设置**，然后展开**适配器**.  
  
2.  选择**WCF BasicHttpRelay**，然后选择发送处理程序。  
  
3.  在**适配器处理程序属性**上**常规**选项卡上，选择**属性**。  
  
4.  在**代理**选项卡上，执行以下操作。  
  
    |使用此选项|执行的操作|  
    |--------------|----------------|  
    |**使用代理**|指示此发送处理程序是否使用代理服务器。<br /><br /> 默认值为清除此复选框。|  
    |**Address**|指定代理服务器的地址。 使用**https**或**http**根据安全配置的方案。 此地址后面可跟冒号和端口号。 例如，http://127.0.0.1:8080。<br /><br /> 此属性，则需要值才**使用代理**选择。<br /><br /> 类型：字符串<br /><br /> 最大长度：256<br /><br /> 默认值为空字符串。|  
    |**用户名**|指定用于身份验证的用户名。 如果使用集成或基本验证，则用户名将包括域，即采用“域\用户名”格式。 如果使用摘要式身份验证，则用户名不包括域\\。<br /><br /> 此属性，则需要值才**使用代理**选择。<br /><br /> 类型：字符串<br /><br /> 最小长度：0<br /><br /> 最大长度：256<br /><br /> 默认值为空字符串。|  
    |**密码**|指定用于身份验证的密码。<br /><br /> 此属性，则需要值才**使用代理**选择。<br /><br /> 类型：字符串<br /><br /> 最小长度：0<br /><br /> 最大长度：256<br /><br /> 默认值为空字符串。|  
  
5.  单击**确定**直到退出所有对话框。  
  
## <a name="see-also"></a>另请参阅  
[SB 消息适配器](../core/sb-messaging-adapter.md)

[使用适配器](../core/using-adapters.md)