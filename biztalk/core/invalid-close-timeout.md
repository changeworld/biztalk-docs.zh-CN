---
title: 关闭超时无效 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b4510329-9fd9-428f-91a3-d72723e9a5e4
caps.latest.revision: 9
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a73c7a6a21b57b8e8fbdff75d2c54d00e90b0a55
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36969470"
---
# <a name="invalid-close-timeout"></a>关闭超时无效
## <a name="details"></a>详细信息  

|                 |                                                                                          |
|-----------------|------------------------------------------------------------------------------------------|
|  产品名称   |    [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]    |
| 产品版本 |                [!INCLUDE[btsWCFVersion](../includes/btswcfversion-md.md)]                |
|    事件 ID     |                                            0                                             |
|  事件源   |                                            0                                             |
|    组件    |                                            0                                             |
|  符号名称  |                                            0                                             |
|  消息正文   | 关闭超时值无效。 有效范围： 0 至 23 小时，0-59 分钟和 0 到 59 秒。 |

## <a name="explanation"></a>解释  

## <a name="user-action"></a>用户操作  
 使用以下过程配置超时范围。  

#### <a name="to-configure-the-timeout-range"></a>配置超时范围的步骤  

1. 单击**启动**，单击**所有程序**，单击[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]，然后单击**BizTalk Server 管理**。  

2. 在控制台根目录中，展开[!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]，展开**BizTalk 组**，然后展开**应用程序**。  

3. 找到你的应用程序，然后找到您的传输。  

4. 右键单击传输名称。  

5. 单击 **“属性”**。  

6. 在端口**类型**列表中，选择正确的端口。  

7. 单击**配置**。  

8. 在中**WCF [**<em>传输类型</em>**] 属性**对话框中，单击**绑定**选项卡。  

9. 确保超时值范围有效。 可接受的值包括：0 到 23 小时、0 到 59 分钟和 0 到 59 秒。
