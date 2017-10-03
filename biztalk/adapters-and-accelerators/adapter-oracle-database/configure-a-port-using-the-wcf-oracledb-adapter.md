---
title: "配置端口在 BizTalk 中使用 WCF OracleDB 适配器 |Microsoft 文档"
description: "创建 WCF OracleDB 发送和接收要在 BizTalk Server 中使用 Oracle 数据库适配器的端口"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e9eafefb-9b30-4801-9be9-6034ae0d3b7d
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b1e910d3a4d76444495de5ee4e20ada352a7a42b
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="configure-a-port-using-the-wcf-oracledb-adapter"></a>配置使用 WCF OracleDB 适配器的端口
如何配置 WCF OracleDB 发送和接收端口上使用 Oracle 数据库执行出站和入站操作[!INCLUDE[adapteroracle](../../includes/adapteroracle-md.md)]。  
  
## <a name="prerequisites"></a>先决条件  
使用是的成员的帐户登录[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理员或 BizTalk 操作员组。 有关更多详细有关权限的信息，请参阅[用于部署和管理 BizTalk 应用程序所需权限](../../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)，和[最低安全权限](https://social.technet.microsoft.com/wiki/contents/articles/24590.minimum-security-rights-for-biztalk-server-2006-to-2016.aspx)。 
  
## <a name="deploy-adapters-to-send-messages-to-oracle-database"></a>部署适配器，以将消息发送到 Oracle 数据库  
  
1.  启动[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理控制台。  
  
2.  添加到 WCF OracleDB 适配器[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理控制台。 有关说明，请参阅[将 Oracle 数据库适配器添加到 BizTalk Server 管理控制台](../../adapters-and-accelerators/adapter-oracle-database/adding-the-oracle-database-adapter-to-biztalk-server-administration-console.md)。  
  
3.  在控制台树中，展开**BizTalk 组**，然后展开**应用程序**。  
  
4.  展开你想要部署的应用程序[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]。  
  
5.  右键单击**发送端口**，指向**新建**，然后指向你想要根据之间的通信模式配置的端口的类型[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]和 Oracle 数据库。  
  
6.  在**发送端口属性**对话框中，在**常规**选项卡上，键入发送端口的名称。  
  
7.  从**类型**下拉列表中，选择 WCF OracleDB，，然后单击**配置**。  
  
8.  在传输属性对话框中，请执行以下操作：  
  
    1.  单击**常规**选项卡上，单击**配置**按钮，然后提供的连接参数的值。 有关连接 URI 的详细信息，请参阅[创建 Oracle 数据库连接 URI](../../adapters-and-accelerators/adapter-oracle-database/create-the-oracle-database-connection-uri.md)。  
  
    2.  上**常规**选项卡上，在**操作**文本框中，键入操作的操作。 请参阅[消息和消息架构](messages-and-message-schemas-for-biztalk-adapter-for-oracle-database.md)有关每个操作的操作的列表。 例如，要调用插入操作 Oracle 数据库中的 HR 模式下的员工表的操作是：  
  
        ```  
        http://Microsoft.LobServices.OracleDB/2007/03/HR/Table/EMPLOYEE/Select  
        ```  
  
    3.  单击**绑定**选项卡上，并指定为公开的绑定属性的值[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]。 有关绑定属性的详细信息，请参阅[阅读有关 Oracle 数据库适配器绑定属性](../../adapters-and-accelerators/adapter-oracle-database/read-about-the-oracle-database-adapter-binding-properties.md)。
  
        > [!NOTE]
        >  绑定属性显示的配置发送端口或接收端口。 例如，与通知相关的绑定属性不可用时配置发送端口，因为通知是入站的操作，需要接收端口配置。  
  
    4.  单击**凭据**选项卡，，然后执行下列操作之一：  
  
        -   选择**不使用单一登录**选项，并指定用户名和密码以连接到 Oracle 数据库。  
  
            -   若要使用 Oracle 数据库凭据进行连接，请键入中的数据库凭据**用户名**和**密码**文本框。  
  
            -   若要使用 Windows 身份验证进行连接，请键入 **/** 中**用户名**文本框和离开**密码**文本框保留为空白。  
  
        -   选择**使用单一登录**选项，并指定分支机构的企业单一登录 (SSO) 应用程序。  
  
    5.  若要返回到**发送端口属性**对话框中，单击**确定**。  
  
9. 从**发送处理程序**列表中，选择**BizTalkServerApplication**。  
  
10. 如果你选择了**静态单向发送端口**在步骤 5 中，指定发送管道。 从**发送管道**列表中，选择对应于 XMLTransmit 管道。  
  
11. 如果你选择了**静态请求-响应端口**在步骤 4 中，指定发送和接收管道。  
  
    1.  从**发送管道**下拉列表中，选择对应于 XMLTransmit 管道。  
  
    2.  从**接收管道**下拉列表中，选择对应于 XMLReceive 管道。  
  
12. 单击 **“确定”**。  
  
## <a name="deploy-adapters-to-receive-messages-from-oracle-database"></a>部署适配器从 Oracle 数据库接收消息  
  
1.  启动[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理控制台。  
  
2.  添加到 WCF OracleDB 适配器[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理控制台。 有关说明，请参阅[将 Oracle 数据库适配器添加到 BizTalk Server 管理控制台](../../adapters-and-accelerators/adapter-oracle-database/adding-the-oracle-database-adapter-to-biztalk-server-administration-console.md)。  
  
3.  在控制台树中，展开**BizTalk 组**，然后展开**应用程序**。  
  
4.  展开你想要部署的应用程序[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]。  
  
5.  右键单击**接收端口**，指向**新建**，然后单击**单向接收端口**或**请求响应接收端口**，具体取决于模式之间的通信[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]和 Oracle 数据库。  
  
6.  在**接收端口属性**对话框中，在**常规**选项卡上，键入接收端口的名称。  
  
7.  上**接收位置**选项卡上，单击**新建**。 **接收位置属性**对话框随即出现。  
  
8.  在**接收位置属性**对话框框中，执行以下操作：  
  
    1.  指定接收位置的名称。  
  
    2.  从**类型**下拉列表中，选择 WCF OracleDB，，然后单击**配置**。  
  
9. 在传输属性对话框中，请执行以下操作：  
  
    1.  单击**常规**选项卡上，单击**配置**按钮，并为连接参数提供值。 有关连接 URI 的详细信息，请参阅[创建 Oracle 数据库连接 URI](../../adapters-and-accelerators/adapter-oracle-database/create-the-oracle-database-connection-uri.md)。  
  
    2.  单击**绑定**选项卡上，并指定绑定以公开的属性的值[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]。 有关绑定属性的详细信息，请参阅[阅读有关 Oracle 数据库适配器绑定属性](../../adapters-and-accelerators/adapter-oracle-database/read-about-the-oracle-database-adapter-binding-properties.md)。
  
        > [!NOTE]
        >  绑定属性显示的配置发送端口或接收端口。 例如，与通知相关的绑定属性不可用时配置发送端口，因为通知是入站的操作，需要接收端口配置。  
  
    3.  单击**行为**选项卡以设置事务的隔离级别。 有关设置事务隔离级别的详细信息，请参阅[配置事务隔离级别和事务超时](../../adapters-and-accelerators/adapter-oracle-database/configure-transaction-isolation-level-and-transaction-timeout-with-oracle-db.md)。  
  
    4.  单击**其他**选项卡，然后执行下列操作之一：  
  
        -   选择**用户帐户**选项，并指定用户名和密码以连接到 Oracle 数据库。  
  
            -   若要使用 Oracle 数据库凭据进行连接，请键入中的数据库凭据**用户名**和**密码**文本框。  
  
            -   若要使用 Windows 身份验证进行连接，请键入 **/** 中**用户名**文本框和离开**密码**文本框保留为空白。  
  
        -   选择**Get 凭据 affiliate 应用程序**选项，然后指定关联 SSO 应用程序。  
  
    5.  若要返回到**接收位置属性**对话框中，单击**确定**。  
  
10. 从**接收处理程序**下拉列表中，选择**BizTalkServerApplication**。  
  
11. 如果你选择了**单向接收端口**在步骤 5 中，指定接收管道。 从**接收管道**列表中，选择对应于 XMLReceive 管道。  
  
12. 如果你选择了**请求响应接收端口**在步骤 5 中，指定发送和接收管道。  
  
    1.  从**接收管道**下拉列表中，选择对应于 XMLReceive 管道。  
  
    2.  从**发送管道**下拉列表中，选择对应于 XMLTransmit 管道。  
  
13. 在**接收位置属性**对话框中，单击**确定**。  
  
14. 在**接收端口属性**对话框中，单击**确定**。  
  
## <a name="see-also"></a>另请参阅  
   [手动配置到 Oracle 数据库适配器的物理端口绑定](../../adapters-and-accelerators/adapter-oracle-database/manually-configure-a-physical-port-binding-to-the-oracle-database-adapter.md)
 
 [连接到 Oracle 数据库使用 Windows 身份验证](../../adapters-and-accelerators/adapter-oracle-database/connect-to-the-oracle-database-using-windows-authentication.md)