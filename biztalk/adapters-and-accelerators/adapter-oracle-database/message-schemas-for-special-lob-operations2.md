---
title: "特殊 LOB Operations2 的消息架构 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- LOB data types, message structure of
- LOB data types, message actions for
ms.assetid: 031989d5-3209-41ab-8836-a40539781e74
caps.latest.revision: "4"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 203ffc81b6dc85fcaf7b80ff097bbeb001b747cd
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="message-schemas-for-special-lob-operations"></a>特殊 LOB 操作的消息架构
表和视图包含 LOB 列; 中加以表示的 ReadLOB 和 UpdateLOB 操作这就是用于存储 Oracle 大型对象 (LOB) 数据的列。 这些操作，可以读取或写入 LOB 数据作为 base64Binary 编码数据的流。 它们对单个列的单个行中的 LOB 数据的操作。  
  
 ReadLOB 和 UpdateLOB 操作和支持的 Oracle LOB 数据类型的概述，请参阅[对表和视图包含 Oracle 数据库中的 LOB 数据的操作](../../adapters-and-accelerators/adapter-oracle-database/operations-on-tables-and-views-that-contain-lob-data-in-oracle-database.md)。  
  
## <a name="message-structure-of-lob-data-type-operations"></a>LOB 数据类型操作的消息结构  
 下表显示对于 ReadLOB 和 UpdateLOB 操作请求和响应消息的结构。 该操作的目标表中的消息操作指定，也会出现在目标命名空间。  
  
|运算|XML 消息|Description|  
|---------------|-----------------|-----------------|  
|ReadLOB|`<ReadLOB xmlns="[VERSION]/[SCHEMA]/Table/[TABLE_NAME]">   <LOB_COLUMN>[COL_NAME]</LOB_COLUMN>   <FILTER>[WHERE_clause]</LOB_COLUMN> </ReadLOB>`|中的 LOB 数据<br /><br /> -LOB_COLUMN 元素中，标识列和<br /><br /> -行相匹配 where 子句筛选器元素中指定<br /><br /> 返回。<br /><br /> Where 子句应匹配只有一行。 如果没有多个匹配行，则返回第一个匹配行中的 LOB 数据。<br /><br /> **重要**ReadLOB 操作旨在支持的 WCF 服务模型中的 LOB 数据的输入流。 应使用表选择操作从 WCF 通道模型读取 LOB 数据或[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]解决方案。|  
|ReadLOB 响应|`<ReadLOBResponse xmlns="[VERSION]/[SCHEMA]/Table/[TABLE_NAME]">   <ReadLOBResult>     [LOB_DATA]   </ReadLOBResult> </ReadLOBResponse>`|LOB 数据作为 base64Binary 编码数据的流返回。<br /><br /> **重要**适配器返回的 WSDL 与用于适配器 ReadLOB 响应消息的实际架构不匹配。|  
|UpdateLOB|`<UpdateLOB xmlns="[VERSION]/[SCHEMA]/Table/[TABLE_NAME]">   <LOB_COLUMN>[COL_NAME]</LOB_COLUMN>   <FILTER>[WHERE_clause]</LOB_COLUMN>   <Stream>[LOB_DATA]</Stream> </UpdateLOB>`|中的 LOB 数据<br /><br /> -LOB_COLUMN 元素中，标识列和<br /><br /> -行相匹配 where 子句筛选器元素中指定<br /><br /> 使用流中的 base64Binary 编码数据更新。<br /><br /> Where 子句应匹配只有一行。 如果有多个匹配行，将引发异常。<br /><br /> **请注意**UpdateLOB 操作将替换所有指定的列和行中的数据。|  
|UpdateLOB 响应|`<UpdateLOBResponse xmlns="[VERSION]/[SCHEMA]/Table/[TABLE_NAME]"> </UpdateLOBResponse>`|返回一个空响应。|  
  
 [VERSION] = 消息版本字符串;例如，"http://Microsoft.LobServices/OracleDB/2007/03"。  
  
 [架构] = Oracle 集合项目;例如，SCOTT。  
  
 [TABLE_NAME] = 包含目标的 LOB 列; 的表例如，EMP。  
  
 [COL_NAME] = 目标的 LOB 列; 的名称例如，LOB_FIELD。  
  
 [WHERE_clause] = An Oracle 数据库的 SELECT 语句的 WHERE 子句，匹配单个行;例如，ID = 1。  
  
 [LOB_DATA] = base64Binary 类型中的 LOB 列数据。  
  
> [!IMPORTANT]
>  在视图上的 ReadLOB 和 UpdateLOB 操作的消息结构相同表只是该操作的命名空间指定视图而不是表： `<ReadLOB xmlns ="[VERSION]/[SCHEMA]/``View``/[VIEW_NAME]">`。  
  
## <a name="message-actions-for-lob-data-type-operations"></a>LOB 数据类型操作的消息操作  
 下表显示使用的消息操作[!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]表上的 ReadLOB 和 UpdateLOB 操作。 [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)]使用的消息操作中指定的表名称来确定该操作的目标表。  
  
|运算|操作|示例|  
|---------------|------------|-------------|  
|ReadLOB|`[VERSION]/[SCHEMA]/Table/[TABLE_NAME]/ReadLOB`|`http:/Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/CUSTOMER/ReadLOB`|  
|ReadLOB 响应|`[VERSION]/[SCHEMA]/Table/[TABLE_NAME]/ReadLOB/response`|`http:/Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/CUSTOMER/ReadLOB/response`|  
|UpdateLOB|`[VERSION]/[SCHEMA]/Table/[TABLE_NAME]/UpdateLOB`|`http:/Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/CUSTOMER/UpdateLOB`|  
|UpdateLOB 响应|`[VERSION]/[SCHEMA]/Table/[TABLE_NAME]/UpdateLOB/response`|`http:/Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/CUSTOMER/UpdateLOB/response`|  
  
 [VERSION] = 消息版本字符串;例如，"http://Microsoft.LobServices.OracleDB/2007/03"。  
  
 [架构] = Oracle 集合项目;例如，SCOTT。  
  
 [TABLE_NAME] = 包含目标的 LOB 列; 的表例如，客户。 (SCOTT。CUSTOMER 表是由安装这些示例中包含的 SQL 脚本。）  
  
> [!IMPORTANT]
>  在视图上的 ReadLOB 和 UpdateLOB 操作的消息操作类似于用于表，只是操作的操作指定了一个视图，而不是表： `[VERSION]/[SCHEMA]/View/[VIEW_NAME]/ReadLOB`。  
  
## <a name="see-also"></a>另请参阅  
 [消息和用于 Oracle 数据库的 BizTalk Adapter 的消息架构](../../adapters-and-accelerators/adapter-oracle-database/messages-and-message-schemas-for-biztalk-adapter-for-oracle-database.md)