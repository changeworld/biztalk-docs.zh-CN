---
title: 有关 BizTalk 项目中包含的 BizTalk Namespace 引用 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- System.Xml namespace
- Microsoft.BizTalk.GlobalPropertySchemas namespace
- namespaces, System.Xml namespace
- System namespace
- namespaces, System namespace
- namespaces, Microsoft.BizTalk.GlobalPropertySchemas namespace
- Microsoft.BizTalk.DefaultPipelines namespace
- projects, namespaces
- namespaces, warnings
- namespaces, Microsoft.BIzTalk.DefaultPipelines namespace
- namespaces
ms.assetid: cb642eac-7307-44f8-bbba-3ae364e11ea2
caps.latest.revision: 10
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 608f3ebf9a80553749fe5de558c2db05e3c7673d
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37016365"
---
# <a name="about-biztalk-namespace-references-included-in-biztalk-projects"></a>有关 BizTalk 项目中包含的 BizTalk Namespace 引用
在添加新的 BizTalk 项目时，默认情况下包括以下命名空间：  
  
- **Microsoft.BizTalk.DefaultPipelines**  
  
- **Microsoft.BizTalk.GlobalPropertySchemas**  
  
- **系统**  
  
- **System.Xml**  
  
  您也可以向项目中添加新的引用和 Web 引用。 有关添加详细信息引用使用**项目**菜单中，请参阅[使用 Visual Studio](../core/using-visual-studio.md)。 有关添加 Web 引用的信息，请参阅[添加 Web 引用](../core/adding-web-references.md)。  
  
> [!CAUTION]
>  请不要删除默认引用。 如果删除默认引用，则在项目中引用 BizTalk 项时可能会出现问题。 可以在解决方案资源管理器中还原默认引用。  
  
> [!CAUTION]
>  如果 BizTalk 项目引用另一程序集，而该程序集进行了更新，不会在 BizTalk 项目中自动提取这些更新或更改。 应在解决方案资源管理器中删除过期的引用，然后重新添加引用（重新引用该程序集）。 或者，也可以关闭解决方案并重新打开该解决方案。 无论采用哪一种方法，都可以在项目中使用对所引用的程序集的最新更新。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [Microsoft.BizTalk.DefaultPipelines 引用](../core/microsoft-biztalk-defaultpipelines-reference.md)  
  
-   [Microsoft.BizTalk.GlobalPropertySchemas 引用](../core/microsoft-biztalk-globalpropertyschemas-reference.md)  
  
-   [系统引用](../core/system-reference.md)  
  
-   [System.Xml 引用](../core/system-xml-reference.md)