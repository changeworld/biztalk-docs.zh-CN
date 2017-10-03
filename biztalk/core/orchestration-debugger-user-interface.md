---
title: "业务流程调试器用户界面 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: bts10.hat.orchdebugger
helpviewer_keywords:
- Orchestration Debugger, debug mode
- Orchestration Debugger, Interactive mode
ms.assetid: ca18f1e2-63b7-4177-82ba-4accc3369a2a
caps.latest.revision: "12"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 4663a642ffc960d969c994b5471d866a80fde828
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="orchestration-debugger-user-interface"></a>业务流程调试器用户界面
在交互（调试）模式下，“业务流程调试器”视图包含三个区域：“服务”窗格、“跟踪的事件”窗格以及“业务流程”窗格。 此外，在交互模式下，在视图底部会依次显示“变量列表”和“变量属性”。  
  
> [!NOTE]
>  业务流程调试器不能显示服务的真实状态，除非它出现在**在断点处**模式，并且您已附加它到的实例。  
  
## <a name="service-pane-in-orchestration-debugger"></a>业务流程调试器中的“服务”窗格  
 “业务流程调试器”窗口的顶部窗格显示以下信息：  
  
|标记|详细信息|  
|---------|------------|  
|Name|指示当前视图（业务流程调试器），并可用于导航到“消息流”视图。|  
|实例详细信息|显示唯一标识当前业务流程实例的服务名称和 GUID。|  
|模式|调试模式（重播/实时）、业务流程状态（已启动、已挂起和已完成等等）、已附加（是或否）和断点模式（在类上或在实例上）。|  
|服务选项|该下拉列表根据调试器和实例的状态显示您可以执行的不同操作。|  
  
 在此信息下，业务流程调试器显示有两个窗格，即左侧的“跟踪的事件”窗格和右侧的“业务流程”窗格。  
  
## <a name="tracked-events-pane-in-orchestration-debugger"></a>业务流程调试器 -“跟踪的事件”窗格  
 “跟踪的事件”窗格列出了业务流程中所执行的每个操作的状态，例如操作是已启动还是已完成。 选择此窗格中的每一行时，“业务流程”窗格中的相应形状将以绿色突出显示该形状的开始时间，并以蓝色突出显示该形状的结束时间。  
  
 “跟踪的事件”窗格显示了以下列：  
  
|选项|操作|  
|------------|------------|  
|操作状态（左列）|特定操作的状态。 箭头表示该操作已开始，终止形状则表示该操作已完成。|  
|操作名称|业务流程中操作的名称。|  
|操作类型|表示操作的形状类型。 箭头指示操作已启动和终止形状指示它已完成。|  
|Time|执行操作的时间。|  
|日期|执行操作的日期。|  
  
## <a name="orchestration-pane-in-orchestration-debugger"></a>业务流程调试器中的“业务流程”窗格  
 “组中心”页中消息事件和服务实例跟踪输出中的“业务流程”窗格是业务流程实例呈现其所有形状的区域。 下表列出了“业务流程”窗格的各种上下文菜单操作：  
  
|选项|操作|  
|------------|------------|  
|在类上设置断点|右键单击形状**类上设置的断点**选项。 该形状上将显示一个红点，指示已设置断点。|  
|在实例上设置断点|右键单击形状**实例上设置断点**选项。 该形状上将显示一个红点，指示已设置断点。|  
|删除类上的断点|右键单击形状**删除断点**选项。 该形状的红点将消失，指示断点已删除。|  
|删除实例上的断点|右键单击形状**实例上设置断点**选项。 该形状的红点将消失，指示断点已删除。|  
  
### <a name="variable-list-and-variable-properties-panes"></a>“变量列表”和“变量属性”窗格  
 为时附加到业务流程的运行时使用的交互式调试仅显示这些窗格**附加**服务选项。 这两个窗格显示在屏幕底部。  
  
 “变量列表”显示变量的名称、值和类型。 变量的值指示变量是否为空值，如果不是空值，则指示它包含的对象种类。 类型是**Assembly.Namespace.Name**的对象。  
  
 “变量属性”窗格显示随对象类型而异的变量属性。 例如，对于端口，该窗格将包含地址、名称、作用域、类型和值。 对于消息，则显示快捷方式；对消息的每个部分都会显示相应的名称、大小、属性、类型和值。 诸如上下文和属性之类的集合以弹出方式显示。 另外，会使用值的部分显示作为工具提示。  
  
 用户可以在不同断点之间对调度进行调试，并检查这些变量的状态。  
  
 下表列出了“变量列表”的上下文菜单操作：  
  
|选项|操作|  
|------------|------------|  
|将消息保存|右键单击一条消息，为非 null 的变量列表窗格中**保存消息**选项。 此时，将显示一条消息，提示您选择保存消息的目录。|  
  
### <a name="service-options-drop-down-list"></a>“服务选项”下拉列表  
 “服务选项”下拉列表将根据实例和调试器的状态显示有效的操作。 下表列出了“服务选项”下拉列表中的可用操作：  
  
|选项|操作|  
|------------|------------|  
|继续服务|如果附加了服务，则继续执行在断点处停止的业务流程实例。|  
|恢复为调试模式|以调试模式恢复挂起的业务流程实例。 这样您就可以进入交互模式，附加到实例，然后进行交互调试。<br /><br /> 可从操作视图和业务流程调试器中访问此选项。 它仅适用于业务流程。|  
|终止服务|终止业务流程实例。|  
|附加|将相应的服务附加到业务流程实例并检索当前状态和变量|  
|删除类上的所有断点|删除业务流程类中的所有断点。 只有在没有附加服务的情况下才可用。|  
|移除所有断点|删除业务流程实例中的所有断点。 只有在附加服务的情况下才可用。|  
|保存所有消息|在您选择了对所有入站/出站消息进行跟踪的情况下，保存与业务流程实例关联的所有消息。|  
|显示断点处的操作|用黄色突出显示形状在中断前执行的最后一次操作。|  
|查看调用业务流程|返回到进行调用的业务流程实例的视图。 也就是说，返回到父业务流程。<br /><br /> 此选项只可用于被调用的业务流程实例。|  
  
## <a name="in-this-section"></a>本节内容  
  
-   [报告在业务流程调试器中的模式](../core/reporting-mode-in-orchestration-debugger.md)  
  
-   [在调试器中业务流程交互模式](../core/interactive-mode-in-orchestration-debugger.md)  
  
## <a name="see-also"></a>另请参阅  
 [调试业务流程](../core/debugging-an-orchestration.md)