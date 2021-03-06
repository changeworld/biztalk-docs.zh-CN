---
title: BAM 动态基础结构 |Microsoft 文档
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- infrastructure, BAM
- BAM, infrastructure
ms.assetid: 88f39438-3213-4f0d-8b8d-e6426c266138
caps.latest.revision: 12
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 3660eeb6f85fb21ff78b7b833b21adbb3af87385
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
ms.locfileid: "22230445"
---
# <a name="bam-dynamic-infrastructure"></a>BAM 动态基础结构
BAM 基础结构包含的 SQL Server 表、 BAM 视图、 存储的过程和作为配置和通过增量托管的 BAM 数据库 （主导入、 存档、 星型架构和分析） 中的数据转换服务 (DTS) 包部署的 BAM 定义。 基础结构是其中，在运行时，事件是关联、 聚合，并且之后可用于查询的用户。  
  
 本部分介绍一些基础结构流程。 例如，从应用程序（BAM 定义）提取目标数据后，可以将其存储以便进行查询。 此外，可以维护预先创建的特定数据聚合，以使聚合查询更加迅速。  
  
 通常，需要在实现数据仓库方面进行广泛的开发工作才能实现此功能。 但是，Microsoft [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 中的 BAM 大大简化了此过程，因为其基于活动和视图定义自动生成 SQL 和 OLAP 基础结构。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [BAM 定义是什么？](../core/what-is-a-bam-definition.md)  
  
-   [什么是 BAM 定义架构？](../core/what-is-a-bam-definition-schema.md)  
  
-   [活动数据存储](../core/activity-data-storage.md)  
  
-   [聚合是什么？](../core/what-is-an-aggregation.md)  
  
-   [查询 BAM 数据](../core/querying-bam-data.md)  
  
-   [BAM 基础结构限制](../core/bam-infrastructure-limitations.md)  
  
-   [如何在非英语安装中定义的范围外数值维度警报](../core/define-out-of-range-numeric-dimension-alerts-in-non-english-installations--bam.md)