---
title: BizTalk Server 中的安全功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- BizTalk Server, security
- Master Secret server, security
- security, Master Secret server
- security, runtime
- security, data
- deploying, security
- security, configuring
- runtime, security
- security, security features
- security, messages
- security, access control
- security, about security
- access control
- security, deploying
- data, security
- messages, security
ms.assetid: 5ab15023-fa71-439e-b3aa-420fe28806fa
caps.latest.revision: 12
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9d904bc842cb04bdf9c1457440c838c8a78e5c8f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36992614"
---
# <a name="security-features-in-biztalk-server"></a>BizTalk Server 中的安全功能
Microsoft® BizTalk® Server 提供了一个标准网关以便在 Intranet 中或通过 Internet 发送和接收文档。 由于发往和从 BizTalk Server 发回的消息可能是业务关键信息，因此在传输消息时以及当 BizTalk Server 处理并存储消息时，采取措施保护这些消息及其所包含信息的安全非常重要。 本部分提供了有关 BizTalk Server 安全功能的信息，并介绍如何使用这些功能来确保数据和环境的安全。  
  
 BizTalk Server 采用以下措施来确保入站和出站消息的安全，确保运行时和配置信息的安全，以及确保与其他应用程序和系统进行安全地集成：  
  
 **消息安全**  
  
- 对消息的发件人进行验证。 BizTalk Server 能够进行身份验证 （通过证书信息或 Windows 集成的安全性） 的消息的发送方验证消息的发件人的身份。 有关详细信息，请参阅[入站消息身份验证](../core/inbound-message-authentication.md)。  
  
- 向消息的收件人进行授权。 BizTalk Server 收到消息后，可确定哪些流程和用户有权接收消息。 有关详细信息，请参阅[向消息收件人授权](../core/authorizing-the-receiver-of-a-message.md)。  
  
  **运行时和配置安全**  
  
- **访问控制和保护数据。** BizTalk Server 使用访问控制来确保 BizTalk Server 流程有适当的限制，并且对业务关键信息的访问受到了控制。 换句话说，BizTalk Server 确保用户和帐户具有完成任务所需的最小用户权限。 有关详细信息，请参阅[访问控制和数据安全性](../core/access-control-and-data-security.md)。  
  
  **集成的安全性**  
  
- 企业单一登录。 BizTalk Server 使用企业单一登录 (SSO) 确保对适配器、发送和接收位置所需的敏感配置信息进行加密，从而确保 BizTalk Server 以安全方式存储和传输此信息。 有关详细信息，请参阅[使用 SSO](../core/using-sso.md)。  
  
## <a name="see-also"></a>请参阅  
 [为 BizTalk Server 设计系统体系结构](../core/designing-the-system-architectures-for-biztalk-server.md)   
 [实现企业单一登录](../core/implementing-enterprise-single-sign-on.md)   
 [规划消息安全性](../core/planning-message-security.md)   
 [访问控制和数据安全性](../core/access-control-and-data-security.md)   
