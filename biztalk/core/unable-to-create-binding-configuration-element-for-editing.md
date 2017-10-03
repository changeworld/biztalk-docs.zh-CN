---
title: "无法创建以进行编辑的绑定配置元素 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 71853662-5a4a-417e-8160-c93dbcbea336
caps.latest.revision: "16"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a5c4387e0cb9287ecc4d491291fdfd1fa6b79ab9
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="unable-to-create-binding-configuration-element-for-editing"></a>法创建要编辑的绑定配置元素
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]|  
|产品版本|[!INCLUDE[btsWCFVersion](../includes/btswcfversion-md.md)]|  
|事件 ID|0|  
|事件源|0|  
|组件|0|  
|符号名称|0|  
|消息正文|无法创建绑定配置元素以进行编辑。 检查 BindingType 和 BindingConfiguration 属性的值。|  
  
## <a name="explanation"></a>解释  
 加载绑定元素以显示在用户界面中时出错。 此错误通常发生在自定义绑定中。 配置文件中的绑定元素可能已丢失，因此绑定下拉列表中没有该元素。  
  
## <a name="user-action"></a>用户操作  
 检查的值**BindingType**和**BindingConfiguration**属性。  
  
 有关创建绑定配置元素的详细信息，请参阅以下资源：  
  
-   [配置 WCF NetMsmq 适配器](../core/configuring-the-wcf-netmsmq-adapter.md)