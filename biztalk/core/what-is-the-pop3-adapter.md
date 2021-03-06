---
title: POP3 适配器概述 | Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- POP3 adapters, availability
- authenticating, POP3 adapters
- POP3 adapters, data duplication
- data duplication
- POP3 adapters, receive adapters
- high availability, POP3 adapters
- POP3 adapters, supported platforms
- POP3 adapters, authenticating
- POP3 adapters, algorithims
- receive adapters, POP3 adapters
ms.assetid: 05e9598b-cdfe-4216-b6bf-1b84f8ddfeae
caps.latest.revision: 30
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: aa0f4679cb898f9ce2c4008505bd1ec4a2540dab
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36974326"
---
# <a name="what-is-the-pop3-adapter"></a>POP3 适配器概述
本部分将介绍 POP3 接收适配器。  
  
## <a name="pop3-receive-adapter"></a>POP3 接收适配器  
 使用 POP3 接收适配器，可以将数据从启用 POP3 的邮箱移至 BizTalk Server。  
  
 POP3 接收适配器的主要功能包括：  
  
-   根据需要从 POP3 服务器邮箱请求文件。  
  
-   根据可配置计划运行轮询。  
  
-   对 POP3 服务器邮箱进行轮询并将数据直接发送到 BizTalk Server。  
  
-   将 POP3 服务器邮箱指定为 IP 地址、主机名、端口、用户名或密码。  
  
-   能够从需要安全套接字层 (SSL) 连接的邮件服务器中下载电子邮件。  
  
-   确保文件送达。  
  
-   隐式 MIME 处理。 使用 POP3 适配器时，无需在接收管道中使用 MIME 解码器。  
  
## <a name="pop3-adapter-supported-platforms"></a>POP3 适配器支持的平台  
 POP3 适配器设计为与符合以下 RFC 的任何 POP3 服务器协同工作：  
  
