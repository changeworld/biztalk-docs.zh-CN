---
title: 将错误发送 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3cf61c82-ad48-4555-af53-fb841fd0f503
caps.latest.revision: 5
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 76aa238227877ab70328e585d5d12b8c428e9061
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36983319"
---
# <a name="send-errors"></a>发送错误
诊断和解决 WCF 发送错误的信息。  
  
## <a name="failed-to-generate-odx-file"></a>生成 ODX 文件失败

|                 |                                   错误详细信息                                    |
|-----------------|------------------------------------------------------------------------------------|
|  产品名称   | [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] |
| 产品版本 |             [!INCLUDE[btsWCFVersion](../includes/btswcfversion-md.md)]             |
|    事件 ID     |                                         0                                          |
|  事件源   |                                         0                                          |
|    组件    |                                         0                                          |
|  符号名称  |                                         0                                          |
|  消息正文   |                            生成 ODX 文件失败                             |
  
### <a name="explanation"></a>解释  
 此错误表示在使用该服务时出错。  
  
### <a name="user-action"></a>用户操作  
 （如果你拥有的 WCF 服务） 托管的服务具有有效的 Web 方法和该元数据的检查。 否则，请与服务提供商联系。  
  
 使用 WCF 服务的其他信息，请参阅[注意事项时使用 WCF 服务与 WCF 发送适配器](../core/considerations-when-consuming-wcf-services-with-the-wcf-send-adapters.md)。
 
## <a name="response-message-body-was-not-read"></a>无法读取响应消息正文
  
|                 |                                        错误详细信息                                        |
|-----------------|---------------------------------------------------------------------------------------------|
|  产品名称   |     [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]      |
| 产品版本 |                 [!INCLUDE[btsWCFVersion](../includes/btswcfversion-md.md)]                  |
|    事件 ID     |                                              0                                              |
|  事件源   |                                              0                                              |
|    组件    |                                              0                                              |
|  符号名称  |                                              0                                              |
|  消息正文   | 未读取响应消息正文（这可能表示连接已关闭）。 |
  
### <a name="explanation"></a>解释  
 发回响应消息之前，客户端可能已断开连接。  
  
### <a name="user-action"></a>用户操作  
 检查客户端连接。 所采取的步骤和操作的范围取决于端口类型。   
有关详细信息，请参阅[工具和实用程序用于故障排除](../core/tools-and-utilities-to-use-for-troubleshooting.md)。