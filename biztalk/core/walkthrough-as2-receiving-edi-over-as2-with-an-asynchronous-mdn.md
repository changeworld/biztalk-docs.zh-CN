---
title: "演练 (AS2): 通过使用异步 MDN 的 AS2 接收 EDI |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ac3962e4-0525-4194-8cf1-b90664f1a139
caps.latest.revision: "40"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a0dd9e94ff74adb4419f95b386861376bb424fd1
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="walkthrough-as2-receiving-edi-over-as2-with-an-asynchronous-mdn"></a>演练 (AS2)：使用异步 MDN 通过 AS2 接收 EDI
本演练将介绍创建一个通过 AS2 传输方法接收 EDI 消息并返回异步 MDN 的解决方案的分步操作过程。  
  
## <a name="prerequisites"></a>先决条件  
 以下为执行本主题中的过程的前提条件：  
  
-   必须以 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理员组或 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] B2B Operators 组成员的身份登录。  
  
-   运行演练的计算机必须安装了 Internet 信息服务 (IIS)。  
  
-   如果运行此演练的计算机安装了 64 位版本的 Windows，则您必须确保 BizTalk 主机标记只能为 32 位。 您还必须确保 IIS 已将“为应用程序池启用 32 位应用程序设置”设置为 True。  有关详细信息，请参阅[教程 3: AS2 教程](../core/tutorial-3-as2-tutorial.md)。  
  
## <a name="how-the-solution-receives-an-edi-interchange-and-returns-an-asynchronous-mdn"></a>解决方案如何接收 EDI 交换并返回异步 MDN  
 该解决方案将执行以下操作：  
  
1.  从贸易合作伙伴通过 HTTP 接收包含有 EDI 交换的 AS2 消息，并对来自 EDIINT/AS2 的交换进行解码。  
  
    > [!NOTE]
    >  此列表中的事件可能不会按所示顺序发生。  
  
2.  生成 MDN 响应，并将其放置到 MessageBox 中。  
  
3.  通过动态发送端口提取消息 MDN。  
  
4.  将异步消息 MDN 返回到贸易合作伙伴。  
  
5.  将 EDI 格式的交换转换为内部 XML 格式，并将其放在 MessageBox 中。  
  
6.  具有 PassThruTransmit 管道的发送端口将从 MessageBox 提取消息 XML 文件。  
  
7.  该发送端口将 EDI 交换 XML 文件发送到 Contoso 参与方的某一文件夹。  
  
 下图显示出此解决方案的结构。  
  
 ![与异步 MDN 的 AS2 接收](../core/media/bts-configuring-the-receiving-of-edi-over-as2-with-an-asynchronous-mdnc.gif "bts_Configuring_the_Receiving_of_EDI_Over_AS2_with_an_Asynchronous_MDNc")  
  
## <a name="the-functionality-in-this-solution"></a>此解决方案中的功能  
 本演练的功能具有以下特点：  
  
-   不会生成 EDI 确认。 生成 EDI 确认进行了演示[演练 (X12)： 接收 EDI 交换和发送回确认](../core/walkthrough-x12--receive-edi-interchanges-and-send-back-an-acknowledgement.md)。 中所述通过 AS2 传输发送 EDI 确认[演练 (AS2): 通过使用异步 MDN 的 AS2 发送 EDI](../core/walkthrough-as2-sending-edi-over-as2-with-an-asynchronous-mdn.md)。  
  
-   该解决方案专用于使用 X12 编码而不是 EDIFACT 编码的交换。  
  
    > [!NOTE]
    >  用于 EDIFACT 编码的配置与用于 X12 编码的配置几近相同。  
  
-   EDI 类型和扩展的验证将在传入交换上执行。  
  
-   系统将启用 AS2 和 EDI 报告功能，并保存事务集以从交换状态报告进行查看。  
  
-   此解决方案不在不可否认数据库中配置签名、压缩、加密或消息存储。 有关配置这些属性的过程，请参阅[配置 AS2 属性](../core/configuring-as2-properties.md)。  
  
## <a name="configuring-and-testing-the-walkthrough"></a>配置和测试演练  
 该解决方案所需的过程包括：  
  
