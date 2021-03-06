---
title: SAP 适配器与 BizTalk Server 的安全 |Microsoft 文档
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- credentials, protecting
- Enterprise Single Sign-On
- security, when using BizTalk Server
- security, protecting credentials
- SSO
ms.assetid: 702cd0f9-d8e1-4dad-8774-b552481d5390
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 4689424deced097d901464263d75e5ae10e4b99f
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
ms.locfileid: "22217773"
---
# <a name="security-with-the-sap-adapter-and-biztalk-server"></a>SAP 适配器与 BizTalk Server 的安全
配置发送端口或接收端口 （位置） 时使用 BizTalk Server 管理控制台或使用[!INCLUDE[consumeadapterservlong](../../includes/consumeadapterservlong-md.md)]若要检索 BizTalk 解决方案的消息架构，必须提供凭据的 SAP 系统。 请务必在一个安全的方法，可帮助防止它们被暴露给潜在的恶意 actors 中提供这些凭据。 本主题讨论如何最安全地提供的凭据[!INCLUDE[adaptersap](../../includes/adaptersap-md.md)]BizTalk Server 解决方案。  
  
 BizTalk 解决方案的上下文中的安全的更多常规讨论是广泛的主题，以及不在本文档的范围。 有关如何使 BizTalk 解决方案更安全的信息，请参阅[安全和保护 BizTalk 消息](../../core/secure-and-protect-your-biztalk-messages.md)。  
  
## <a name="how-do-i-protect-credentials-when-i-use-the-consume-adapter-service-biztalk-project-add-in"></a>当我使用时如何保护凭据使用适配器服务 BizTalk Project 外接程序？  
 当你使用[!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]要检索 BizTalk 解决方案的消息架构，您必须提供用户名和密码 SAP 系统。 你应当只做这从**安全**选项卡上**配置适配器**对话框。 这可确保你的凭据将不显示在**Uri**字段[!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]对话框中，有权访问您的计算机屏幕的任何人都可以读取。 有关如何通过使用来检索消息架构的详细信息[!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]，包括如何的 SAP 系统输入用户名和密码，请参阅[获取 Visual Studio 中的 SAP 操作的元数据](../../adapters-and-accelerators/adapter-sap/get-metadata-for-sap-operations-in-visual-studio.md)。  
  
## <a name="how-do-i-protect-credentials-when-i-configure-a-send-port-or-a-receive-location"></a>如何保护凭据时配置发送端口或接收位置？  
 BizTalk 解决方案使用 Microsoft BizTalk WCF 自定义适配器来使用 WCF 服务。 [!INCLUDE[adaptersap_short](../../includes/adaptersap-short-md.md)]是使客户端可以使用 SAP 系统，就像它是 WCF 服务的 WCF 自定义绑定。 BizTalk 解决方案使用[!INCLUDE[adaptersap_short](../../includes/adaptersap-short-md.md)]通过发送端口和接收配置为使用 WCF 自定义适配器，这反过来，，配置为使用的位置[!INCLUDE[adaptersap_short](../../includes/adaptersap-short-md.md)]用作其传输方式。 有关如何配置发送端口和接收的端口 （接收位置），包括如何配置 WCF 自定义适配器的详细信息，请参阅[手动配置到 SAP 适配器的物理端口绑定](../../adapters-and-accelerators/adapter-sap/manually-configure-a-physical-port-binding-to-the-sap-adapter.md)。  
  
 配置中的 SAP 系统凭据**凭据**选项卡**WCF 自定义传输属性**对话框发送端口或从**其他**选项卡**WCF 自定义传输属性**对话框接收位置。 由于 WCF 自定义适配器支持企业单一登录 (SSO)，你可以选择这些选项卡中的任何一个提供用户名和密码或 SSO 关联应用程序。 以下主题讨论这两个选项。  
  
### <a name="user-name-password-credentials"></a>用户名密码凭据  
 你应仅提供用户名和密码从**凭据**选项卡 （对于发送端口） 或**其他**选项卡 （用于接收位置） 中**WCF 自定义传输属性**对话框。 这可确保以下项：  
  
-   你的凭据将不会显示在**Uri**对话框中的字段。 这可以阻止有权访问你的屏幕 （或具有权限，使他们能够查看发送端口或接收位置属性） 的那些看到你的凭据。  
  
-   如果导出发送端口或接收端口绑定，你的密码将不写入到绑定文件中。 这将禁止所有人具有访问权限到文件中查看你的密码。  
  