- **RFC 1939。** 邮局协议版本 3 (请参阅[ http://go.microsoft.com/fwlink/?LinkId=58808 ](http://go.microsoft.com/fwlink/?LinkId=58808))  
  
- **RFC 1734。** POP3 身份验证命令 (请参阅[ http://go.microsoft.com/fwlink/?LinkId=58809 ](http://go.microsoft.com/fwlink/?LinkId=58809))  
  
- **RFC 2045。** 多用途 Internet 邮件扩展 (MIME) 第一部分： Internet 消息正文格式 (请参阅[ http://go.microsoft.com/fwlink/?LinkId=58810 ](http://go.microsoft.com/fwlink/?LinkId=58810))  
  
- **RFC 2046。** 多用途 Internet 邮件扩展 (MIME) 第二部分： 媒体类型 (请参阅[ http://go.microsoft.com/fwlink/?LinkId=58811 ](http://go.microsoft.com/fwlink/?LinkId=58811))  
  
- **RFC 最多允许 2047年。** 非 ASCII 文本的 MIME （多用途 Internet 邮件扩展） 第三部分： 消息标头扩展 (请参阅[ http://go.microsoft.com/fwlink/?LinkId=58812 ](http://go.microsoft.com/fwlink/?LinkId=58812))  
  
  根据 Microsoft Exchange Server 2003 对 POP3 适配器进行了大量的测试。  
  
## <a name="considerations-for-preventing-data-duplication-when-using-the-pop3-adapter"></a>使用 POP3 适配器时防止数据重复的注意事项  
 POP3 适配器不是事务性适配器，因此可能出现处理同一消息的多个副本的情况，这可能导致数据重复。 在以下情况中，POP3 适配器可能会传送消息的重复副本：  
  
-   在电子邮件已成功提交到 BizTalk Server 以进行处理后，POP3 适配器将始终从配置为要监视的邮箱中删除电子邮件。 如果 POP3 适配器从邮箱中检索到电子邮件并将其提交给 BizTalk Server 以便进行处理，但未能从邮箱中删除该电子邮件，那么，在 POP3 适配器下一次轮询该邮箱时，会将该电子邮件重新提交给 BizTalk Server。  
  
-   如果位于单独 BizTalk 主机实例中的多个 POP3 适配器实例正在同时监视同一个邮箱，并且 POP3 服务器允许与其邮箱进行多个并行连接，则该适配器可能传送消息的重复副本。  
  
## <a name="high-availability-for-the-pop3-adapter"></a>POP3 适配器的高可用性  
 某些 POP3 服务器允许与给定邮箱进行多个并行连接。 如果将多个 POP3 适配器实例配置为从此类 POP3 服务器上的邮箱中检索邮件，则可能出现数据重复。 因此，应当只将一个 POP3 适配器实例配置为从允许多个并行连接的邮箱中检索邮件。  
  
 若要为此方案中的 POP3 适配器提供容错功能，则应将单个 POP3 适配器接收处理程序配置为在群集 BizTalk 主机中运行。 有关详细信息请参阅[群集主机内运行适配器处理程序的注意事项](../core/considerations-for-running-adapter-handlers-within-a-clustered-host1.md)。  
  
## <a name="authentication-warnings-when-multiple-instances-of-the-pop3-adapter-connect-to-the-same-mailbox"></a>多个 POP3 适配器实例连接到同一邮箱时的验证警告  
 可以将 BizTalk Server 配置为允许多个 POP3 适配器实例从同一邮箱中检索邮件。 在这种情况下，由于某些 POP3 服务器采用了锁定机制，因此在 BizTalk Server 应用程序日志中可能生成验证警告。 这些警告对于 POP3 适配器功能没有影响，因而在此方案中可以安全地将其忽略。  
  
## <a name="encrypted-messages-received-by-the-pop3-adapter-that-are-sent-to-the-suspended-queue-may-be-viewable-in-clear-text"></a>由 POP3 适配器接收的加密消息（发送到挂起队列）的明文形式可能允许查看  
 您可以对 POP3 适配器进行配置，对经数字加密的电子邮件进行解密。 这是通过设置**应用 MIME 解码**属性设置为**True**的接收位置，使用 POP3 适配器。 如果 POP3 适配器收到经数字加密的电子邮件并**应用 MIME 解码**接收位置属性设置为**True** POP3 适配器尝试解密该电子邮件，如下所示：  
  
- 该 POP3 适配器将搜索与用来加密电子邮件的公钥证书相匹配的私钥证书。 该私钥证书必须位于运行指定主机实例（与 POP3 接收处理程序绑定）的服务器的个人证书存储区中。  
  
- 如果 POP3 适配器找到相应的私钥证书，它将使用该私钥证书解密电子邮件。  
  
- 该电子邮件将被解密并保存到 BizTalk MessageBox 中。  
  
  如果一个消息经过解密并保存到 BizTalk MessageBox 中后被挂起，则在 BizTalk 挂起队列中，消息内容的明文形式将是可见的。  
  
  如果要阻止安全消息文本显示在挂起队列中，请执行以下步骤：  
  
- 设置**应用 MIME 解码**属性设置为**False**为该使用 POP3 适配器接收位置和解密使用 SMIME 管道组件的管道中的消息。  
  
  > [!NOTE]
  >  此方法将阻止您将特定于电子邮件的属性升级到消息上下文中。  
  
- 如果要将特定于电子邮件的属性应用到消息的上下文中，并要确保加密消息被路由到挂起队列时仍处于加密状态，请执行以下步骤：  
  
  -   选中选项**失败消息启用路由功能**使用 POP3 适配器的接收位置所在接收端口上。  
  
  -   创建一个业务流程，以订阅在传输到使用 POP3 适配器的接收位置所在接收端口时失败的消息。  
  
  -   为该业务流程配置一个可使用 SMIME 管道组件在管道中加密消息的发送端口。  
  
  -   为该业务流程配置一个挂起形状，以挂起业务流程实例和消息。  
  
  -   生成并部署该业务流程，然后将已部署的业务流程绑定到适当的接收端口。  
  
## <a name="maximum-message-size-supported-by-the-pop3-adapter"></a>POP3 适配器支持的最大消息大小  
 经测试，POP3 适配器支持接收大小不超过 50 MB 的消息。  
  
## <a name="see-also"></a>请参阅  
 [POP3 适配器](../core/pop3-adapter.md)