-   使用所需的消息架构生成并部署 BizTalk 项目，并将 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 设置为在处理接收的交换时使用这些架构。  
  
-   启用接收 AS2 消息时使用的 BTS ISAPI 筛选器。  
  
-   按照接收位置中的配置，创建一个用于从 Fabrikam 接收 AS2 消息的 Contoso 虚拟目录。  
  
-   创建一个用于从 Contoso 接收 MDN 的 Fabrikam 虚拟目录。  
  
-   指定 Windows SharePoint Services 不管理 Contoso 和 Fabrikam 虚拟目录。  
  
-   为 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 创建一个静态单向 HTTP 接收端口以从贸易合作伙伴接收包含 EDI 业务文档的 AS2 消息。 将接收管道配置为 AS2EDIReceive 管道。  
  
-   为 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 创建一个动态单向 HTTP 发送端口以发送对应于所接收 AS2 消息的 MDN。  
  
    > [!NOTE]
    >  此发送端口基于 EdiIntAS.IsAS2AsynchronousMDN 属性（由 AS2EdiReceive 管道设置为 True）和相关标记订阅 MDN。 发送端口必须是动态的，因此它将向消息标头的 Receipt-Delivery-Notification 行中的地址发送该 MDN。  
  
-   创建静态单向 FILE 发送端口以将 EDI 负载（XML 格式）发送到本地文件夹。 创建本地文件夹。  
  
-   为 Fabrikam 和 Contoso 创建参与方（贸易合作伙伴）。  
  
-   为这两个贸易方创建业务配置文件每个。  
  
-   在 Fabrikam 和 Contoso 的业务配置文件之间创建一个 AS2 协议。 AS2 协议中将包含发送 AS2 消息并接收返回的异步 MDN 的属性。  
  
-   创建 X12 协议之间的业务配置文件，Fabrikam 和 Contoso 接收 X12 消息。  
  
-   通过使用提供的是 HTTP 发件人实用工具 AS2 教程文件的一部分测试解决方案。 该实用工具将通过 AS2 传输类型发送一条包含 EDI 交换的测试 AS2 消息。 该实用工具通过 AS2 传输方法发送一条包含有 EDI 交换的测试 AS2 消息（X12_00401_864.edi，也包括在 AS2 教程中）。 在此演练中使用的 HTTP 发送实用工具和测试消息与交付用于本教程的版本相同。  
  
### <a name="configuring-the-walkthrough"></a>配置演练  
 本部分介绍配置演练的步骤。  
  
##### <a name="to-deploy-the-message-schema"></a>部署消息架构  
  
1.  在 [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] 中，打开项目 [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]SDK\AS2 Tutorial\Schemas\Schemas.btproj。  
  
    > [!NOTE]
    >  此项目随 AS2 教程一起提供，其中包括一个 864 架构以与测试消息一起使用。  
  
    > [!NOTE]
    >  本主题假定你已从你的应用程序添加了对包含 EDI 架构、管道和业务流程的 BizTalk EDI 应用程序的引用。 如果没有，请参阅[如何添加对 BizTalk Server EDI 应用程序的引用](http://msdn.microsoft.com/library/7af066fb-372f-4709-b566-c8d6b4a9d782)。  
  
2.  右键单击**架构**项目在解决方案资源管理器，，然后单击**属性**。 单击**签名**在项目设计器中，检查的选项卡**对程序集签名**复选框，然后从下拉列表中选择**新建**并提供所需的值创建强名称密钥文件。 保存所做的更改并关闭项目属性窗口。  
  
3.  生成并部署 Schemas.btproj。  
  
##### <a name="to-enable-the-bts-isapi-filter"></a>启用 BTS ISAPI 筛选器  
  
1.  单击**启动**，指向**所有程序**，指向**管理工具**，然后单击**Internet Information Services (IIS) Manager**.  
  
    > [!TIP]
    >  具体取决于操作系统，管理工具开始菜单选项可能不可用。 在这种情况下，单击**启动**，单击**运行**，并输入`inetmgr`若要打开 Internet 信息服务 (IIS) 管理器。  
  
2.  选择的根 Web 服务器条目并在**功能视图**，双击**处理程序映射**然后在操作窗格中单击**添加脚本映射**。  
  
    > [!NOTE]
    >  在 Web 服务器级别配置的脚本映射将导致此映射将应用于所有子网站。 如果你想要限制映射到特定的网站或虚拟文件夹，选择目标站点或而不是 Web 服务器的文件夹。  
  
3.  在**添加脚本映射**对话框框中，输入`BtsHttpReceive.dll`中**请求路径**字段。  
  
4.  在**可执行文件**字段中，单击**省略号 （...）**按钮，然后浏览到[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]HttpReceive。 选择 BtsHttpReceive.dll，然后单击**确定**。  
  
5.  输入`BizTalk HTTP Receive`中`Name`字段，然后再单击**请求限制**。  
  
6.  在请求限制对话框中，选择**谓词**选项卡上，然后选择**的以下谓词之一**。 输入`POST`作为谓词。  
  
7.  上**访问**选项卡上，选择**脚本**，然后单击**确定**。  
  
8.  单击**确定**出现提示时允许 ISAPI 扩展插件，则单击**是**。  
  
##### <a name="to-configure-the-contoso-web-page"></a>配置 Contoso 网页  
  
1.  在 IIS 管理器中，右键单击**应用程序池**和选择**添加应用程序池**。  
  
2.  在**添加应用程序池**对话框框中，输入**BizTalkAppPool**中**名称**，然后选择**.NET Framework V4.0.30210**中**.NET framework 版本**下拉列表。 单击 **“确定”**。  
  
    > [!NOTE]
    >  根据计算机上安装的 [!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)] 版本，.NET Framework 的版本可能会有所不同。  
  
