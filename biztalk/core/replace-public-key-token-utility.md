---
title: "将公共密钥令牌实用程序 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Replace Public Key Token Utility
- utilities, Replace Public Key Token Utility
- public key token
ms.assetid: ed8673b9-af06-4bd7-b8b7-7371e4dd0fed
caps.latest.revision: "12"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 7dee6fff7de065c3663ab373f739f7fb465947c8
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="replace-public-key-token-utility"></a>将公共密钥令牌实用程序
此实用程序可以用从强名称程序集密钥 (.snk) 文件派生的公钥标记替换文件中的公钥标记或变量。  
  
 此实用程序可能会很有用，开发人员编写的脚本使用时[BTSTask 命令行参考](../core/btstask-command-line-reference.md)部署程序集。 要想成功部署，必须提供程序集的完全限定名称，包括程序集的公钥标记。 程序集的公钥标记是从 .snk 文件中提取的，并在程序集生成时指定给它。 然而，在将程序集部署到新的环境之前，通常会使用其他公钥标记重新生成它。 因此，开发人员可能不知道部署脚本运行时程序集将使用什么公钥标记。  
  
 可以通过以下两种方法使用替换公钥标记实用程序解决此问题：  
  
-   **方案 1。** 在部署脚本中，开发人员可以使用公钥标记，也可以使用表示公钥标记的占位符。 运行脚本之前，用户可以运行替换公钥标记实用程序，以使用从 .snk 文件（用于针对目标环境生成程序集的文件）提取的公钥标记替代脚本文件中的公钥标记或占位符。  
  
-   **方案 2。** 开发人员可以配置用于自动替换新公钥标记，如下所示的脚本： 脚本开始时，请在调用替换 Public Key Token 实用程序和点到包含公钥标记的.snk 文件。 在脚本中，使用环境变量 %NEWTOKEN% 表示公钥标记。 脚本运行时，实用程序从 .snk 文件中提取公钥标记的值，并将该值设置到环境变量 %NEWTOKEN% 中。 脚本运行时，将用指定的 .snk 文件中的公钥标记来替代 %NEWTOKEN% 的每个实例。 例如：  
  
    ```  
    ReplacePKT.bat key.snk  
    ...  
    ...  
    gacutil /u Assembly, ... PublicKey=%NEWTOKEN% ...  
    ```  
  
## <a name="location-in-sdk"></a>在 SDK 中的位置  
 替换公钥标记实用程序位于：  
  
 [!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]SDK\Utilities\ReplacePublicKeyToken\\。  
  
 替换公钥标记实用程序由三个文件组成：  
  
-   ReplacePKT.bat  
  
-   ReplacePKT.vbs  
  
-   ReplacePKT.wsf  
  
## <a name="procedures"></a>过程  
 使用以下过程，用从 .snk 文件中提取的公钥标记替换文件中公钥标记或占位符的所有实例，如方案 1 中所述。  
  
#### <a name="to-replace-instances-of-a-public-key-token-or-a-placeholder-in-a-file"></a>替换文件中公钥标记或占位符的实例  
  
1.  确保本地计算机上具有以下所有文件：三个替换公钥标记实用程序文件（ReplacePKT.bat、ReplacePKT.vbs、ReplacePKT.wsf）、脚本文件和 .snk 文件。  
  
2.  在命令窗口中，将目录更改到包含替换公钥标记实用程序文件的文件夹。  
  
3.  从命令提示符处，运行以下命令：  
  
4.  **ReplacePKT \<**  *.snk 文件*  **>  \<**  *旧的公钥令牌*  **>  \<**  *文件替换***>**  
  
    |选项|Description|  
    |------------|-----------------|  
    |**\<***.snk 文件***>**|.snk 文件的完整路径，该文件中包含的公钥标记将替换现有的公钥标记或占位符 。|  
    |**\<***旧的公钥令牌***>**|要替换的公钥标记或占位符。|  
    |**\<***文件替换***>**|要替换的公钥标记或占位符所在文件的完整路径。|  
  
     例如：  
  
     **ReplacePKT.bat C:\Tokens\MyToken.snk 12ab3456cd789e12 C:\Scripts\MyScript.vbs**  
  
 使用以下过程，自动设置脚本中使用从 .snk 文件中提取的公钥标记的环境变量，如方案 2 中所述。  
  
#### <a name="to-set-an-environment-variable-that-uses-a-public-key-token"></a>设置使用公钥标记的环境变量  
  
1.  在脚本文件的开始处，添加以下代码行：  
  
    ```  
    ReplacePKT <filename>.snk  
    ```  
  
     其中\< *filename*> 是从中派生公钥标记的.snk 文件的名称。  
  
    ```  
    Example: ReplacePKT.bat MyToken.snk  
    ```  
  
2.  在脚本文件中，使用`%NEWTOKEN%`来表示公钥标记。  
  
     例如：  
  
    ```  
    PublicKey=%NEWTOKEN%  
    ```  
  
3.  将脚本文件传送给用户时，请将组成替换公钥标记实用程序的三个文件（ReplacePKT.bat、ReplacePKT.vbs、ReplacePKT.wsf）包括在内。 确保脚本用户在运行脚本之前将这三个文件全部复制到文件系统中的同一文件夹。  
  
## <a name="see-also"></a>另请参阅  
 [SDK 中的实用程序](../core/utilities-in-the-sdk.md)