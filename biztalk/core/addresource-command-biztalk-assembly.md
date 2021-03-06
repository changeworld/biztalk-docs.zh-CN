---
title: AddResource 命令： BizTalk 程序集 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c18607b5-d929-48c9-9fa3-f728a7a80d04
caps.latest.revision: 24
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 21dcffc7a404f891dbcb01c7d84e0236106308e6
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37011086"
---
# <a name="addresource-command-biztalk-assembly"></a>AddResource 命令：BizTalk 程序集
若要将 BizTalk 程序集添加到 BizTalk 应用程序，请使用**AddResource**命令并指定**system.biztalk: biztalkassembly**类型参数。 运行此命令可将程序集添加到 BizTalk 管理数据库中。 该程序集还会显示在 BizTalk Server 管理控制台中，即它所添加到的应用程序的“资源”文件夹下。 该程序集中包含的项目也会显示在相应的文件夹下。 此外，当您使用列出这些项目[ListApp 命令](../core/listapp-command.md)。  
  
 使用此命令时，请切记以下几点：  
  
- 如果某个程序集与应用程序中已存在的程序集具有相同的全名，则必须指定“Overwrite”参数，否则 AddResource 操作将失败。 全名包括名称、公钥标记、区域性和版本。 但是，如果其他应用程序依赖于此程序集，则即使指定了“Overwrite”参数，AddResource 操作也会失败。  
  
- 如果组中存在具有同一全名的其他程序集，则即使指定了“Overwrite”参数，AddResource 操作也会失败。  
  
- 如果要覆盖包含业务流程的程序集，则在运行此命令之前，必须先停止并取消登记这些业务流程。 此外，必须停止并取消登记业务流程绑定到的发送端口，并且必须禁用接收位置。  
  
- 如果要添加的程序集依赖于并未包含在该应用程序中的其他项目，则 AddResource 操作将失败。  
  
  有关依赖关系的详细信息，请参阅[依赖项和应用程序部署](../core/dependencies-and-application-deployment.md)。  
  
## <a name="usage"></a>用法  
 **BTSTask AddResource** [**/ApplicationName:**<em>值</em>] **/Type:System.BizTalk:BizTalkAssembly** [**/Overwrite**] **/Source:**<em>值</em>[**/Destination:**<em>值</em>] [**/Options:GacOnAdd** <em>&#124;</em> **GacOnInstall**<em>&#124;</em>**GacOnImport**] [**/Server:** <em>值</em>] [**/database:**<em>值</em>]  
  
## <a name="parameters"></a>Parameters  
  
|参数|Required|ReplTest1|  
|---------------|--------------|-----------|  
|**/ ApplicationName** (或 **/A**，请参阅备注)|“否”|向其添加程序集的 BizTalk 应用程序的名称。 如果名称包含空格，则必须将其括在双引号 （"）。 如果未指定应用程序名称，则将使用默认 BizTalk 应用程序。|  
|**/ 键入**(或 **/T**，请参阅备注)|是|**System.biztalk: biztalkassembly** （此值不区分大小写。）|  
|**/ 覆盖**(或 **/Ov**，请参阅备注)|“否”|更新现有程序集的选项。 如果未指定，且应用程序中已存在与要添加的程序集具有相同全名的程序集，则 AddResource 操作将失败。 全名对应于程序集的本地唯一标识符 (LUID)。 可以通过使用应用程序中查看项目的 Luid [ListApp 命令](../core/listapp-command.md)。 如果其他应用程序依赖于要覆盖的程序集，则即使指定了此参数，AddResource 操作也会失败。|  
|**/Source** (或 **/So**，请参阅备注)|是|程序集文件的完整路径，包含文件名。 如果路径包含空格，则必须将其括在双引号 （"）。|  
|**/ 目标**(或 **/De**，请参阅备注)|“否”|从 .msi 文件安装应用程序时，程序集文件要复制到的位置的完整路径。 如果未提供，则安装期间该程序集文件将不会复制到本地文件系统。 如果路径包含空格，则必须将其括在双引号 （"）。 **注意：** 可以使用在 BizTalk Server 安装过程中设置，环境变量 %btad_installdir%来指定应用程序安装文件夹。 这将在其他目标计算机上为应用程序的文件创建一致的安装位置。 例如：“%BTAD_InstallDir%\MyFiles\Orchestrations.dll”|  
|**/ 选项**(或 **/Op**，请参阅备注)|“否”|-   **GacOnAdd**： 指定程序集安装到全局程序集缓存 (GAC) 在本地计算机上在 AddResource 操作过程。<br />-   **GacOnInstall**： 指定当从.msi 文件安装应用程序时，将程序集安装到 GAC。<br />-   **GacOnImport**： 指定导入应用程序.msi 文件时，将程序集安装到 GAC。<br /><br /> 多个选项之间必须用逗号分开。|  
|**/ 服务器**(或 **/Se**，请参阅备注)|“否”|BizTalk 管理数据库的宿主 SQL Server 实例的名称，格式为“服务器名称\实例名称,端口”。<br /><br /> 只在实例名称与服务器名称不相同时才需要指定实例名称。 只在 SQL Server 不使用默认端口号 (1433) 时才需要指定端口。<br /><br /> 示例：<br /><br /> Server=MyServer<br /><br /> Server=MyServer\MySQLServer,1533<br /><br /> 如果未提供，则使用本地计算机上运行的 SQL Server 实例的名称。|  
|**/ 数据库**(或 **/Da**，请参阅备注)|“否”|BizTalk 管理数据库的名称。 如果未指定，则使用在本地 SQL Server 实例中运行的 BizTalk 管理数据库。|  
  
## <a name="sample"></a>示例  
 **BTSTask AddResource /ApplicationName:MyApplication /Type:System.BizTalk:BizTalkAssembly / 覆盖**  
  
 **/Source:"%BTAD_InstallDir%\Source Assemblies\Orchestrations.dll"/Destination:"%BTAD_InstallDir%\New Assemblies\Orchestrations.dll"/Options:GacOnInstall，GacOnImport /Server:MyDatabaseServer /Database:BizTalkMgmtDb**  
  
## <a name="remarks"></a>Remarks  
 参数不区分大小写。 指定参数无需键入整个参数名，只需键入可明确标识该参数的参数名的前几个字母即可。  
  
## <a name="see-also"></a>请参阅  
 [AddResource 命令](../core/addresource-command.md)   
 [如何将 BizTalk 程序集添加到应用程序](../core/how-to-add-a-biztalk-assembly-to-an-application.md)