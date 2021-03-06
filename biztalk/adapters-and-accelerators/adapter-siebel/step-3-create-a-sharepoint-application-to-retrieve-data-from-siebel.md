---
title: 步骤 3： 创建 SharePoint 应用程序以从 Siebel 检索数据 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 86bde531-2daf-452b-b3e6-5481d66f72e7
caps.latest.revision: 14
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: df6c92b371291f4359c4bbce5e16529700bcc0c8
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36971862"
---
# <a name="step-3-create-a-sharepoint-application-to-retrieve-data-from-siebel"></a>步骤 3： 创建 SharePoint 应用程序以从 Siebel 检索数据
![步骤 3，共 4 步](../../adapters-and-accelerators/adapter-oracle-ebs/media/step-3of4.gif "Step_3of4")  
  
 **完成时间：** 15 分钟。  
  
 **目标：** 现在必须通过使用 Business Data Catalog Definition Editor，创建将应用程序定义文件，并将其导入 Office SharePoint Server。  
  
## <a name="prerequisites"></a>必要條件  
  
-   您应创建了一个应用程序定义文件，如中所述[步骤 2： 为 Siebel 业务组件操作创建应用程序定义文件](../../adapters-and-accelerators/adapter-siebel/step-2-create-an-application-definition-file-for-siebel-business-component.md)。  
  
-   必须运行 Microsoft 单一登录服务。  
  
## <a name="how-to-create-a-sharepoint-application"></a>如何创建 SharePoint 应用程序  
 创建 SharePoint 应用程序涉及以下步骤：  
  
-   在 SharePoint 中创建的单一登录 (SSO) 应用程序  
  
-   创建共享的服务提供程序 (SSP)  
  
-   导入应用程序定义文件  
  
-   创建 Web 部件页，并添加 Web 部件  
  
## <a name="creating-an-sso-application-in-sharepoint"></a>在 SharePoint 中创建的 SSO 应用程序  
 若要在 Siebel 系统中的 SharePoint 应用程序中访问数据，必须设置映射到 Siebel 用户的 SharePoint 用户的 SSO 应用程序。 在 SharePoint 中创建的 SSO 应用程序涉及以下步骤：  
  