### <a name="enterprise-single-sign-on-and-sso-affiliate-applications"></a>企业单一登录和 SSO Affiliate 应用程序  
 你可以配置 WCF 自定义适配器以使用 SSO 以获取有关 SAP 系统的凭据。 SSO 使用数据库和主密钥进行加密和存储用户凭据。 它还提供服务，以 Microsoft Windows 帐户映射到用于访问后端系统的辅助凭据。 通过使用 SSO，你可以映射到的用户名和密码 SAP 系统上的 Windows 帐户。  
  
 SSO 使用*affiliate 应用程序*和*SSO 映射*映射到后端系统的凭据。 关联应用程序是指系统或需要辅助凭据的应用程序的 sso 的逻辑实体。 SSO 映射是与关联应用程序相关联。 它映射到该帐户用于访问关联系统或应用程序的辅助凭据的 Windows 帐户。 SSO 映射可以与 Windows 用户帐户或与组相关联。  
  
 若要使用具有 SSO [!INCLUDE[adaptersap_short](../../includes/adaptersap-short-md.md)]，你必须执行以下操作。  
  
1.  在 SSO 来保留名称为 SAP 系统的密码凭据的用户中创建关联应用程序。 通常由拥有 SSO 管理权限的特殊类型执行此步骤。  
  
2.  创建一个用户或组映射将您的 Windows 帐户映射到的用户的关联应用程序和用于建立与 SAP 系统的连接的密码。 具体取决于你的安装，用户可能能够执行此步骤，或它可能需要具有特殊类型的 SSO 管理权限的人员。  
  
> [!NOTE]
>  为 SSO 配置时，WCF 自定义适配器使用提供的 SSO 服务从 SSO 数据库中获取的 SAP 用户名和密码。 它提供了这些 （未加密的） 到[!INCLUDE[adaptersap_short](../../includes/adaptersap-short-md.md)]，以便该适配器可以打开与 SAP 系统的连接。 SSO 跨之间的连接提供任何加密或保护[!INCLUDE[adaptersap_short](../../includes/adaptersap-short-md.md)]和 SAP 系统。  
  
 有关如何使用 SSO，包括有关如何创建关联应用程序和 SSO 映射信息的信息请参阅[使用 SSO](../../core/using-sso.md)。 有关 SSO 的更多常规信息，请参阅[实现 Enterprise 上单一登录](../../core/implementing-enterprise-single-sign-on.md)。  
  
## <a name="the-acceptcredentialsinuri-binding-property"></a>AcceptCredentialsInUri 绑定属性  
 [!INCLUDE[adaptersap_short](../../includes/adaptersap-short-md.md)]曲面**AcceptCredentialsInUri**绑定属性。 此属性确定是否允许连接 URI 中使用 SAP 系统凭据。 默认情况下， **AcceptCredentialsInUri**是**false**和[!INCLUDE[adaptersap_short](../../includes/adaptersap-short-md.md)]URI 中包括凭据时引发异常。  
  
 此属性是因为存在某些编程方案中需要的凭据必须存在于连接 URI 显示中。 这应永远不会是这种情况，在您配置发送端口或接收位置，或当你使用[!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]检索消息架构从[!INCLUDE[adaptersap_short](../../includes/adaptersap-short-md.md)]。 在这种情况下，建议你不要设置**AcceptCredentialsInUri**到**true**。 有关详细信息[!INCLUDE[adaptersap_short](../../includes/adaptersap-short-md.md)]绑定属性，请参阅[了解针对 ORacle E-business Suite 绑定属性的 BizTalk 适配器](../../adapters-and-accelerators/adapter-oracle-ebs/read-about-the-biztalk-adapter-for-oracle-e-business-suite-binding-properties.md)。  
  
 **AcceptCredentialsInUri**绑定属性中不可用[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]中**绑定**选项卡上配置 WCF 自定义或 WCF SAP 时接收或发送端口。 若要设置的值**AcceptCredentialsInUri**绑定属性，则必须打开后已生成元数据中使用创建的适配器绑定文件 （XML 文件） [!INCLUDE[consumeadapterservshort](../../includes/consumeadapterservshort-md.md)]，然后找到中的此绑定属性该文件。 指定此绑定属性适当的值，保存该绑定文件，然后导入中的绑定文件[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]。 请参阅[重用 SAP 适配器绑定](../../adapters-and-accelerators/adapter-sap/reuse-sap-adapter-bindings.md)有关的说明。  
  
## <a name="see-also"></a>另请参阅  
[最佳做法来保护 SAP 适配器](../../adapters-and-accelerators/adapter-sap/best-practices-to-secure-the-sap-adapter.md)  
 [保护你的 SAP 应用程序](../../adapters-and-accelerators/adapter-sap/secure-your-sap-applications.md)   