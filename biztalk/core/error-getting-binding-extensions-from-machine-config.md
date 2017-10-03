---
title: "从 machine.config 中获取绑定扩展时出错 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 65ab48cf-575b-4db6-984a-880f7e286959
caps.latest.revision: "10"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: b8dfdedb58e4372caed38c7c272cbaaf65fefbcb
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="error-getting-binding-extensions-from-machineconfig"></a>从 machine.config 获取绑定扩展时出错。
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]|  
|产品版本|[!INCLUDE[btsWCFVersion](../includes/btswcfversion-md.md)]|  
|事件 ID|0|  
|事件源|0|  
|组件|0|  
|符号名称|0|  
|消息正文|从 machine.config 获取绑定扩展时出错。|  
  
## <a name="explanation"></a>解释  
 当接收位置或发送端口绑定配置具有用户定义的绑定扩展，但 machine.config 文件中未定义该扩展时，发生此错误。 这种情况主要会出现的 WCF 自定义和 WCF CustomIsolated 适配器。  
  
## <a name="user-action"></a>用户操作  
 在 machine.config 文件中定义接收位置或发送端口中使用的绑定扩展。 同时，要获取自定义行为或绑定元素以使用 WCF-Custom 适配器，请完成这些步骤：  
  
1.  GAC 程序集  
  
2.  修改 machine.config 文件 (位于**%FrameworkDir%\v4.0.30319\CONFIG**)。  
  
    1.  加载你的行为 DLL 在服务配置编辑器 (**svcConfigEditor.exe**)。  
  
    2.  保存到配置**app.config**文件  
  
    3.  复制并粘贴**system.servicemodel** machine.config 中的类似节中的扩展部分。如果**system.servicemodel**部分不在 machine.config，你必须创建一个。 以下是 machine.config 文件的配置部分的示例：  
  
        ```  
          <system.serviceModel>  
            <extensions>  
              <behaviorExtensions>  
                <add name="BizTalkWcfContractNamespaceTestServiceBehaviorExtension" type="ASB.BizTalk.Samples.BizTalkWcfContractNamespaceTestServiceBehaviorExtension, CustomBizTalkWcfBehaviors, Version=1.0.0.0, Culture=neutral, PublicKeyToken=7631521c07cf34b4" />  
              </behaviorExtensions>  
            </extensions>  
          </system.serviceModel>  
        ```  
  
> [!NOTE]
>  此外可以将上面的代码添加到 WCF 扩展选项卡。如果扩展需要在接收端，请参阅**\<主机名 > 属性对话框中，WCF 扩展**选项卡 （WCF 自定义或 WCF CustomIsolated 适配器接收处理程序） [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。 如果扩展需要在发送端，请参阅**\<主机名 > 属性对话框中，WCF 扩展**选项卡 （WCF 自定义适配器发送处理程序） [!INCLUDE[ui-guidance-developers-reference](../includes/ui-guidance-developers-reference.md)]。  
  
 3. 关闭并重新打开管理控制台。 您应该能够在 WCF-Custom 适配器中查看您的自定义行为，并且当您启用时端口应保持启用状态。