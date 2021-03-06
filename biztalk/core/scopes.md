---
title: 作用域 |Microsoft 文档
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- scopes, exception handling
- Scope shape [Orchestration Designer], nesting
- scopes, variables
- scopes, Scope shape [Orchestration Designer]
- Scope shape [Orchestration Designer], exception handling
- scopes, transactions
- scopes, synchronization
- scopes, nesting
- Scope shape [Orchestration Designer], transactions
ms.assetid: 51d81ce4-0034-4415-b6ab-4c952737c1bd
caps.latest.revision: 11
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 2bc4d1b5d926540477293591ade8123126be1b84
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
ms.locfileid: "22269773"
---
# <a name="scopes"></a>作用域
作用域是用于对操作进行分组的一种框架。 作用域主要用于事务性执行和异常处理。  
  
 一个作用域包含一个或多个块。 作用域具有正文并且可以选择附加任意数目的异常处理块。 它也可以具有可选的补偿模块，这由该作用域的特性决定。 某些作用域将仅用于异常处理，不要求补偿。 其他一些作用域将是显式事务性的，并且将始终具有默认的补偿处理程序以及您为它创建的可选的补偿处理程序。 事务性作用域也将具有默认的异常处理程序以及您为它创建的任意数目的附加异常处理程序。  
  
## <a name="synchronized-scopes"></a>同步的作用域  
 您可以指定作用域是同步的还是非同步的。 通过同步某个作用域，您将确保在该作用域中访问的任何共享数据都不会被一个或多个并行操作写入您的业务流程，也不会在其他操作正在读取它时写入业务流程。  
  
 原子事务作用域始终是同步的。 同步的作用域中的所有操作都被视为同步的，其任何异常处理程序中的所有操作也都被视为同步的。 事务作用域的补偿处理程序中的操作是非同步的。  
  
> [!CAUTION]
>  请注意，如果不认真设计您的流程，仍可能会遇到死锁情况。 例如：业务流程 A 中并行的两个分支都访问同一消息，一个要发送该消息，一个要接收该消息，因此，这两个分支必须具有同步的作用域。 第二个业务流程接收该消息并发送回该消息。 业务流程 A 中的发送分支有可能在接收分支前收到对其的锁定，因此您将以死锁结束。  
  
## <a name="nesting-of-scopes"></a>作用域嵌套  
 可以嵌套**作用域**内其他形状**作用域**形状。 嵌套作用域的规则如下：  
  
-   事务作用域和/或同步的作用域不能嵌套在同步的作用域内，包括同步的作用域的异常处理程序。  
  
-   原子事务作用域不能在其内部嵌套任何其他事务作用域。  
  
-   事务作用域不能嵌套在非事务作用域或业务流程内。  
  
-   你可嵌套最大深度 21 级的作用域。  
  
-   **调用 Orchestration**形状可以包括在作用域，但调用业务流程将被视为与任何其他相同嵌套事务，并应用相同的规则。  
  
-   **启动业务流程**形状可以包括在作用域内。 对嵌套的限制并不适用于已启动的业务流程。  
  
## <a name="scope-variables"></a>作用域变量  
 可以在作用域一级上声明消息或相关集之类的变量。 但是，作用域变量的名称不能与业务流程变量的名称同名；不允许名称隐藏。  
  
## <a name="see-also"></a>另请参阅  
 [使用事务和处理异常](../core/using-transactions-and-handling-exceptions.md)   
 [原子事务](../core/atomic-transactions.md)