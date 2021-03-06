---
title: 处理错误的错误 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 602be8a5-1f28-457d-8e12-ba06cff65491
caps.latest.revision: 5
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: c494614465df4faeead9ec30d79dfdf47cc321c1
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36999078"
---
# <a name="error-handling-errors"></a>处理错误时出错
有关诊断和解决 WCF 错误处理错误的信息。  

## <a name="error-handling-options-disable-location-on-failure-and-suspend-request-message-on-failure-should-not-both-be-set-to-false"></a>错误处理选项“失败时禁用位置”和“失败时挂起请求消息”不应同时设置为 False    

|                 |                                                                                                详细信息                                                                                                 |
|-----------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  产品名称   |                                                           [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]                                                           |
| 产品版本 |                                                                       [!INCLUDE[btsWCFVersion](../includes/btswcfversion-md.md)]                                                                       |
|    事件 ID     |                                                                                                   0                                                                                                    |
|  事件源   |                                                                                                   0                                                                                                    |
|    组件    |                                                                                                   0                                                                                                    |
|  符号名称  |                                                                                                   0                                                                                                    |
|  消息正文   | 错误处理选项“失败时禁用位置”和“失败时挂起请求消息”不应都设置为 False，因为可能发生消息丢失。 请将一个或两个选项设置为 True。 |

## <a name="explanation"></a>解释  
 在 Wcf-netmsmq 适配器中，选项**失败时禁用位置**并**在失败时挂起请求消息**不能同时应处于选中状态。 由于接收位置继续接收无效消息，但这些消息未被挂起并存储在 MessageBox 中，则可能发生消息丢失。  

## <a name="user-action"></a>用户操作  
 使用以下过程配置适配器设置。    

1. 打开 **“BizTalk Server 管理”**。  

2. 在控制台根目录中，展开[!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]，展开**BizTalk 组**，然后展开**应用程序**。  

3. 找到你的应用程序，然后找到您的传输。  

4. 右键单击传输名称。  

5. 选择**属性**。  

6. 在端口**类型**列表中，选择正确的端口。  

7. 选择 **“配置”**。  

8. 在中**WCF [**<em>传输类型</em>**] 传输属性**对话框中，选择**消息**选项卡。  

9. 在中**的错误处理**部分中，确保**失败时禁用位置**或**失败时挂起请求消息**检查。
