---
title: 就是测试的重要性的原因 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ce91aca5-56d3-4fb8-abe2-af0039804706
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a74f22813f9752f82985d2e984f5effeb3208e6e
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37009166"
---
# <a name="why-it-is-important-to-test"></a>是测试的重要性
本主题提供的思维方式，实现对不足，无法测试概述介绍与故障来测试 BizTalk 解决方案相关的风险和对比优势的自动测试的手动测试的缺陷。  
  
## <a name="testing-as-overhead"></a>测试作为"开销"  
 遗憾的是，与渐增的投资回报 (ROI) 的需求，项目的测试阶段往往会出现一个方面可以是项目计划的第一个调整至后。  
  
 一个自变量的测试 BizTalk 解决方案是，"我们不需要测试我们的解决方案，因为 Microsoft 已进行全面测试 BizTalk Server。" True，Microsoft 彻底测试 BizTalk Server 时，不同的使用方案需要一个几乎无数的业务需求的排列数的吞吐量、 高可用性，适配器使用情况、 延迟、 跟踪要求，业务流程使用情况和自定义代码。 BizTalk Server 是极其灵活，只能适应这么多不同的使用方案，因为它不只是能预测和测试所有这些。 此外，在 BizTalk Server 环境中应用的默认设置应进行优化以适应每个使用方案。 确定特定使用方案的最优设置的唯一方法是测试解决方案、 测量各种参数、 优化环境，并重新测试。 请考虑下图描绘了 BizTalk Server 解决方案的示例物理体系结构。  
  
 ![BizTalk Server 部署的体系结构](../technical-guides/media/5359cf00-e285-4168-a988-8d3b677eb6ba.gif "5359cf00-e285-4168-a988-8d3b677eb6ba")  
示例物理 BizTalk 体系结构  
  
 您可以看到在上面的关系图中的 BizTalk Server 解决方案包含很多移动部件，包括多台计算机运行 BizTalk Server 中，运行 SQL Server、 服务器群集节点和 Active Directory 域的计算机。 系统已启动并运行后，将应用于优化每个业务要求，并使该解决方案的总体投资回报率最大化应用程序的许多配置调整。 这种单一方案显示了在 play 中有多个变量。 除了环境的物理体系结构，请考虑下图中，描述了通过 BizTalk Server 消息流。  
  
 ![通过 BizTalk Server 的消息流](../technical-guides/media/dea79a42-5f60-49a1-abdb-870988784ffe.gif "dea79a42-5f60-49a1-abdb-870988784ffe")  
示例逻辑 BizTalk 消息流  
  
 当我们查看 BizTalk Server 处理的消息的逻辑图时，我们看到的需要测试每个项目，包括自定义发送和接收管道组件和自定义类，可以从 BizTalk 业务流程调用其他变量。 考虑到的类型的复杂性和使用自定义组件和 BizTalk 组件而异项目到项目，变得更为明显就是执行每个特定使用方案测试重要的原因。  
  
## <a name="testing-methodology-and-timelines"></a>测试方法和时间线  
 若要确保有效和高效地执行测试，测试工具应该是完全自动; 因此它是比较容易再现并最大程度减少人为错误的可能性。 此外，应为测试计划项目时所分配足够的时间。 测试最低要求方法将包含类似于以下手动步骤：  
  
1. 手动加载到接收终结点，如文件删除或通过使用 SOAP 客户端调用 Web 服务的一个或多个消息。  
  
2. 手动验证正确的内容和消息的结构。 因为通常在项目中存在多个架构时，消息可能是混合使用平面文件和 XML，也可能包含跨字段依赖项。  
  
   > [!NOTE]  
   >  此示例将涉及 SWIFT 消息的任何项目。 这些是依赖项跨字段的平面文件消息。 也就是说，一个字段的值依赖于另一个 – 不会; 执行简单的 XSD 验证因此 SWIFT 加速器将用于验证消息的 BizTalk 规则引擎使用。 有关详细信息[SWIFT 加速器](http://go.microsoft.com/fwlink/?LinkID=79657)，请参阅[SWIFT 加速器](http://go.microsoft.com/fwlink/?LinkID=79657)(http://go.microsoft.com/fwlink/?LinkID=79657)。  
  
3. 手动检查有错误的 BizTalk Server 计算机上的事件日志。  
  
4. 手动检查 BAM 数据库 （如果使用） 来验证正确记录活动信息。  
  
   使用手动过程，如上文所述的测试是一个主观问题且容易出错。 请考虑无需检查上百行 SWIFT 消息与跨 10 个不同的测试用例字段依赖关系。 大多数项目将不能为开发人员，或即使它们是可以的将不倾向于可靠、 精确地参与此类任务。 主观、 手动错误不易测试过程的实现添加到项目的风险，并会增加故障的可能性。  
  
   失败的风险通常会放大的项目规划未包含足够的时间进行测试的时间线。 时常测试策略枢轴上这是一个单一的手动测试传递的项目计划一周左右的推出日期之前。 这种有限的测试将项目放在风险。 给定的测试，这种有限的时间线，如果检测到任何问题，然后项目可能会延迟，因为分配了没有时间来解决问题。 此外，如果问题是发现并修复，可能有没有足够的时间保留系统投入之前执行后续测试通过。  
  
   "单个最终生成，单个测试通过，take 项目 live"的测试是，它通常会导致延迟的项目、 项目超出预算，或甚至更糟的是，完全失败的项目 ！ 对于关键任务系统，这种测试方法是待势灾难。  
  
## <a name="testing-effectively-and-efficiently"></a>测试有效性和效率  
 通常被视为昂贵 luxury 而不是整型要求相应的测试，因为它是经常附加，在项目的结尾。 考虑到不同种类企业环境中使用的软件和硬件堆栈的复杂性，这种方法并不现实。 可以按需重新运行自动的测试方法的实现是测试有效性和效率的最佳方法，最终为企业提供优秀 ROI 的项目取得成功的必备组件。 通过投资中完整的端到端功能的每个代码路径通过系统测试的项目的开始处为生成测试资产。 这些资产需投资 （即开发时间） 中获益，提高了测试有效性和效率更高版本。 若要从项目需要派生此类框架的投资最大程度减少我们建议你利用 Visual Studio 2010 负载测试框架。 Visual Studio 2010 包括大多数测试成功所需的常见测试步骤，是在本指南中稍后介绍的测试方案中使用的框架。  
  
## <a name="see-also"></a>请参阅  
 [实现自动测试](../technical-guides/implementing-automated-testing.md)