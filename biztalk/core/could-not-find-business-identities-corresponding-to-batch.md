---
title: 找不到与批相对应的业务标识 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1c9baf11-e9c6-482d-a47d-aa99852939bf
caps.latest.revision: 3
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 3a5076bc5c4887e1819ab64a32bb987fb9b06248
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36975822"
---
# <a name="could-not-find-business-identities-corresponding-to-batch"></a>找不到与批相对应的业务标识
## <a name="details"></a>详细信息  
  
|                 |                                                                                        |
|-----------------|----------------------------------------------------------------------------------------|
|  产品名称   |   [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]   |
| 产品版本 |               [!INCLUDE[btsEDIVersion](../includes/btsediversion-md.md)]               |
|    事件 ID     |                                           -                                            |
|  事件源   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] EDI |
|    组件    |                                       EDI 引擎                                       |
|  符号名称  |                               IdentitiesNotFoundForBatch                               |
|  消息正文   |             找不到与批相对应的业务标识{0}。             |
  
## <a name="explanation"></a>解释  
 此错误/警告/信息事件表明 BizTalk Server 由于数据不足而无法处理某个批处理消息。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请确保具有给定 Id 的批处理所包含协议的协议属性中存在，并且为协议指定了正确的业务标识。