1.  **管理服务器上单一登录设置**。 在此步骤中，你指定的用户帐户，可以管理和设置单一登录服务。 您可以从管理服务器设置页来执行操作。 此选项可从 SharePoint 中心管理控制台。 有关此步骤的详细信息，请参阅"配置单一登录适用于 Office SharePoint Server 2007"部分在[ http://go.microsoft.com/fwlink/?LinkId=105291 ](http://go.microsoft.com/fwlink/?LinkId=105291)。  
  
2.  **管理企业应用程序定义的设置**。 在此步骤中，您配置企业应用程序定义的设置。 您可以从企业应用程序定义页的管理设置执行操作。 此选项可从 SharePoint 中心管理控制台。  
  
    1.  在管理中心内，在顶部导航栏上，单击**操作**。  
  
    2.  在操作页中**的安全配置**部分中，单击**管理的单一登录设置**。  
  
    3.  在单一登录页上，管理设置中**企业应用程序定义设置**部分中，单击**管理企业应用程序定义的设置**。  
  
    4.  在管理企业应用程序定义页上，提供的值**显示名称**，**应用程序名称**，并**联系人电子邮件地址**字段。  
  
        > [!IMPORTANT]
        >  有关**应用程序名称**字段中，请确保指定相同的 SSO 应用程序名称为指定**SecondarySsoApplicationId**时创建应用程序定义文件中，为变量中所述[步骤 2： 为 Siebel 业务组件操作创建应用程序定义文件](../../adapters-and-accelerators/adapter-siebel/step-2-create-an-application-definition-file-for-siebel-business-component.md)。  
  
    5.  将其他字段保留为默认值，然后单击**确定**。  
  
3.  **管理企业应用程序定义的帐户信息**。 在此步骤中，启用单个用户或组从 SharePoint 连接到企业应用程序。 从根本上来说，在此步骤中您映射单个用户或组到用户在 LOB 系统。 您还指定用于连接到 LOB 系统的凭据。 您可以从管理帐户信息执行操作的企业应用程序定义页。 此选项可从 SharePoint 中心管理控制台。 有关此步骤的详细信息，请参阅"管理企业应用程序定义的帐户信息"部分在[ http://go.microsoft.com/fwlink/?LinkId=105291 ](http://go.microsoft.com/fwlink/?LinkId=105291)。  
  
## <a name="creating-a-shared-services-provider"></a>创建共享的服务提供程序  
 SSP 是共享的服务和及其支持资源的逻辑分组。 您可以创建使用 SharePoint 管理中心控制台 SSP。  
  
 必须创建 SSP 时定义 Web 站点 请记住的端口号和你创建的站点地址。 你将导出到此站点的业务数据目录应用程序定义。  
  
 有关创建 SSP 的详细信息，请参阅"一章概述： 创建和配置共享服务提供程序"处[ http://go.microsoft.com/fwlink/?LinkId=105119 ](http://go.microsoft.com/fwlink/?LinkId=105119)。  
  
## <a name="importing-the-application-definition-file"></a>导入应用程序定义文件  
 现在必须将应用程序定义文件导入 ssp。  
  
#### <a name="to-import-the-application-definition-file"></a>若要导入应用程序定义文件  
  
1. 启动 SharePoint 3.0 管理中心。 单击**启动**，依次指向**所有程序**，指向**Microsoft Office Server**，然后单击**SharePoint 3.0 管理中心**.  
  
2. 在左侧的导航窗格中，单击你想要导入应用程序定义的 SSP 的名称。  
  
3. 在中**业务数据目录**部分中，单击**导入应用程序定义**。  
  
4. 在导入应用程序定义页，此时会打开，浏览到 Siebel_Account.xml，选择该文件，并单击**打开**。  
  
5. 单击“导入” 。  
  
6. 单击“确定” 。  
  
   导入应用程序之后, 中，你可以查看你的应用程序通过转到**查看应用程序**链接。 单击以查看应用程序中的实体的应用程序名称。  
  
## <a name="creating-web-parts"></a>创建 Web 部件  
 现在必须在您的 SharePoint 站点查看和管理将从 Siebel 系统中提取的业务数据中创建 Web 部件。 Web 部件是信息的可重用的组件，可包含任何类型的基于 Web，包括分析、 协作式和和数据库信息。  
  
 在本教程中，在 Business Data Catalog Definition Editor 创建方法实例创建 Web 部件。 Office SharePoint Server 提供了特定使用 Web 部件的不同种类。 Finder 方法实例，我们将使用**业务数据列表**Web 部件。 此 Web 部件，可指定要对帐户业务组件执行查询的搜索表达式。 对于本教程，我们称之为**查询帐户**Web 部件。  
  
 本部分介绍如何创建这些 Web 部件。 有关创建 Web 部件的详细信息，请参阅 Microsoft Office SharePoint Server 2007 文档 （"自定义业务数据列表、 Web 部件和网站"） 处[ http://go.microsoft.com/fwlink/?LinkId=104131 ](http://go.microsoft.com/fwlink/?LinkId=104131)。  
  
 Web 部件将添加到单个 Web 部件页。 必须添加 Web 部件之前创建的 Web 部件页。 对于本教程中，调用该 Web 部件页**Siebel 帐户**。  
  
### <a name="creating-a-web-part-page"></a>创建 Web 部件页  
 本部分介绍如何创建 Web 部件页。  
  
##### <a name="to-create-a-web-part-page"></a>若要创建的 web 部件页  
  
1. 启动 SharePoint 3.0 管理中心。 单击**启动**，依次指向**所有程序**，指向**Microsoft Office Server**，然后单击**SharePoint 3.0 管理中心**。  
  
2. 在左侧的导航窗格中，单击你想要导入应用程序定义的 SSP 的名称。  
  
3. 在共享服务管理页上，从右上角，单击**站点操作**，然后单击**创建**。  
  
    ![若要创建 web 部件的菜单](../../adapters-and-accelerators/adapter-oracle-ebs/media/a9872c3e-f823-4c47-a538-19242565d2e9.gif "a9872c3e-f823-4c47-a538-19242565d2e9")  
  
4. 在创建页下**网页**部分中，单击**Web 部件页**。  
  
5. 在新的 Web 部件页中，执行以下步骤：  
  
   1. 在中**名称**字段中，指定页面的名称。 对于本教程，将名称指定为`Siebel Account`。  
  
   2. 选择**如果文件已存在，则覆盖**复选框，如果你想要使用相同的名称创建的页覆盖旧页面。  
  
   3. 在中**布局**部分中，从**选择一个布局模板**框中，选择适用于 Web 部件页的布局。 对于本教程中，选择**整页、 垂直**。  
  
   4. 在中**保存位置**部分中，在**文档库**列表中，选择**窗体模板**。  
  
   5. 单击 **“创建”**。 只需创建后下, 图显示的 Web 部件页。  
  
       ![空 Web 部件页](../../adapters-and-accelerators/adapter-siebel/media/1fa218f5-de81-43be-b1b1-c46de422f112.gif "1fa218f5-de81-43be-b1b1-c46de422f112")  
  
      您现在必须将不同的 Web 部件添加到此页。  
  
### <a name="adding-a-business-data-list-web-part"></a>添加业务数据列表 Web 部件  
 现在，你必须将业务数据列表 Web 部件添加到 Web 部件页。 使用此 Web 部件，您将查询帐户业务组件使用的搜索表达式。 此 Web 部件对应于创建在 Business Data Catalog Definition Editor 的 Finder 方法实例 (QueryAccount)。  
  
##### <a name="to-add-a-business-data-list-web-part"></a>若要添加业务数据列表 Web 部件  
  
1.  在中**Siebel 帐户**页上，在**标头**部分中，单击**添加 Web 部件**。  
  
2.  在中**添加 Web 部件**对话框中**业务数据**部分中，选择**业务数据列表**复选框，然后依次**添加**。  
  
     ![创建业务数据 Web 部件的选项](../../adapters-and-accelerators/adapter-oracle-ebs/media/ae7c952c-1592-495f-9452-c1bffd44421c.gif "ae7c952c-1592-495f-9452-c1bffd44421c")  
  
3.  在新添加的业务数据列表 Web 部件，单击**打开工具窗格**链接。  
  
     ![Web 部件中打开工具窗格](../../adapters-and-accelerators/adapter-oracle-ebs/media/4e7a1cb1-69dc-4e0d-a211-6a217dc4a549.gif "4e7a1cb1-69dc-4e0d-a211-6a217dc4a549")  
  
4.  业务数据列表工具窗格将在右窗格中打开。 在中**业务数据列表**部分中，对于**类型**字段中，单击**浏览**按钮。  
  
     ![业务数据列表工具窗格](../../adapters-and-accelerators/adapter-siebel/media/3b6e1576-03ce-4fc8-bf5a-7b414ef4408c.gif "3b6e1576-03ce-4fc8-bf5a-7b414ef4408c")  
  
5.  在中**业务数据类型选取器**对话框中，选择**Siebel_Account_Instance**应用程序，，然后单击**确定**。  
  
     ![选择应用程序实例](../../adapters-and-accelerators/adapter-siebel/media/a658d06a-83a8-4e4b-9451-ce58e7ac3632.gif "a658d06a-83a8-4e4b-9451-ce58e7ac3632")  
  
6.  展开**外观**节点，然后在**标题**字段中，指定 Web 部件的标题。 对于此 Web 部件，指定**Account List**。  
  
7.  在业务数据列表工具窗格中，单击**Apply**，然后单击**确定**。 业务数据列表 Web 部件现在看起来如下所示：  
  
     ![业务数据列表 Web 部件](../../adapters-and-accelerators/adapter-siebel/media/06dbb84a-38c3-4ece-b981-5aa7471909ed.gif "06dbb84a-38c3-4ece-b981-5aa7471909ed")  
  
    > [!NOTE]
    >  此外可以更改参数列的显示的顺序。 就可以通过单击**编辑视图**向 Web 部件右上角的链接。  
  
8.  单击**退出编辑模式**从页面的右上角。  
  
## <a name="next-steps"></a>后续步骤  
 通过从 Siebel 系统检索数据来测试 SharePoint 应用程序。 请参阅[步骤 4： 测试 SharePoint 应用程序](../../adapters-and-accelerators/adapter-oracle-ebs/step-4-test-your-sharepoint-application.md)。  
  
## <a name="see-also"></a>请参阅  
 [教程 1：在 SharePoint 站点上从 Siebel 系统提供数据](../../adapters-and-accelerators/adapter-siebel/tutorial-1-presenting-data-from-a-siebel-system-on-a-sharepoint-site.md)