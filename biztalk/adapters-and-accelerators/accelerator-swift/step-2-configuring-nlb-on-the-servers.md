---
title: "步骤 2： 在服务器上配置 NLB |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Network Load Balancing
- configuring, NLB
- NLB
ms.assetid: 30b2f645-b495-49a5-852b-cf89d25fd2b7
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: f10a05f23012990a1a0cc3dd50e0ca3db4282c84
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="step-2-configuring-nlb-on-the-servers"></a>步骤 2： 在服务器上配置 NLB
安装的基础平台并使用正确的网络设置配置服务器后 (请参阅[步骤 1： 安装基础平台](../../adapters-and-accelerators/accelerator-swift/step-1-installing-the-base-platform.md))，你可能需要启用 BizTalk HTTP 前端服务器和 BizTalk 上的负载平衡消息服务器。 仅当你有一个或多个 BizTalk HTTP 前端服务器从一个或多个 BizTalk 消息传送服务器的单独计算机上安装，则需要此步骤。  
  
 负载平衡可确保客户端计算机 （Internet Explorer 用户浏览到 MRSR 站点） 和 MRSR 服务器之间以及 MRSR 服务器和邮件服务器之间的高可用性通信。  
  
 上的负载平衡**公共**启用 Intranet 用户连接到这些计算机上的 IIS Web 服务器所需的 HTTP 前端服务器的接口。 上的负载平衡**私有**启用联系在这些计算机上的 web 服务的消息传送服务器所需的 HTTP 前端服务器的接口。  
  
 在消息传递的服务器中，假设有两台服务器配置上的负载平衡**私有**网络适配器。  
  
 有关详细信息，请参阅[!INCLUDE[btsBizTalkServer2006r3](../../includes/btsbiztalkserver2006r3-md.md)]部署指南。