3.  选择**应用程序池**，在功能视图选择**BizTalkAppPool**，然后单击**高级设置**中**操作**窗格。  
  
4.  在**高级设置**对话框中，选择**标识**，然后单击**省略号 （...）**按钮。  
  
5.  在**应用程序池标识**对话框中，选择**自定义帐户**，然后单击**设置**。  
  
6.  输入**用户名**和**密码**是 administrators 组的成员的用户帐户，输入中的密码**确认密码**，然后单击**确定**三次以返回到 IIS 管理器。  
  
7.  在 IIS 管理器中，打开**站点**文件夹。 右键单击**Default Web Site**节点，，然后选择**添加应用程序**。  
  
8.  在**添加应用程序**对话框框中，输入**Contoso**中**别名**文本中，然后单击**选择**。  
  
9. 在**选择应用程序池**对话框中，选择**BizTalkAppPool**单击**确定**。  
  
10. 有关**物理路径**，单击**省略号 （...）**按钮，然后浏览到[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]HttpReceive。  
  
11. 单击**测试设置**并验证没有显示在错误**测试连接**对话框。 单击 **“关闭”**，然后单击 **“确定”**。  
  
12. 在 IIS 管理器中，选择 Contoso 虚拟目录和在**功能视图**，双击**身份验证**。  
  
13. 在**身份验证**页上，选择**匿名身份验证**并确认**状态**是**已启用**。 如果**状态**是**禁用**，单击**启用**中**操作**窗格。  
  
##### <a name="to-configure-the-fabrikam-web-page"></a>配置 Fabrikam 网页  
  
1.  在 IIS 管理器中，打开**站点**文件夹。 右键单击**Default Web Site**节点，，然后选择**添加应用程序**。  
  
2.  在**添加应用程序**对话框框中，输入**Fabrikam**中**别名**，然后单击**选择**。  
  
3.  在**选择应用程序池**对话框中，选择**BizTalkAppPool**单击**确定**。  
  
4.  有关**物理路径**，单击**省略号 （...）**按钮，然后浏览到[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]SDK\AS2 Tutorial\Fabrikam。  
  
5.  单击**测试设置**并验证没有显示在错误**测试连接**对话框。 单击 **“关闭”**，然后单击 **“确定”**。  
  
6.  在 IIS 管理器中，选择 Contoso 虚拟目录和在**功能视图**，双击**身份验证**。  
  
7.  在**身份验证**页上，选择**匿名身份验证**并确认**状态**是**已启用**。 如果**状态**是**禁用**，单击**启用**中**操作**窗格。  
  
