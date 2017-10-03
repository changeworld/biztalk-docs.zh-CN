---
title: "Siebel 适配器中的 SiebelParameter 类 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SiebelParameter
- Data Provider for Siebel, SiebelParameter
- SiebelParameter, supported properties and methods
ms.assetid: 1dcb72c7-a470-4609-8aba-a5c8ad5f3ac9
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 27df4b207b23cd04f7d29a2a18ec4ab032836e5b
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="siebelparameter-class-in-the-siebel-adapter"></a>Siebel 适配器中 SiebelParameter 类
[!INCLUDE[adoprovidersiebelshort](../../includes/adoprovidersiebelshort-md.md)]提供`DbParameter`实现，若要启用的 ADO.NET 客户端可以指定特定命令的参数。 使用的实例`System.Data.Common.DbCommand`类[!INCLUDE[adoprovidersiebelshort](../../includes/adoprovidersiebelshort-md.md)]，客户端程序可以获取的实例`System.Data.Common.DbParameter`类。  
  
```  
//In this example, command is an instance of DbCommand  
DbParameter param = command.CreateParameter();  
```  
  
 或者，可以使用以下方法：  
  
```  
  
//Here command is an instance of SiebelCommand  
SiebelParameter param = (SiebelParameter) command.CreateParameter();                  
param.ParameterName = "@Time";  
```  
  
 `SiebelParameter`类继承自`DbParameter`。  命名空间中存在`Microsoft.Data.SiebelClient`。  
  
## <a name="supported-properties"></a>受支持的属性  
 `SiebelParameter`类支持以下`DbParameter`*公共*属性：  
  
|Name|Get/Set|Description|  
|----------|--------------|-----------------|  
|**DbType**|获取和设置|参数的数据类型。 请参阅[基本 Siebel 数据类型](../../adapters-and-accelerators/adapter-siebel/basic-siebel-data-types.md)。|  
|**方向**|获取和设置|支持以下值：<br /><br /> -                     `ParameterDirection.Input`<br /><br /> -                     `ParameterDirection.Output`<br /><br /> -                     `ParameterDirection.InputOutput`|  
|**IsNullable**|获取和设置|属性不受支持，并将引发异常，如果调用。|  
|**参数名称**|获取和设置|[!INCLUDE[adoprovidersiebelshort](../../includes/adoprovidersiebelshort-md.md)]支持此属性对于的 ADO.NET 客户端可以指定参数名称。|  
|**值**|获取和设置|[!INCLUDE[adoprovidersiebelshort](../../includes/adoprovidersiebelshort-md.md)]表示作为字符串的参数值。|  
  
###  <a name="BKMK_Datatypes"></a>支持的数据类型  
 下表总结了简单 Siebel 字段类型[!INCLUDE[adoprovidersiebelshort](../../includes/adoprovidersiebelshort-md.md)]支持。 有关更详细说明，请参阅[基本 Siebel 数据类型](../../adapters-and-accelerators/adapter-siebel/basic-siebel-data-types.md)。  
  
|Siebel 字段类型|.NET 类型|XML 架构类型|  
|-----------------------|---------------|---------------------|  
|DTYPE_BOOL|Boolean|xsd:boolean|  
|DTYPE_CURRENCY|Decimal|xsd:decimal|  
|DTYPE_DATE|DateTime|xsd:dateTime|  
|DTYPE_DATETIME|DateTime|xsd:dateTime|  
|DTYPE_ UTCDATETIME|DateTime|xsd:dateTime|  
|DTYPE_ID|字符串|xsd:string|  
|DTYPE_INTEGER|Integer|xsd:int|  
|DTYPE_NOTE|字符串|xsd:string|  
|DTYPE_NUMBER|Decimal|xsd:decimal|  
|DTYPE_PHONE|字符串|xsd:string|  
|DTYPE_TEXT|字符串|xsd:string|  
|DTYPE_TIME|DateTime|xsd:dateTime|  
  
## <a name="supported-methods"></a>支持的方法  
 `SiebelParameter`类不重写中的任何特殊方法`DbParameter`。  
  
## <a name="see-also"></a>另请参阅  
 [扩展 Siebel 适配器 ADO.NET 接口](../../adapters-and-accelerators/adapter-siebel/extend-ado-net-interfaces-with-the-siebel-adapter.md)