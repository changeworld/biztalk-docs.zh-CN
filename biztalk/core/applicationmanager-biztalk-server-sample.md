---
title: ApplicationManager （BizTalk Server 示例） |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 51ebe7a8-a0ca-4d2a-bf40-ec6421ba5a95
caps.latest.revision: 13
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b926f9e848ab86f5b168d46b3b0e84d85356f592
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37010734"
---
# <a name="applicationmanager-biztalk-server-sample"></a>ApplicationManager（BizTalk Server 示例）
ApplicationManager 示例演示如何使用管理对象启动或停止 BizTalk 应用程序。  

## <a name="prerequisites"></a>必要條件  

- 您必须具有 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理权限才能使用此示例中的管理对象。  

- Windows PowerShell 脚本需要 Windows PowerShell 执行策略以允许脚本执行。 有关详细信息请参阅：[检查执行策略](http://go.microsoft.com/fwlink/?LinkId=128930)。  

## <a name="what-this-sample-does"></a>本示例的用途  
 此示例演示如何使用**BtsCatalogExplorer**并**应用程序**类**Microsoft.BizTalk.ExplorerOM**命名空间来启动和停止已部署 BizTalk 应用程序。 本示例是使用 Microsoft [!INCLUDE[btsVCSharp](../includes/btsvcsharp-md.md)] 编写的。 本主题中还包含 Windows PowerShell 示例脚本。 本示例将演示以下操作：  

-   通过使用连接到 BizTalk 管理数据库**BtsCatalogExplorer**类。  

-   查找中的应用程序实例**BtsCatalogExplorer**根据应用程序名称。  

-   提交应用程序的启动和停止命令。  

## <a name="where-to-find-this-sample"></a>本示例的所在位置  
 本示例位于以下 SDK 位置中：  

 \<*示例路径*\>\Admin\ExplorerOM\ApplicationManager  

 下表显示了本示例中的文件及其用途说明：  


|                                 文件                                 |                                                 Description                                                  |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
|                               Program.cs                                | 本示例中演示的操作所需的 [!INCLUDE[btsVCSharp](../includes/btsvcsharp-md.md)] 源文件。 |
| ApplicationManager.sln、ApplicationManager.csproj、ApplicationManager.suo |                                  示例的解决方案文件和项目文件。                                  |

## <a name="building-and-running-this-sample"></a>生成并运行本示例  

#### <a name="to-build-this-sample"></a>生成示例  

1. 在 [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] 中，打开解决方案文件 ApplicationManager.sln。  

2. 在“生成”  菜单上，单击“生成解决方案” 。  

#### <a name="to-run-this-sample"></a>运行本示例的步骤  

1. 打开命令窗口并导航到以下文件夹：  

    \<*示例路径*\>\Admin\ExplorerOM\ApplicationManager\bin\Debug  

2. 运行文件 ApplicationManager.exe 提供以下两个有序命令行参数：  

   - **\<启动&#124;停止\>** 第一个参数是要部署的应用程序执行的操作。  

   - **\<ApplicationName\>** 第二个参数是部署的应用程序的名称。  

     例如：  

   ```  
   ApplicationManager.exe stop MyBizTalkApp  
   ```  

    命令行参数不足时运行示例将显示使用语法。 例如：  

   ```  
   Usage:  

   ApplicationManager <start|stop> <Application Name>  

    Where:  
     <Application Name> = The name of the application that needs to be changed  

   Example: ApplicationManager start Application1  
   ```  

## <a name="windows-powershell-script-example"></a>Windows Powershell 脚本示例  
 以下 Windows PowerShell 脚本片段可用于演示的相同功能**ExplorerOM**类：  

```  
#=== Make sure the ExplorerOM assembly is loaded ===#  

[void] [System.reflection.Assembly]::LoadWithPartialName("Microsoft.BizTalk.ExplorerOM")  

#=== Connect the BizTalk Management database ===#  

$Catalog = New-Object Microsoft.BizTalk.ExplorerOM.BtsCatalogExplorer  
$Catalog.ConnectionString = "SERVER=.;DATABASE=BizTalkMgmtDb;Integrated Security=SSPI"  

#=== Loop through applications in the catalog trying to find a name match ===#  

foreach($app in $Catalog.Applications)  
{  
    if ($($app.Name) -ieq $args[1])  
    {  

        #=== The first command-line argument should be "start" or "stop" ===#  

        if ($args[0] -ieq "start")  
        {  
            Write-Host `r`nIssuing start command to $app.Name...`r`n  
            $app.Start([Microsoft.BizTalk.ExplorerOM.ApplicationStartOption] "StartAll")  
            $Catalog.SaveChanges()  
        }  

        if ($args[0] -ieq "stop")  
        {  
            Write-Host `r`nIssuing stop command to $app.Name...`r`n  
            $app.Stop([Microsoft.BizTalk.ExplorerOM.ApplicationStopOption] "StopAll")  
            $Catalog.SaveChanges()  
        }  

    }  
}  
```  

 脚本中需要与 [!INCLUDE[btsVCSharp](../includes/btsvcsharp-md.md)] 示例相同的命令行参数。 下面是一个运行 Windows PowerShell 脚本以启动部署的 BizTalk 应用程序的示例：  

```  
PS C:\> .\ApplicationManager.ps1 start MyBizTalkApp  

Issuing start command to MyBizTalkApp ...  
```  

## <a name="see-also"></a>请参阅  
 [Admin-ExplorerOM（BizTalk Server 示例文件夹）](../core/admin-explorerom-biztalk-server-samples-folder.md)