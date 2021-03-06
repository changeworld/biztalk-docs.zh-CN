---
title: 定义数据库的自动增长设置 |Microsoft 文档
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dd86dd49-6505-4673-b413-d3af729dfca9
caps.latest.revision: 2
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 1d37bcce2d60167496bc55a12c65a488db17fceb
ms.sourcegitcommit: 32f380810b90b70e5df7be72a6a14988a747868e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2018
ms.locfileid: "29710784"
---
# <a name="define-auto-growth-settings-for-databases"></a>定义数据库的自动增长设置
你应设置为固定数量的兆字节而不是一个百分比，尤其是对于 MessageBox 和 BizTalk 跟踪数据库的数据库自动增长。 根据你的 BizTalk 应用程序和吞吐量，MessageBox 和跟踪数据库可能会非常大。 如果将自动增长设置为百分比，然后自动增长可能是非常高。  
  
## <a name="how-instant-file-initialization-works"></a>如何即时文件初始化的工作原理  
 当 SQL Server 会增加文件的大小时，它必须首先初始化的新空间，然后才能使用。 这是涉及使用空页填充新的空间的阻止操作。 在 Windows 上的 SQL Server 支持"即时文件初始化。" 这可以极大地降低文件增长操作的性能影响。 有关详细信息，请参阅 [数据库文件初始化](https://docs.microsoft.com/sql/relational-databases/databases/database-instant-file-initialization)。 本主题概述了必须谨慎以启用即时文件初始化的步骤。  
  
## <a name="enable-instant-file-initialization"></a>启用即时文件初始化  
 有关步骤启用即时文件初始化，请参阅[数据库文件初始化](https://docs.microsoft.com/sql/relational-databases/databases/database-instant-file-initialization)。 创建文件组并将 BizTalk Server 数据库表、 索引和日志文件移到相应的文件组，请按照中的建议[BizTalk 性能优化指南](../technical-guides/biztalk-server-2013-performance-optimization-guide.md)。 理想情况下支持的文件组的文件的大小应预分配并且如果可能，请设置为静态大小。  
  
 如果新系统并不明确设定静态大小，然后配置带有**启用自动增长**选项并指定文件增长等手段**中兆字节为单位**。 增长增量通常应是不大于 100 MB （适用于大型文件）、 10 MB （适用于中型文件） 或 （适用于小文件） 的 1 MB。
