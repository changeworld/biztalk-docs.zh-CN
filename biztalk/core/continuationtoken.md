---
title: ContinuationToken |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2d4911fc-c6fb-4628-9177-bd723d4d8ebc
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 1f0d36737ddd16e34ecfe4680c7660e16c99f676
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37001862"
---
# <a name="continuationtoken"></a>ContinuationToken
继续标记用来关联 BAM 基础结构中各种不同的信息。 假设有一个业务流程用于构造以下类型的消息：  
  
- 由采购订单号标识的采购订单  
  
- 由销售订单号标识的销售订单  
  
- 由发货订单号标识的发货订单  
  
  在此过程中，有三个重要的标识符： 采购订单 ID、 销售订单 ID 和发货订单 id。 其中每个标识符都表示原始订单生存期内的一个重要事件，但这些标示符无法直接关联。 若要跟踪与采购订单相关的事件，必须标识各消息间共有的信息，这样 BAM 跟踪基础结构才能准确地关联事件。  
  
## <a name="format"></a>“格式”  
 继续标记由一个表达式元素和一项或多项运算组成：  
  
```  
<ic:ContinuationToken>  
  <ic:Expression>  
    <!-- Operations -->  
  </ic:Expression>  
</ic:ContinuationToken>  
```  
  
## <a name="remarks"></a>Remarks  
 ContinuationToken 表达式中不允许使用以下常见运算：  
  
- And  
  
- 等于  
  
  [WF/WCF 中的运算部分标头应具有相似的图表及其他图表，具体视需要而定]  
  
## <a name="example"></a>示例  
 在此示例中，WF 流程的继续标记检索从工作流使用`GetWorkflowProperty`。 在此开发人员之所以决定通过使用自定义代码为工作流中的连续符提供支持，可能是因为确定继续标记的流程涉及两个或三个以上的表达式并且可能依赖外部数据。  
  
```  
<ic:ContinuationToken>  
  <ic:Expression>  
    <wf:Operation Name="GetWorkflowProperty">  
      <wf:Argument>ContinuationToken</wf:Argument>  
    </wf:Operation>  
  </ic:Expression>  
</ic:ContinuationToken>  
```  
  
 您可以选择在您的新 WF 或 WCF 应用程序中提供类似功能，或者，如果使用表达式运算创建标记非常简便，则无需编写额外的代码。  
  
 下面的示例通过使用建立为 WCF 流程的继续标记**XPath**操作从当前消息中检索信用卡卡号和**常量**和**串联**操作前面加上"CID_"字符串检索到的号码：  
  
```  
<ic:ContinuationToken>  
  <ic:Expression>  
    <ic:Operation Name="Constant">  
      <ic:Argument>CID_</ic:Argument>  
    </ic:Operation>  
    <wcf:Operation Name="XPath">  
      <wcf:Argument>//Purchase/Payment/CreditCardNumber</wcf:Argument>  
    </wcf:Operation>  
    <ic:Operation Name="Concatenate" />  
  </ic:Expression>  
</ic:ContinuationToken>  
```  
  
## <a name="see-also"></a>请参阅  
 [侦听器 OnEvent 元素](../core/interceptor-onevent-element.md)