##### <a name="to-specify-that-your-virtual-directory-is-not-managed-by-windows-sharepoint-services"></a>指定虚拟目录不由 Windows SharePoint Services 托管  
  
1.  如果您的计算机上安装 Windows SharePoint Services，请单击**启动**，指向**所有程序**，指向**管理工具**，然后单击**SharePoint 3.0 管理中心**。  
  
    > [!NOTE]
    >  如果用于设置演练的同一计算机上还安装了 Windows SharePoint Server，则此过程是必需的。 在该情况下，您必须指定 IIS 虚拟目录不由 Windows SharePoint Server 托管。  
  
2.  上**管理中心**页上，在**管理中心**，单击**应用程序管理**。  
  
3.  上**应用程序管理**页上，单击**定义管理路径**。  
  
4.  在**定义管理路径**页上，在**添加新路径**中**路径**文本框中，输入**Contoso**。 下**类型**，单击**排除路径**，然后单击**确定**。  
  
5.  请为 Fabrikam 虚拟目录重复步骤 4。  
  
##### <a name="to-create-a-receive-port-to-receive-the-edi-interchange-over-as2-from-fabrikam"></a>创建接收端口以通过 AS2 从 Fabrikam 接收 EDI 交换  
  
1.  在[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理控制台中，右键单击**接收端口**节点下的**BizTalk 应用程序 1**节点，指向**新建**，然后单击**单向接收端口**。  
  
2.  将接收端口，然后单击**接收位置**在控制台树中。  
  
3.  单击 **“新建”**。  
  
4.  名称的接收位置中，选择**HTTP**为**类型**，然后单击**配置**。  
  
5.  有关**虚拟目录以及 ISAPI 扩展**，输入`/Contoso/BTSHTTPReceive.dll`。  
  
6.  选择**挂起失败的请求**复选框，然后单击**确定**。  
  
7.  有关**接收管道**，选择**AS2EDIReceive**。  
  
8.  单击**确定**，然后单击**确定**试。  
  
9. 在**接收位置**窗格[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理控制台中，右击接收位置，然后单击**启用**。  
  
##### <a name="to-create-a-dynamic-send-port-to-send-the-mdn-to-fabrikam"></a>创建动态发送端口将 MDN 发送至 Fabrikam  
  
1.  在[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理控制台中，右键单击**发送端口**节点下的**BizTalk 应用程序 1**节点，指向**新建**，然后单击**动态单向发送端口**。  
  
2.  在**发送端口属性**对话框中，名称发送端口。  
  
3.  有关**发送管道**，选择**AS2Send**。  
  
4.  在控制台树中，选择**筛选器**。 有关**属性**，输入**EdiIntAS.IsAS2AsynchronousMDN**; 对于**运算符**，输入 **==** ; 以及**值**，输入**True**。  
  
5.  单击 **“确定”**。  
  
##### <a name="to-create-a-send-port-to-send-the-edi-payload-to-a-local-folder"></a>创建用于将 EDI 负载发送到本地文件夹的发送端口  
  
1.  在 Windows 资源管理器，创建一个名为 Contoso 本地文件夹**EDI_to_Contoso**发送 EDI 负载。  
  
2.  在[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理控制台中，右键单击**发送端口**，指向**新建**，然后单击**静态单向发送端口**。  
  
3.  在**发送端口属性**对话框中，你发送端口，例如，名称**Send_Payload**。 选择**文件**为**类型**，然后单击**配置**。  
  
4.  在**文件传输属性**对话框中，为**目标文件夹**，浏览到并选择**EDI_to_Contoso**步骤 1 中创建的文件夹。 保留**文件名**作为**%MessageID%.xml**。 单击 **“确定”**。  
  
5.  接受默认的**PassThruTransmit**为**发送管道**。  
  
6.  单击**筛选器**在控制台树中。 有关**属性**，输入**BTS。MessageType**。 有关**运算符**，输入 **==** 。 有关**值**，电子邮件中，输入消息类型`http://schemas.microsoft.com/BizTalk/Edi/X12/2006#X12_00401_864`。  
  
7.  单击 **“确定”**。  
  
8.  在**发送端口**窗格[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理控制台中，右击发送端口，然后单击**启动**。  
  
##### <a name="to-create-a-party-and-a-business-profile-for-fabrikam"></a>若要为 Fabrikam 创建方和业务配置文件  
  
1.  右键单击**方**中的节点[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理控制台中，依次指向**新建**，然后单击**方**。  
  
2.  输入的名称在方**名称**文本中，然后单击**确定**。  
  
    > [!NOTE]
    >  通过选择**本地 BizTalk 处理接收的消息从该参与方发送方或支持消息**复选框，你可以指定当事方正在创建将为同一个组织还承载[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]. 此基础，某些属性将启用，或当您创建了协议时，禁用。 但是，对于本演练中，可以选中此复选框。  
  
3.  右键单击方名称，指向**新建**，然后单击**业务配置文件**。  
  
4.  在**配置文件属性**对话框中，在**常规**页上，输入**Fabrikam_Profile**中**名称**文本框。  
  
    > [!NOTE]
    >  在创建参与方时，也将创建一个配置文件。 你可以重命名，并使用该配置文件而不是创建一个新。 若要重命名配置文件，右键单击配置文件，然后选择**属性**。 在**常规**页上，指定配置文件的名称。  
  
##### <a name="to-create-a-party-and-a-business-profile-for-contoso"></a>为 Contoso 创建参与方和业务配置文件  
  
1.  右键单击**方**中的节点[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理控制台中，依次指向**新建**，然后单击**方**。  
  
2.  输入的名称在方**名称**文本中，然后单击**确定**。  
  
    > [!NOTE]
    >  通过选择**本地 BizTalk 处理接收的消息从该参与方发送方或支持消息**复选框，你可以指定当事方正在创建将为同一个组织还承载[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]. 此基础，某些属性将启用，或当您创建了协议时，禁用。 但是，对于本演练中，可以选中此复选框。  
  
3.  右键单击方名称，指向**新建**，然后单击**业务配置文件**。  
  
4.  在**配置文件属性**对话框中，在**常规**页上，输入**Contoso_Profile**中**名称**文本框。  
  
    > [!NOTE]
    >  在创建参与方时，也将创建一个配置文件。 你可以重命名，并使用该配置文件而不是创建一个新。 若要重命名配置文件，右键单击配置文件，然后选择**属性**。 在**常规**页上，指定配置文件的名称。  
  
##### <a name="to-create-an-as2-agreement-between-the-two-business-profiles"></a>在两个业务配置文件之间创建 AS2 协议  
  
1.  右键单击**Fabrikam_Profile**，指向**新建**，然后单击**协议**。  
  
2.  在**常规属性**页上，为**名称**文本框中，输入协议的名称。  
  
3.  从**协议**下拉列表中，选择**AS2**。  
  
4.  在**第二个合作伙伴**部分中，从**名称**下拉列表中，选择**Contoso**。  
  
5.  在**第二个合作伙伴**部分中，从**配置文件**下拉列表中，选择**Contoso_Profile**。  
  
     你将注意到两个新选项卡获取旁边添加**常规**选项卡。每个选项卡用于配置一个单向 AS2 协议。  
  
6.  在**常规**选项卡上，在**常规属性**页上，在**常见主机设置**部分中，选择**打开 reporting**。  
  
7.  在上执行以下任务**Fabrikam-> Contoso**选项卡。  
  
    1.  上**标识符**页上，输入值**AS2-从**和**AS2-到**。 有关**AS2-从**，输入`Fabrikam`。 有关**AS2-到**，输入`Contoso`。  
  
    2.  上**验证**页上，选择**使用验证和 MDN 的协议设置，而不是消息标头**复选框  
  
    3.  在**确认 (Mdn)**页上，执行以下操作：  
  
        1.  选择**请求 MDN**复选框。  
  
        2.  请确保**请求签名的 MDN**清除复选框。  
  
        3.  选择**请求异步 MDN**复选框。  
  
        4.  在**回执送达选项 (URL)**文本框中，输入`http://localhost/Fabrikam/Default.aspx?Destination=_MDNToFabrikam`。  
  
8.  在上执行以下任务**Contoso-> Fabrikam**选项卡。  
  
    > [!NOTE]
    >  在此演练中，我们将指定的选项卡中所需的值，以便可以成功创建协议。 若要成功创建了协议，这两个单向协议选项必须为定义的值**AS2-从**和**AS2-到**。  
  
    1.  上**标识符**页上，输入值**AS2-从**和**AS2-到**。 有关**AS2-从**，输入`Contoso`。 有关**AS2-到**，输入`Fabrikam`。  
  
9. 单击 **“应用”**。  
  
10. 单击 **“确定”**。 新添加的协议被列入**协议**部分**方和业务配置文件**窗格。 默认情况下，启用新添加的协议。  
  
##### <a name="to-create-an-x12-agreement-between-the-two-business-profiles"></a>在两个业务配置文件之间创建 X12 协议  
  
1.  右键单击**Fabrikam_Profile**，指向**新建**，然后单击**协议**。  
  
2.  在**常规属性**页上，为**名称**文本框中，输入协议的名称。  
  
3.  从**协议**下拉列表中，选择**X12**。  
  
4.  在**第二个合作伙伴**部分中，从**名称**下拉列表中，选择**Contoso**。  
  
5.  在**第二个合作伙伴**部分中，从**配置文件**下拉列表中，选择**Contoso_Profile**。  
  
     你将注意到两个新选项卡获取旁边添加**常规**选项卡。每个选项卡可用于配置一个单向 X12 协议。  
  
6.  在**常规**选项卡上，在**常规属性**页上，在**常见主机设置**部分中，选择**打开 reporting**，，然后选择**用于报告的应用商店消息负载**。  
  
7.  在上执行以下任务**Fabrikam-> Contoso**选项卡。  
  
    1.  上**标识符**下页上**交换设置**部分中，输入限定符和标识符字段的值 (**ISA5**， **ISA6**， **ISA7**，和**ISA8**) 对应于测试消息中这些标头字段的值。  
  
        > [!NOTE]
        >  [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 要求为发送方和接收方的限定符和标识符字段输入值才能执行协议解析。 它将与匹配的值**ISA5**， **ISA6**， **ISA7**，和**ISA8**与协议的属性中的交换标头中。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]此外将匹配的发件人限定符和 （而不是收件人限定符和标识符） 的标识符来解析协议。 如果 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 无法解析协议，则将使用后备协议属性。  
  
        > [!NOTE]
        >  对于本演练中，设置**ISA5**到**ZZ**， **ISA6**到**7654321**， **ISA7**到**ZZ**，和**ISA8**到**1234567**。  
  
    2.  上**验证**下页上**交换设置**部分中，请确保**检查重复的 isa13**选项处于未选中状态。  
  
        > [!NOTE]
        >  清除**检查重复的 isa13**属性使您能够接收同一消息的多个实例。  
  
    3.  如果你使用其中一个标准架构附带[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]上**本地主机设置**下页上**事务设置设置**部分中，选择要用于对架构的命名空间处理传入的交换。  
  
        |使用此选项|执行的操作|  
        |--------------|----------------|  
        |**Default**|选中列中的复选框|  
        |**目标 Namespace**|选择 `http://schemas.microsoft.com/BizTalk/EDI/X12/2006`。|  
  
        > [!NOTE]
        >  设置属性可以使 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 确定处理传入 850 交换时使用的架构。 如果某一交换的 GS02 和 ST01 的值是在网格行上输入的，则将使用同一行的目标命名空间来确定要使用的架构。  
  
    4.  上**包络线**下页上**事务设置设置**部分中，执行以下操作：  
  
        |使用此选项|执行的操作|  
        |--------------|----------------|  
        |**Default**|选择**默认**。 **注意：**当作为默认值的值选择此行**GS1**， **GS2**， **GS3**， **GS7**，和**GS8**使用即使的值**事务类型**，**版本/发行版**，和**目标命名空间**不的匹配项消息。|  
        |**事务类型**|例如，选择你的测试消息的消息类型**864 – 短信**。|  
        |**版本/发行版**|输入**00401**。|  
        |**目标命名空间**|选择**http://schemas.microsoft.com/BizTalk/EDI/X12/2006**。|  
        |**GS1**|验证是否选择测试消息的消息类型，例如， **TX-短信 (864)**。|  
        |**GS2**|输入**01**。|  
        |**GS3**|输入**7654321**。|  
        |**GS4**|选择所需的日期格式。 选择**CCYYMMDD**。 **注意：**你需要在下拉列表中选择值，而不仅仅是在要显示默认值的字段中单击。 如果你仅单击字段，而没有从下拉列表中选择值，则实际上并未选择值。|  
        |**GS5**|选择所需的时间格式。 选择**HHMMSSdd**。|  
        |**GS7**|选择**T-运输数据协调委员会 (TDCC)**。|  
        |**GS8**|验证已作为中输入的 EDI 版本**00401**。|  
  
8.  在上执行以下任务**Contoso-> Fabrikam**选项卡。  
  
    > [!NOTE]
    >  在此演练中，我们将指定的选项卡中所需的值，以便可以成功创建协议。 若要成功创建了协议，这两个单向协议选项必须为定义的值**ISA5**， **ISA6**， **ISA7**，和**ISA8**。  
  
    1.  上**标识符**下页上**交换设置**部分中，输入限定符和标识符字段的值 (**ISA5**， **ISA6**， **ISA7**，和**ISA8**) 对应于测试消息中这些标头字段的值。  
  
        > [!NOTE]
        >  对于本演练中，设置**ISA5**到**ZZ**， **ISA6**到**1234567**， **ISA7**到**ZZ**，和**ISA8**到**7654321**。  
  
9. 单击 **“应用”**。  
  
10. 单击 **“确定”**。 新添加的协议被列入**协议**部分**方和业务配置文件**窗格。 默认情况下，启用新添加的协议。  
  
### <a name="testing-the-walkthrough"></a>测试演练  
 本部分提供有关如何测试演练的信息。  
  
##### <a name="to-test-the-solution"></a>若要测试解决方案  
  
1.  在 [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] 中，打开 [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]SDK\AS2 Tutorial\Sender 文件夹中的 Sender.csproj 项目。  
  
2.  在 HttpSender.cs 中，确保未注释以下行（紧接在 //Request Asynchronous MDN 注释行下面）：  
  
    ```  
    Stream sr = new FileStream(getBizTalkInstallPath() + @"SDK\AS2 Tutorial\X12_00401_864.edi", FileMode.Open, FileAccess.Read);  
    ```  
  
3.  确保未注释以下行（紧接在 //Request Synchronous MDN 注释行下面）：  
  
    ```  
    Stream sr = new FileStream(getBizTalkInstallPath() + @"SDK\AS2 Tutorial\X12_00401_864-Sync.edi", FileMode.Open, FileAccess.Read);  
    ```  
  
4.  生成此项目。  
  
5.  在 Windows 资源管理器中，移至 [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)] SDK\AS2 Tutorial。 在记事本中打开 X12_00401_864.edi。 删除用于定义 Disposition-Notification-Options 头的行，然后保存该文件。  
  
6.  在 Windows 资源管理器，移动到[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]SDK\AS2 Tutorial\Sender\bin\debug 和执行**Sender.exe**。  
  
    > [!NOTE]
    >  在此实例中运行 Sender.exe 将把消息 X12_00401_864.edi 发送到 Contoso 虚拟目录（BTS http 接收位置）。  
  
7.  打开创建将 EDI 负载发送到 (\EDI_to_Contoso) 的 Contoso 本地文件夹。 验证该文件夹中有一个 .XML 文件。 打开该 XML 文件并验证它包含有一个 864 事务集。  
  
8.  打开 MDN 要返回的 Fabrikam 本地文件夹。 在 Windows 资源管理器，移动到[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]SDK\AS2 教程\\_MDNToFabrikam。 打开记事本中的消息文件，并验证该 MDN。 验证在 MDN 中，AS2-From 是 Contoso，AS2-To 是 Fabrikam。  
  
9. 在记事本中打开测试消息 X12_00401_864.edi，验证 \EDI_to_Contoso 本地文件夹的输出消息中的事务集与 X12_00401_864.edi 输入消息中的事务集相对应。  
  
## <a name="see-also"></a>另请参阅  
 [开发和配置 BizTalk Server AS2 解决方案](../core/developing-and-configuring-biztalk-server-as2-solutions.md)