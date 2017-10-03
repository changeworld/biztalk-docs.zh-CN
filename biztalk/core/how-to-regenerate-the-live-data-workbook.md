---
title: "如何重新生成实时数据工作簿 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4bd3a3fa-a550-4363-bbc0-2153226509ad
caps.latest.revision: "21"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 8fcabebb1429fae8531753a8a3aede5595bb148f
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-regenerate-the-live-data-workbook"></a>如何重新生成实时数据工作簿
在 BAM 实时数据工作簿丢失或损坏时，可使用 BAM 管理实用程序重新生成工作簿。 此过程在从 [!INCLUDE[btsBizTalkServer2004](../includes/btsbiztalkserver2004-md.md)] 升级到 [!INCLUDE[btsBizTalkServer2006r3](../includes/btsbiztalkserver2006r3-md.md)] 时也非常有用，这是因为用于 [!INCLUDE[btsBizTalkServer2004](../includes/btsbiztalkserver2004-md.md)] 的实时数据工作簿与 [!INCLUDE[btsBizTalkServer2006r3](../includes/btsbiztalkserver2006r3-md.md)] 不兼容。  
  
 常规步骤如下所示：  
  
-   使用 BAM 管理实用程序从 BAM 数据库中检索 BAM 定义。  
  
-   重新创建数据透视表。 由于 get-defxml 命令完成的 XML 检索仅包含活动和视图，因此必须使用用于 Excel 的 BAM 加载项重新创建数据透视表。  
  
-   重命名数据透视表。 如果要从 [!INCLUDE[btsBizTalkServer2004](../includes/btsbiztalkserver2004-md.md)] 升级到 [!INCLUDE[btsBizTalkServer2006r3](../includes/btsbiztalkserver2006r3-md.md)]，则必须执行这一步骤。 这是必要自[!INCLUDE[btsBizTalkServer2004](../includes/btsbiztalkserver2004-md.md)]，BAM 存储名称的 BAM 工作簿的两个集： 显示名称和内部名称。 在检索 BAM 定义时，XML 包含工作簿的内部名称。 必须重命名数据透视表，以确保实时数据工作簿可正确地连接到数据库。  
  
-   使用 BAM 管理实用程序重新生成实时数据工作簿。  
  
### <a name="to-retrieve-the-bam-definition"></a>检索 BAM 定义  
  
1.  单击**启动**，单击**运行**，类型**cmd**，然后单击**确定**。  
  
2.  在命令提示符下，导航到以下目录：[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]Tracking。  
  
3.  类型： **bm.exe get defxml-FileName:abc.xml**  
  
    > [!NOTE]
    >  在支持用户帐户控制 (UAC) 的系统上，可能需要具有管理权限才能运行该工具。  
  
### <a name="to-re-create-the-pivottable-reports"></a>重新创建数据透视表  
  
1.  单击**启动**，指向**所有程序**，指向**Microsoft Office**，然后单击**Microsoft Office Excel**。  
  
2.  单击**外接程序**选项卡上，然后选择**导入 XML**从**BAM**下拉列表中的**菜单命令**组。  
  
    > [!NOTE]
    >  如果**外接程序**选项卡上不存在，请按照中的说明[步骤 1: BAM 外接程序添加到 Microsoft Office Excel](http://msdn.microsoft.com/library/3400969f-0c54-4a75-979d-ad2f7af86448)若要添加的 BAM 外接程序。  
  
3.  导航到[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]跟踪文件夹并选择 abc.xml 文件。  
  
4.  根据您的定义重新创建数据透视表。  
  
5.  保存该工作簿。 若要执行此操作，请单击**文件**菜单，，然后单击**另存为**键入 mynewbook.xls 时提示输入文件名称。  
  
### <a name="to-rename-the-pivottable-reports-optional"></a>重命名数据透视表（可选）  
  
1.  打开时检索的 BAM 定义，通过单击使用记事本创建 abc.xml 文件**启动**、 单击**运行**，键入记事本[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]Tracking\abc.xml，，然后单击**确定**。  
  
2.  找到\<标题 > 标记下\<BAMDefinition >\\< 扩展\>\\< OWC\>\\< PivotTableView\>\\<数据透视表\>\\< 数据透视视图\>\\< 标签\>。 此标记的内容是某个数据透视表的内部名称。 可以通过查找下一步中找到其他数据透视表报告的内部名称\<标题 > 标记。 打开**mynewbook.xls**并使用位于重命名你的数据透视表报告的名称。  
  
3.  保存已更新的工作簿。  
  
    > [!NOTE]
    >  你必须遵循此过程，仅当您正在从升级[!INCLUDE[btsBizTalkServer2004](../includes/btsbiztalkserver2004-md.md)]到[!INCLUDE[btsBizTalkServer2006r3](../includes/btsbiztalkserver2006r3-md.md)]。  
  
### <a name="to-regenerate-the-bam-live-data-workbook"></a>重新生成 BAM 实时数据工作簿  
  
1.  单击**启动**，单击**运行**，类型**cmd**，然后单击**确定**。  
  
2.  在命令提示符下，导航到以下目录：[!INCLUDE[btsBiztalkServerPath](../includes/btsbiztalkserverpath-md.md)]Tracking。  
  
3.  类型： **bm.exe 重新生成 livedataworkbook-WorkbookName:mynewbook.xls**  
  
    > [!NOTE]
    >  在支持用户帐户控制 (UAC) 的系统上，可能需要具有管理权限才能运行该工具。  
  
## <a name="see-also"></a>另请参阅  
 [管理 BAM](../core/managing-bam.md)   
 [BAM 管理实用工具](../core/bam-management-utility.md)   
 [使用 for Excel 的 BAM 外接程序的要求](../core/requirements-for-using-the-bam-add-in-for-excel.md)   
 [步骤 1: BAM 外接程序添加到 Microsoft Office Excel](http://msdn.microsoft.com/library/3400969f-0c54-4a75-979d-ad2f7af86448)