---
title: 使用 IPv6 寻址的 BizTalk 适配器 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 93cd2ead-5e87-47ac-8f78-d56b80afd34e
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 73047c13c5ea328dd71807a3ba7eea79ddee87ce
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37003686"
---
# <a name="using-ipv6-addressing-with-biztalk-adapters"></a>对 BizTalk 适配器使用 IPv6 寻址
BizTalk Server 适配器支持使用 IPv6 寻址。 本主题介绍了指定 UNC 路径的 IPv6 地址时应当使用的命名法、指定文本 IPv6 地址时使用的命名法，以及如何对 HTTP 和 SOAP 适配器使用 IPv6 范围标识符。  
  
## <a name="ipv6-address-nomenclature-used-for-a-unc-path"></a>用于 UNC 路径的 IPv6 地址命名法  
 如果在 UNC 路径中指定一个文本 IPv6 地址，请按照以下步骤进行操作：  
  
1. 使用短划线“-”字符替换任何冒号“:”字符。  
  
2. 将文本追加"**ipv6-literal.net**"的 IP 地址。  
  
   例如，如果计算机的 IPv6 地址为 2001:DB8:2a:1005:230:48ff:fe73:989d，则指向该计算机上文件共享路径的 URI 的命名法为：  
  
```  
\\2001-DB8-2a-1005-230-48ff-fe73-989d.ipv6-literal.net\<sharename\>  
```  
  
 其中\< *sharename* \>是目标计算机上的文件共享的名称。  
  
> [!NOTE]
>  确保用于运行文件发送和接收处理程序的主机实例的用户帐户具有对该文件共享的相应权限。 与文件适配器接收文件所需的文件夹权限的详细信息请参阅[配置文件接收处理程序](../core/configure-the-file-adapter.md)。 发送与文件适配器的文件时所需的文件夹权限的详细信息请参阅[与文件适配器的已知问题](../core/known-issues-with-the-file-adapter.md)。 有关支持与文件适配器一起使用的文件系统的信息，请参阅[ http://support.microsoft.com/kb/815070 ](http://support.microsoft.com/kb/815070)。  
  
## <a name="using-ipv6-scope-identifiers-with-the-http-adapter-and-the-soap-send-adapter"></a>对 HTTP 适配器和 SOAP 发送适配器使用 IPv6 范围标识符  
 HTTP 发送和接收适配器和 SOAP 发送适配器要求，如果 IPv6 地址中使用的范围标识符，则该范围标识符必须使用转义码转义 **%25**。 例如， **fe80::550c:489f:e65e:aef3%8**是有效的 IPv6 地址包含范围标识符 (%8)。 若要将此 IPv6 地址用于 HTTP 发送和接收适配器或 SOAP 发送适配器，必须对该范围标识符进行转义，如下所示：  
  
```  
fe80::550c:489f:e65e:aef3%258  
```  
  
## <a name="adapter-uri-nomenclature-used-for-a-literal-ipv6-address"></a>用于文本 IPv6 地址的适配器 URI 命名法  
  
-   若要将文本 IPv6 地址用于适配器 URI，请将 IP 地址两边括上方括号“[”、“]”。 例如，具有 IPv6 地址 2001:DB8:2a:1005:230:48ff:fe73:989d 的 URI 的命名法应为：  
  
    ```  
    [2001:DB8:2a:1005:230:48ff:fe73:989d]  
    ```  
  
    > [!NOTE]
    >  将文本 IPv6 地址用于适配器 Uri 应遵循中确立的准则[RFC2732](http://go.microsoft.com/fwlink/?LinkId=90375)。  
  
-   如果指定文本 IPv6 地址作为用于 POP3 接收适配器、SMTP 发送适配器或 SQL 发送和接收适配器的服务器名，则 IPv6 地址不应用方括号括起来。  
  
## <a name="summary-of-considerations-when-using-literal-ipv6-addressing-with-biztalk-adapters"></a>对 BizTalk 适配器使用文本 IPv6 寻址时的注意事项摘要  
 下表简要列出了何时使用文本 IPv6 地址需要将 IP 地址用方括号“[”、“]”括起来，以及何时需要对用在 IPv6 地址中的范围标识符进行转义：  
  
|适配器|是否需要将文本 IPv6 地址用方括号括起来？|是否需要对范围标识符进行转义？|  
|---|---|---|  
|POP3 接收|“否”|“否”|  
|SMTP 发送|“否”|“否”|  
|SQL 发送和接收|“否”|“否”|  
|文件发送和接收|否 (请参阅部分**IPv6 地址命名法用于 UNC 路径**)|“否”|  
|HTTP 发送和接收|是|是|  
|MQSeries 发送和接收|是|“否”|  
|MSMQ 发送和接收|是|“否”|  
|SOAP 发送|是|是|  
|SOAP 接收|是|“否”|  
|WCF 发送和接收|是|“否”|