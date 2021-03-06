---
title: 使用 BizTalk 映射器 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- bts10.mapper.grid
ms.assetid: 07c69603-ee79-44b2-80b1-6ae4e4c8fb4e
caps.latest.revision: 29
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: dfa3ac3d03e5f9537284ea4e4371ab5a443d2b42
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36967526"
---
# <a name="using-biztalk-mapper"></a>使用 BizTalk 映射器

## <a name="overview"></a>概述
BizTalk 映射器驻留在 [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] Shell 中。 BizTalk 映射器中的某些功能依赖于 [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] Shell 的用户界面元素。 例如，使用**文件**，**编辑**，并**视图**菜单正如您将在执行其他开发[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]。 提供了有关此通用功能的信息**帮助**菜单。  
  
 在向 BizTalk 项目添加新的映射，打开现有的映射（.btm 文件）或在 [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] 主编辑窗口中单击与映射相应的选项卡重新激活该映射时，BizTalk 映射器将变为活动状态。  
  
> [!NOTE]
>  BizTalk 映射器使用 UTF-16 字符编码保存映射文件。  
>
>  生成操作时向 BizTalk 项目添加现有项目，请始终设置为**BtsCompile**。 即使在重命名现有项目，其生成操作设置为默认值**BtsCompile**。 因此，添加或重命名现有项目时，您需要根据是否需要生成该特殊项目来对生成操作进行相应设置。  

## <a name="parts-of-the-biztalk-mapper"></a>BizTalk 映射器的各个部分  
 下图显示了 [!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)] 中 BizTalk 映射器的各个部分。  
  
 ![BizTalk 映射器](../core/media/mapper-views.gif "Mapper_Views")  
  
 每个视图的功能如下：  
  
- **Visual Studio 映射器实用工具功能区。** [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]映射器提供了显示映射器相关命令的实用工具功能区。 该功能区提供源架构信息、用于源和目标架构的关联视图的切换按钮、用于显示或隐藏所有作用域链接的切换按钮、用于打开或关闭自动滚动的切换开关、用于平移映射器界面的按钮、用于放大或缩小的控件以及搜索文本框。 下图显示了您可以在网格页顶部看到的实用工具功能区。  
  
   ![映射器功能区](../core/media/mapper-ribbon.gif "Mapper_Ribbon")  
  
- **源架构树视图。** 此视图共享主[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]编辑与目标架构树视图和网格视图窗口。  
  
   顾名思义，此视图显示了描述作为映射源的实例消息的架构。 定义映射的链接可引导您从源架构树视图进入网格视图，并最终进入目标架构树视图。  
  
   有关 BizTalk 架构在架构树视图中的表示方式的详细信息，请参阅[BizTalk 架构表示法](../core/biztalk-representation-of-schemas.md)。  
  
- **目标架构树视图。** 此视图共享主[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]编辑与源架构树视图和网格视图窗口。  
  
   顾名思义，此视图显示了描述作为映射目标的实例消息的架构。 定义映射的链接可引导您从网格视图进入目标架构树视图，并最终从源架构树视图进入。  
  
   有关 BizTalk 架构在架构树视图中的表示方式的详细信息，请参阅[BizTalk 架构表示法](../core/biztalk-representation-of-schemas.md)。  
  
- **网格视图。** 此视图共享主[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]编辑与源架构树视图和目标架构树视图中，使用左侧的源架构树视图和目标架构树视图右侧的窗口。  
  
   顾名思义，此视图在映射定义中扮演着关键角色，其中包含控制如何将源实例消息中的数据转换至符合目标架构的实例消息的链接和 functoid。  
  
   网格视图可以具有多个层（称为网格页），通过使用这些层，可以将复杂映射组织到映射的逻辑分支中。 网格页所使用的空间通常比一次可以显示的空间要多，有多种有效方法可以在网格页中进行滚动。  
  
   目前您可使用此视图构建映射。  
  
- **Visual Studio 工具箱窗口。** 此视图用于显示可在 BizTalk 映射中使用的 functoid，并用作拖放操作源以将 functoid 置于网格页中。  
  
   “工具箱”中显示的 functoid 按类别进行组织。 有关可用的 functoid 的详细信息，请参阅[映射中的 Functoid](../core/functoids-in-maps.md)。 另请参阅**Functoid 参考** [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。 
  
- **Visual Studio 属性窗口。** 此视图及其关联对话框用于检查和设置你为定义映射而创建的链接和 functoid。  
  
   在网格视图中的网格页中选择链接或 functoid，在源或目标架构树视图，选择 schema 节点或中选择映射**解决方案资源管理器**窗口; 该链接，functoid 的相应属性schema 节点或映射中出现**属性**窗口使用标准的 Visual Studio 约定。 例如，属性将分组为不同的类别，您可以按这些类别或按字母顺序显示属性。  
  
   有关不同的可用于链接、 functoid、 schema 节点或映射本身的属性集的详细信息，请参阅**映射属性参考**和**Schema Property Reference**[!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)].  
  
- **Visual Studio 任务列表和输出窗口。** 这些视图用于检查执行以下操作的结果：通过在编译源代码和生成其他类型的项目时使用这些视图的相同方式，验证、编译和测试 BizTalk 映射。  
  
  除了这些视图外，你还可以与几个对话框交互。 在编辑诸如 functoid 输入参数等复杂属性时，通常会打开这些对话框。  
  
  “解决方案资源管理器”窗口通常与 BizTalk 映射器结合使用。 例如，若要创建新的映射，请右键单击 BizTalk 项目中的**解决方案资源管理器**窗口中，单击**添加**，单击**添加新项**，然后使用**添加新项**对话框进行命名和创建新的映射。  
  
## <a name="next-steps"></a>后续步骤
  
-   [使用 BizTalk 映射器命令](../core/using-biztalk-mapper-commands.md)  
  
-   [使用网格页](../core/working-with-grid-pages.md)  
  
-   [如何管理视图](../core/how-to-manage-views.md)  
  
-   [如何自定义的颜色和字体在 BizTalk 映射器](../core/how-to-customize-colors-and-font-in-biztalk-mapper.md)  
  
-   [如何展开和折叠架构树](../core/how-to-resize-the-schema-picker-and-expand-and-collapse-the-schema-trees.md)  
  
-   [如何撤消或重做用户操作](../core/how-to-undo-or-redo-user-operations.md)  
  
-   [如何搜索映射项](../core/how-to-search-for-map-items.md)  
  
-   [使用 BizTalk 映射器中的增强功能](../core/using-enhanced-features-in-biztalk-mapper.md)  
  
-   [如何查看信息提示和工具提示](../core/how-to-view-infotip-and-tooltip.md)  
  
## <a name="see-also"></a>请参阅  
 [如何优化链接的显示](../core/how-to-optimize-the-display-of-links.md)