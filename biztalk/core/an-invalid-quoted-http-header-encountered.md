---
title: 无效的引用时遇到的 HTTP 标头 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bb530ee6-ec6a-4791-ae99-b9db426c0896
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 7ca0d7463f4604e8a159c12fab690e494a13fb60
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36971006"
---
# <a name="an-invalid-quoted-http-header-encountered"></a>遇到无效的引用 HTTP 标头
## <a name="details"></a>详细信息  
  
|                 |                                                                                                              |
|-----------------|--------------------------------------------------------------------------------------------------------------|
|  产品名称   |              [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]              |
| 产品版本 |                          [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]                          |
|    事件 ID     |                                                      -                                                       |
|  事件源   |            [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI            |
|    组件    |                                                  AS2 引擎                                                  |
|  符号名称  |                                                      -                                                       |
|  消息正文   | 遇到无效的引用 HTTP 标头。  详细信息如下： 标头名称:"{0}"标头值:"{1}" |
  
## <a name="explanation"></a>解释  
 此错误/警告/信息事件表明 AS2 接收管道或 AS2 发送管道无法处理 AS2 消息，因为消息中 AS2-From 或 AS2-To HTTP 标头的名称未用引号正确括起来。 用引号将标头名称括起来以便在名称中包含空格、反斜杠或双引号。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请按照 RFC 4130“MIME-Based Secure Peer-to-Peer Business Data Interchange Using HTTP, Applicability Statement 2 (AS2)（针对使用 HTTP 进行基于 MIME 的安全对等业务数据交换的 Applicability Statement 2 (AS2)）”中第 6.2 节“AS2 系统标识符”中所述的规则用引号将 AS2 消息中的标头名称括起来。