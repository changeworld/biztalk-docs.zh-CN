---
title: 使用 ESB 异常管理 |Microsoft 文档
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: de6ce411-2d34-4fd8-9644-6fbc9cec266d
caps.latest.revision: 3
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c4eff5a729b8c8ca191b2185180e312f9e895c02
ms.sourcegitcommit: 3fc338e52d5dbca2c3ea1685a2faafc7582fe23a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
ms.locfileid: "26008534"
---
# <a name="using-esb-exception-management"></a>使用 ESB 异常管理
在一组的上下文，并在大量不同的处理阶段中 ESB 期间可能出现错误和异常。 本部分提供有关处理异常的信息，并描述如何在您可以发布通过 ESB 管理门户的详细信息。  
  
## <a name="overview"></a>概述  
 有多种方法在 BizTalk Server 解决方案，包括使用框架，例如 Enterprise Library 中处理异常。 但是，当使用 ESB 和 BizTalk Server 进行开发时, 你会使用基于消息的环境。 在 BizTalk 解决方案中的所有内容都是面向消息的和 BizTalk 开发人员思考面向消息的方式。 因此，[!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]实现异常处理的面向消息的方法。  
  
 ESB 异常管理 Framework 遵循提供灵活的方法，来监视异常并使错误响应为来自外部解决方案的设计模式-可能是在业务部门级别。  
  
 以下主题讨论 ESB 异常管理框架中更多详细信息：  
  
-   [ESB 异常管理框架设计](../esb-toolkit/design-of-the-esb-exception-management-framework.md)  
  
-   [异常管理框架组件](../esb-toolkit/the-components-of-the-exception-management-framework.md)  
  
-   [使用异常管理框架](../esb-toolkit/using-the-exception-management-framework.md)  
  
-   [创建自定义异常处理程序](../esb-toolkit/creating-custom-exception-handlers.md)