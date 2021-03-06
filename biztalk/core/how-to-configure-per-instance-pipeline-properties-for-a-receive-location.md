---
title: 如何配置每个实例的管道属性接收位置 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- pipelines, properties
- receive locations, configuring
- managing [pipelines], properties
- managing [pipelines], receive locations
- managing [receive locations], pipelines
- managing [pipelines], configuring
- pipelines, receive locations
- pipelines, configuring
- receive locations, pipelines
- managing [receive locations], configuring
ms.assetid: e1ed3b10-2f39-479b-a3e6-22b4b2872192
caps.latest.revision: 13
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 27c591e7ea30dd97b116f89c3d50d03ea48392b4
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36982414"
---
# <a name="how-to-configure-per-instance-pipeline-properties-for-a-receive-location"></a>如何配置每个实例的管道属性接收位置
本主题介绍在将管道部署到 BizTalk 组之后如何使用 BizTalk Server 管理控制台为接收位置配置管道属性。 您所做的更改将只覆盖此接收位置的默认管道属性，因此如果需要，可以为 BizTalk 组中的每个接收位置配置不同的管道属性。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行本主题中的过程，必须是 BizTalk Server Administrators 组的成员的帐户登录。 有关详细的权限的信息，请参阅[用于部署和管理 BizTalk 应用程序所需权限](../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)。  
  
> [!NOTE]
>  使用每个实例的管道属性设置的值时**DocumentSpecNames** XML 拆装器组件的管道、 指定的文档架构和管道中的属性必须在同一项目中定义。  
  
### <a name="to-configure-per-instance-pipeline-properties-for-a-receive-location"></a>为接收位置配置基于实例的管道属性  
  
1. 单击**启动**，单击**所有程序**，单击[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]，然后单击**BizTalk Server 管理**。  
  
2. 在控制台树中，展开**BizTalk Server 管理**，展开包含要为其配置管道属性中，展开该接收位置的 BizTalk 组**应用程序**，，然后展开包含接收位置的应用程序。  
  
3. 单击**接收位置**文件夹中，右键单击该接收位置，然后依次**属性**。  
  
4. 单击右侧的省略号 （...）**接收管道**框。  
  
5. 配置属性，然后单击**确定**。 有关详细信息，请单击**帮助**属性页上。  
  
   > [!IMPORTANT]
   >  请确保输入正确的管道属性的信息。 如果输入无效值，例如一个字符串，而不是数字，它将生成一个错误。  
  
6. 如果这是一个请求-响应接收位置，单击右侧的省略号 （...）**发送管道**框。  
  
7. 配置属性，然后单击**确定**两次。 有关详细信息，请单击**帮助**属性页上。  
  
## <a name="see-also"></a>请参阅  
 [管理管道](../core/managing-pipelines.md)   
 [创建和配置发送端口](../core/creating-and-configuring-send-ports.md)   
 [管理接收位置](../core/managing-receive-locations.md)