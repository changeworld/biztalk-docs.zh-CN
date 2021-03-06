---
title: 使用 Oracle E-business Suite 适配器处理事务 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b443be9d-a93d-4836-8717-5ee9dad4442f
caps.latest.revision: 6
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a9d5bc59cdce4b78a01dc867e12a84eac3b3469d
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37010910"
---
# <a name="handle-transactions-with-the-oracle-e-business-suite-adapter"></a>使用 Oracle E-business Suite 适配器处理事务
[!INCLUDE[adapteroracleebusinesslong](../../includes/adapteroracleebusinesslong-md.md)] 并不会启动 Oracle E-business Suite 中执行操作时的事务。 相反，适配器执行的操作提供的适配器客户端的事务上下文。 若要执行操作在事务中使用[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]，您必须：  
  
-   启用适配器客户端中的事务。 例如，若要启用 BizTalk Server 中的事务，必须选择**使用事务**中的复选框**事务**区域**消息**WCF 自定义选项卡或WCF OracleEBS 端口。  
  
-   设置的值**UseAmbientTransaction**属性绑定到**True**在适配器中。 有关绑定属性的详细信息，请参阅[了解关于 BizTalk Adapter for Oracle E-business Suite 绑定属性](../../adapters-and-accelerators/adapter-oracle-ebs/read-about-the-biztalk-adapter-for-oracle-e-business-suite-binding-properties.md)。  
  
> [!IMPORTANT]
>  若要使用该适配器 Oracle E-business Suite 中执行事务，您必须安装**Microsoft Transaction Server 的 Oracle 服务**组件，同时运行适配器的计算机上安装 Oracle 客户端，客户端。  
  
## <a name="transactions-in-the-outbound-operations"></a>出站操作中的事务  
 [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]在单个事务中执行的出站操作。 复合操作的所有操作都均在单个事务，但使用不同的 ODP.NET 连接。 有关显示的出站操作详细信息[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]，请参阅[原理适配器面 Oracle E-business Suite 元数据？](https://msdn.microsoft.com/library/dd788431.aspx)。  
  
## <a name="transactions-in-the-inbound-operations"></a>入站操作中的事务  
 [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]公开以下两个入站的操作：  
  
- **轮询**： 轮询语句和轮询后语句 （如果指定） 的执行在事务中，而轮询的数据可用语句在不同事务中执行。 同样，轮询语句和轮询后语句的执行使用相同的 ODP.NET 连接，而使用不同的 ODP.NET 连接执行轮询的数据可用语句。  
  
- **通知**： 在使用单个 ODP.NET 连接的事务中执行通知操作。  
  
  有关显示的入站操作详细信息[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]，请参阅[原理适配器面 Oracle E-business Suite 元数据？](https://msdn.microsoft.com/library/dd788431.aspx)。  
  
## <a name="see-also"></a>请参阅  
[了解用于 Oracle E-Business Suite 的 BizTalk 适配器](../../adapters-and-accelerators/adapter-oracle-ebs/understand-biztalk-adapter-for-oracle-e-business-suite.md)