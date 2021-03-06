---
title: 字段属性节点 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9e964c07-53e5-473f-84f2-05af4796cbbe
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: ef3cbf401ce5408c59ae164ca528c41a647eba2f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36972134"
---
# <a name="field-attribute-nodes"></a>“字段属性”节点

## <a name="overview"></a>概述
在 BizTalk 编辑器中，使用**字段属性**节点可以是简单在本质上，如字符串和数字信息的项进行说明。 此外，它们用于时有问题的信息显示为一条消息，而不是显示为一个 XML 元素的内容的实际实例中的属性的值。 有关其他信息存储为元素内容的信息，请参阅[字段元素节点](../core/field-element-nodes.md)。  

 虽然最简单的方式使用**字段属性**节点是为的子节点**记录**节点，它们还可以使用为的子节点**属性组**节点。 在后一种情况下，**字段属性**节点的子级**属性组**节点都可用作属性的任何**记录**包括该的节点**属性组**节点。 有关详细信息**属性组**节点，请参阅[属性组节点](../core/attribute-group-nodes.md)。  

> [!NOTE]
>  在 BizTalk 编辑器中的元素和属性元素只能通过**字段**节点，但它们具有不同的图标与它们关联在架构树视图中，XSD 窗口中的不同 XML 表示形式和在 Visual Studio 属性窗口中的不同属性。  

 对于任何给定项的项信息意味着单一的离散简单类型，例如字符串或数字，其中一条 XML 消息中的信息有始终是一个有关是否应将该信息表示为属性的元素，或作为的问题该元素的子元素。 作为一般规则，表示的某项信息，如属性往往是更合适时可能的值为离散，几个单位，往往可以修改该元素本身的语义。 代表，往往是更合适时的可能值可以重复的次数，可变数量的子元素的某项信息可能具有更广泛范围的值，可能会很长，如下所示的长字符串，并同级的几个值之一，它们的顺序是相关。 如果你创建现有类型的 XML 架构文档，使用的所选**字段元素**节点或**字段属性**节点信息的特定项的已完成，并您必须使用与 XML 相匹配的节点。  

> [!NOTE]
>  根节点可能没有**字段**属性。 **字段**特性附加到**根**节点将不与架构一起保存。  

## <a name="xsd-representation"></a>XSD 表示形式  
 当**字段属性**节点插入到**记录**节点，在任何其他子节点结尾处插入该实体**记录**节点。 其中包括之后插入**序列**，**选**，或**所有**元素，其中包含任何非属性节点，和以前的所有属性节点后插入。 下面的示例显示了一个新**字段属性**节点，以粗体显示的末尾插入**记录**节点，其中对节点进行了命名以说明其标识）。  

```  
<xs:element name="ContainingRecord">  
    <xs:complexType>  
        <xs:sequence>  
            <xs:element name="FieldElement" type="xs:string" />  
            <xs:element name="EmptyNestedRecord">  
                <xs:complexType />  
            </xs:element>  
        </xs:sequence>  
        <xs:attribute name="ExistingFieldAttribute" type="xs:string" />  

    </xs:complexType>  
</xs:element>  

```  

## <a name="see-also"></a>请参阅  
- [架构的 BizTalk 表示形式](../core/biztalk-representation-of-schemas.md)   
- [节点属性](../core/node-properties.md)   
- **字段元素节点属性** [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]  
- [如何设置节点属性](../core/how-to-set-node-properties.md)   
- [“属性组”节点](../core/attribute-group-nodes.md)
