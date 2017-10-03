---
title: "如何在向地图添加大容量复制 Functoid |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1cff63fc-8f34-4bd0-8501-a8401bde6349
caps.latest.revision: "8"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 4cee6f2c53bbd3b3dbabe55f0160309532d0ebf3
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-add-mass-copy-functoids-to-a-map"></a>如何向映射中添加“批量复制”Functoid
**大容量复制**functoid 使你使用包含的架构的映射**任何**和**anyAttribute**元素。 实际上，这些元素是 XML 架构定义语言为匹配未知结构或属性集而提供的通配符。  
  
 有关概念性信息**大容量复制**functoid，请参阅[大容量复制 Functoid](../core/mass-copy-functoid.md)。  
  
### <a name="to-add-the-mass-copy-functoid-to-a-map-and-configure-it"></a>向映射添加“批量复制”functoid 并对其进行配置  
  
1.  与[!INCLUDE[btsVStudioNoVersion](../includes/btsvstudionoversion-md.md)]工具箱处于活动状态，单击**高级 Functoid**选项卡以选择 functoid 该类别。  
  
     此时，将显示所选类别的高级 functoid 列表。  
  
2.  拖动**大容量复制**functoid (![](../core/media/advmasscopy.gif "advmasscopy")) 从工具箱拖到网格页上的适当位置。  
  
    > [!NOTE]
    >  该 functoid 将放置到显示的网格页上。 如果你想要将 functoid 放到不同的网格页面上，你需要首先显示其他网格该页。  
  
    > [!NOTE]
    >  如果是构造使用多个 functoid 的映射，则需要考虑它们的左右位置关系。 Functoid 是按照从左到右的顺序执行的。 一个 functoid 的输出只能输入到其右侧的另一个 functoid 中。  
  
3.  若要建立的输入的参数**大容量复制**functoid，通过将一条记录拖到源架构中创建的输入的链接**大容量复制**functoid，或拖动**大容量复制** functoid 到源架构中的记录。  
  
4.  若要使用输出参数从**大容量复制**functoid，通过拖动创建一条输出链接**大容量复制**到记录在目标架构中，或通过将一条记录拖到目标架构中的 functoid**大容量复制**functoid。  
  
    > [!NOTE]
    >  与其他 functoid，您不能使用的输出**大容量复制**functoid 作为另一个 functoid 的输入。  
  
> [!NOTE]
>  你可以插入和配置**大容量复制**通过链接两个 functoid 直接记录。 详细信息，请参阅"使用大容量复制 functoid 链接"部分中[如何自动链接记录](../core/how-to-link-records-automatically.md)。  
  
## <a name="see-also"></a>另请参阅  
 [向地图添加高级的 Functoid](../core/adding-advanced-functoids-to-a-map.md)