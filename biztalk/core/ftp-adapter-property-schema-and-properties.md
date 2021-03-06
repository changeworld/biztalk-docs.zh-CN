---
title: FTP 适配器属性架构和属性 |Microsoft 文档
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- configuring [FTP adapters], schemas
- FTP adapters, properties
- BeforePut property [FTP adapters]
- PassiveMode property [FTP adapters]
- configuring [FTP adapters], properties
- UserName property, FTP adapters
- SSOAffiliateApplication property [FTP adapters]
- AfterPut property [FTP adapters]
- ReceivedFileName property [FTP adapters]
- RepresentationType property [FTP adapters]
- SpoolingFolder property [FTP adapters]
- FTP adapters, schemas
- CommandLogFileName property [FTP adapters]
- AllocateStorage property [FTP adapters]
- schemas, FTP adapters
- Password property [FTP adapters]
- MaxConnections property [FTP adapters]
ms.assetid: 677fdb61-c2b0-4df2-a826-840113e61e8b
caps.latest.revision: 19
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 1cf72847fccd84a1435e436a4bf2b59d36e26179
ms.sourcegitcommit: 3fc338e52d5dbca2c3ea1685a2faafc7582fe23a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
ms.locfileid: "26006134"
---
# <a name="ftp-adapter-property-schema-and-properties"></a>FTP 适配器属性架构和属性
下表包含 FTP 适配器属性架构中的属性。  
  
 **Namespace:** http://schemas.microsoft.com/BizTalk/2003/ftp-properties  
  
|Name|类型|Description|  
|----------|----------|-----------------|  
|**RepresentationType**|xs:string|指定 FTP 适配器发送数据的方式。<br /><br /> **有效值：** 二进制或 ASCII|  
|**SSOAffiliateApplication**|xs:string|指定要在 FTP 发送端口上使用的企业单一登录关联应用程序。|  
|**UserName**|xs:string|指定发送消息时登录 FTP 服务器所用的用户名。|  
|**密码**|xs:string|指定发送消息时登录 FTP 服务器所用的密码。|  
|**BeforePut**|xs:string|指定要在文件 PUT，例如用于更改 FTP 服务器上的默认值的命令之前运行的 FTP 命令。 用分号 (;) 分隔命令。 不需要 open 命令。|  
|**AfterPut**|xs:string|指定要在文件 PUT 后运行的 FTP 命令。 用分号 (;) 分隔命令。|  
|**ReceivedFileName**|xs:string|指定 FTP 适配器从中读取消息的文件的全名。|  
|**MaxConnections**|xs:unsignedInt|指定服务器允许并行打开的最大 FTP 连接数。 0 表示无限制。|  
|**CommandLogFileName**|xs:string|指定日志文件副本的保存位置，在通过 FTP 发送或接收文件时，可以使用该副本来诊断错误情况。|  
|**AllocateStorage**|xs:boolean|此选项在 BizTalk Server 中已弃用并建议不要使用此属性。|  
|**PassiveMode**|xs:boolean|指定适配器用来连接 FTP 服务器的模式。<br /><br /> 在主动模式中，FTP 服务器连接到由 FTP 适配器打开的端口。 在被动模式中，FTP 适配器连接到由 FTP 服务器打开的端口。<br /><br /> 如果**PassiveMode**为 false，则适配器用来连接到 FTP 服务器使用主动模式。 此属性的默认值为 False。|  
|**SpoolingFolder**|xs:string|指定 FTP 服务器上临时文件夹的位置。 此位置用于确保在传输失败后可以进行恢复。|  
|**UseSsl**|xs:boolean|指定 FTP 适配器是否必须使用 SSL 与 FTPS 服务器进行通信。|  
|**UseDataProtection**|xs:boolean|指定是否对文件传输进行 SSL 加密。 如果适配器发送和接收来自 FTPS 服务器的数据文件时必须使用 SSL 加密，请选择 true。 对于要以纯文本形式发送和接收数据文件的适配器，请选择 false。|  
|**FtpsConnectionMode**|xs:string|指定用于 FTPS 服务器的 SSL 连接模式。<br /><br /> **有效值：** 隐式或显式|  
|**ClientCertificateHash**|xs:string|指定必须在安全套接字层 (SSL) 协商中使用的客户端证书的 SHA1 哈希。<br /><br /> 基于此哈希，从运行 BizTalk 主机实例的用户帐户的个人存储中提取客户端证书。|  
  
## <a name="see-also"></a>另请参阅  
 [配置 FTP 适配器](../core/configuring-the-ftp-adapter.md)
 
 [有关 FTP 适配器的最佳做法和建议](../core/best-practices-and-recommendations-for-the-ftp-adapter.md)
 
 [FTP 适配器](../core/ftp-adapter.md)