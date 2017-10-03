---
title: "TIBCO 企业消息服务要求和限制 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- encryption
- messages, compression
- EMS limitations
- message compression
- API, adding to GAC
- global assembly cache, adding API
- GAC, adding TIBCO EMS API
- system requirements
- TIBCO.EMS.dll
- EMS requirements
- messages, encryption
ms.assetid: 6e4c022c-e6a8-4ac5-b998-b0465002a31e
caps.latest.revision: "10"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 81e49f4a74cce4414fd9d0b069a382d9facb03d0
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="tibco-enterprise-message-service-requirements-and-limitations"></a>TIBCO Enterprise Message Service 要求和限制
## <a name="system-requirements"></a>系统要求  
 用于 TIBCO Enterprise Message Service 的 Microsoft BizTalk 适配器支持 TIBCO Enterprise Message Service (EMS) 版本 4.2。 TIBCO EMS 版本 4.2 随附有客户端 SDK（使用 TIBCO EMS C# API）。 用于 TIBCO EMS 的 BizTalk 适配器使用此 API 与 TIBCO EMS 通信。  
  
## <a name="adding-the-api-to-the-gac"></a>将 API 添加到 GAC  
 用于 TIBCO EMS 的 BizTalk 适配器要求将 TIBCO EMS C# API TIBCO.EMS.dll 添加到全局程序集缓存 (GAC) 中。 如果未安装此程序集，则适配器会触发异常并记录相应的消息。  
  
#### <a name="to-add-the-tibco-ems-c-api-to-the-gac"></a>将 TIBCO EMS C# API 添加到 GAC  
  
1.  将复制到 TIBCO EMS C #API 你[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]计算机。  
  
2.  将目录更改为 C# API 文件，TIBCO 的位置。EMS。DLL。  
  
     在默认安装中，此 DLL 的路径是 c:\tibco\ems\clients\cs\TIBCO。EMS。DLL。  
  
3.  在命令提示符下键入：  
  
     `C:\bin> gacutil /i TIBCO.EMS.dll`  
  
     TIBCO。EMS.dll 现在显示 gac。  
  
     若要查看 GAC 列表中，在控制面板中，打开**管理工具**，打开**Microsoft.NET Framework X.XConfiguration**，然后单击**程序集缓存**。  
  
## <a name="limitations"></a>限制  
 BizTalk 适配器 TIBCO 企业消息服务使用 TIBCO。EMS.dll 与 TIBCO 企业消息服务进行通信。 当你使用 TIBCO EMS C# API 时，应考虑以下限制：  
  
-   使 TIBCO EMS 客户端将消息以压缩形式发送到 EMS 的消息压缩时无法使用 C# API。  
  
-   加密的适配器和服务器之间的消息时无法使用 C# API。 C# API 不允许使用 OpenSSL 库的 SSL 加密。  
  
-   C# API 不支持进行 ems 相关的管理 API。  
  
-   无法发送或接收使用 BizTalk TIBCO EMS 适配器大于 50 MB 的大小的消息。 超出此大小，环境遇到 System.OutOfMemoryException 异常。  
  
## <a name="see-also"></a>另请参阅  
 [规划和体系结构](../core/planning-and-architecture16.md)