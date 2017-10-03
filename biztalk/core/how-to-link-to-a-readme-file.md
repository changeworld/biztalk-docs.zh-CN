---
title: "如何链接到一个自述文件 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- linking, readme files
- applications, readme files
- linking, applications
- applications, linking
ms.assetid: 7ddbfe77-c8b5-4f90-80ee-8fd5ba57170b
caps.latest.revision: "15"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5024806c6ca69c504666665551dfb0948a0f56b1
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-link-to-a-readme-file"></a>如何链接到一个自述文件
本主题介绍如何使用 BizTalk Server 管理控制台或命令行来添加 Readme.htm 文件，该文件在用户单击控制面板中的“添加或删除程序”中的相应链接时出现。  
  
 安装 BizTalk 应用程序时，在控制面板的“添加或删除程序”中会自动创建指向名为 Readme.htm 的文件的链接。 如果应用程序的安装文件夹中存在 Readme.htm 文件，用户可以打开它通过在你的应用程序的名称下单击显示的"单击此处支持信息"链接，然后单击"%btad_installdir%\readme.htm。" （%btad_installdir%是表示应用程序安装文件夹的环境变量。）  
  
 这样控制面板中“添加或删除程序”中的指向 Readme.htm 文件的链接就可正常运行了，为此您需要执行以下操作：  
  
-   命名 Readme.htm 文件。  
  
-   向应用程序添加 Readme.htm 时，需指定应用程序安装文件夹作为该文件的目标位置（如下面步骤 6 所述）。 默认应用程序安装文件夹是 %ProgramFiles%\Generated by BizTalk\ApplicationName。 您可以将此路径表示为 %BTAD_InstallDir%。  
  
 如果要覆盖应用程序中已有的 Readme.htm 文件，请指定“覆盖”选项。 如果未指定该选项，并且 Readme.htm 文件已存在于应用程序中，则添加操作将失败。  
  
> [!NOTE]
>  如果为此应用程序安装了多个 .msi 文件，并且为每个 .msi 文件选择了不同的安装路径，则当用户单击“添加或删除程序”中的自述文件链接时，包含在最近一次安装的 .msi 文件中的 Readme.htm 文件将被打开。  
  
> [!IMPORTANT]
>  如果没有创建自述文件，或者没有像本主题中介绍的那样将其添加到应用程序中，则在用户单击“自述文件”链接时不会显示任何内容。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行本主题中的过程，必须使用 BizTalk Server Administrators 组的成员帐户登录。 有关更多详细权限的信息，请参阅[用于部署和管理 BizTalk 应用程序所需权限](../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)。  
  
## <a name="to-add-a-readme-file-to-an-application"></a>向应用程序添加自述文件  
  
#### <a name="using-the-biztalk-server-administration-console"></a>使用 BizTalk Server 管理控制台  
  
1.  单击**启动**，指向**所有程序**，指向[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]，然后单击**BizTalk Server 管理**。  
  
2.  在控制台树中，展开“[!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]”，然后展开包含要向其添加 Readme.htm 文件的应用程序的 BizTalk 组。  
  
3.  展开**应用程序**和你想要将 Readme.htm 文件添加应用程序。  
  
4.  右键单击**资源**文件夹，指向**添加**，然后单击**资源**。  
  
5.  单击**添加**，选择 Readme.htm 文件，然后单击**打开**。  
  
6.  在**目标位置**，按以下方式在默认情况下，指定应用程序安装文件夹的完整路径: %btad_installdir%\readme.htm。 不应更改此路径。 如果所提供的应用程序安装文件夹路径不正确，则安装时不会将自述文件文件复制到该路径中，链接也不能正常工作。  
  
7.  完成后，单击 **“确定”**。  
  
#### <a name="using-the-command-line"></a>使用命令行  
  
1.  如下所示打开命令提示符： 单击**启动**，单击**运行**，类型`cmd`，然后单击**确定**。  
  
2.  键入以下命令，替换为适当的值下, 表中所述：  
  
     **BTSTask AddResource** [**/ApplicationName:***值*] **/Type:System.BizTalk:File** [**/覆盖**] **/Source:***值*[**/Destination:***值*] [**/Server:** *值*] [**/数据库：***值*]  
  
     例如：  
  
     **BTSTask AddResource /ApplicationName:MyApplication /Type:System.BizTalk:File / 覆盖 /Source:"C:\Readme Files\MyApplication\Readme.htm"/Destination:%BTAD_InstallDir%\Readme.htm"/Server:MyServer /Database:BizTalkMgmtDB**  
  
    |参数|值|  
    |---------------|-----------|  
    |**/ 应用程序名称**|向其添加自述文件的 BizTalk 应用程序的名称。 如果未指定应用程序名称，则将使用默认 BizTalk 应用程序。 我名称包含空格，则必须将它括在双引号 （"）。|  
    |**/ 类型**|System.BizTalk:File（此值不区分大小写。）|  
    |**/ 覆盖**|覆盖现有文件的选项。 如果没有指定，并在文件中的应用程序与正在添加的文件具有相同的名称已存在，则 AddResource 操作将失败。|  
    |**/ 源**|源文件的完整路径，包括文件名。 如果路径包含空格，必须将它括在双引号 （"）。|  
    |**/ 目标**|%BTAD_InstallDir%\Readme.htm<br /><br /> 这表示应用程序安装文件夹和 Readme.htm 文件的完整路径，它是安装应用程序时将 Readme.htm 文件复制到的位置。 如果不提供该路径，则自述文件不会被复制到应用程序安装文件夹中，“添加或删除程序”中的 Readme.htm 链接也不能正常工作。|  
    |**/ 服务器**|承载 BizTalk 管理数据库的 SQL Server 实例的名称。 如果指定了“Database”参数，则此参数是必需的。 如果未提供，则使用 localhost。 如果未指定“Server”参数和“Database”参数，则使用组的默认 BizTalk 管理数据库。|  
    |**/ 数据库**|BizTalk 管理数据库的名称。 如果指定了“Server”参数，则此参数是必需的。 如果未指定“Server”参数和“Database”参数，则使用组的默认 BizTalk 管理数据库。|  
  
## <a name="see-also"></a>另请参阅  
 [创建和修改 BizTalk 应用程序](../core/creating-and-modifying-biztalk-applications.md)   
 [AddResource 命令： 文件](../core/addresource-command-file.md)