---
title: X12 EDI 字符集 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 76e7b327-b0bd-4f16-8bfe-6c0184059f2b
caps.latest.revision: 2
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9bd501c81b92f4fa7824009a949fd6c7e58eaf3b
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "37023099"
---
# <a name="x12-edi-character-set"></a>X12 EDI 字符集
使用 Ñ 字符或重读符号 （'） 时，指定以下项：  


|                                                                   |                                  字符集                                   |
|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
|             仅 Ñ EDI 文档中的字符              |                            使用扩展字符集                            |
|           抑音符 (\`) EDI 文档中            |                              使用 UTF8 字符集                              |
| Ñ 字符**并**抑音符 (\`) 在同一文档中： | -入站的文档必须具有 UTF8 编码<br />-使用 UTF8 字符集 |

 以下链接提供了有关 EDI 字符集的详细信息：  

 [EDI 字符集](http://go.microsoft.com/fwlink/p/?LinkId=271249)  

 [EDI 字符集支持](http://go.microsoft.com/fwlink/p/?LinkId=271250)