---
title: 基本业务流程 Design3 |Microsoft 文档
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- orchestrations, design
ms.assetid: c1df6d0e-51cf-4728-8d55-60eff21611b8
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9823c2ab9221e9348ef891ab4ceb19a732ffbcbf
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
ms.locfileid: "22230709"
---
# <a name="basic-orchestration-design"></a>基本业务流程设计
当创建基本的业务流程时，会出现 XML 中您的业务流程的接收端口。 将 XML 发送到后端系统以供处理。 在后端系统中，可能发生停止业务流程的异常。 生成该异常提供业务流程未完成的信息。  
  
 出现错误时，调用将被挂起。 在事件查看器日志中，您可以查看该故障的错误和原因。  
  
 若要防止业务流程进入挂起状态和重定向错误，您可创建一个 CatchExpression。 若要捕获由后端生成的异常并帮助找到问题起因，可以在业务流程中使用作用域形状。  
  
## <a name="see-also"></a>另请参阅  
 [使用 BizTalk Server 异常处理](../core/using-biztalk-server-exception-handling5.md)