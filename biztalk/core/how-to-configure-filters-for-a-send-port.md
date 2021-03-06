---
title: 如何为发送端口配置筛选器 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- filters, configuring
- filters, send ports
- configuring, filters
- managing [send ports], configuring
- send ports, configuring
- send ports, filters
- managing [send ports], filters
ms.assetid: ad13ca8e-bb1d-4449-8163-49dd9d5d92f8
caps.latest.revision: 15
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: ae9c522f982ca82bf865bcfe6c4b481b0133ec7f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36988174"
---
# <a name="how-to-configure-filters-for-a-send-port"></a>如何为发送端口配置筛选器
本主题将介绍如何使用 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理控制台为发送端口配置筛选器。 您可以使用筛选器来创建简单消息传送或基于内容的路由 (CBR) 应用程序。 筛选器可以设置消息属性或字段的条件，这些条件决定哪些消息将被路由到发送端口。 筛选器不筛选由业务流程路由到发送端口的消息。  
  
 您可以创建一个或多个筛选器表达式，表达式包含消息属性、运算符以及使用此运算符根据该属性进行验证的值。  
  
 例如，您可以创建如下所示的表达式：  
  
 MSMQ.MsgID = 1  
  
 使用此筛选器，发送端口组将只订阅 MSMQ 消息 ID 为 1 的消息。  
  
 您可以创建其他表达式，并指定该表达式与其他表达式有 AND 或 OR 关系，例如：  
  
 MSMQ.MsgID = 1 OR  
  
 SMTP.From = MyServer  
  
 在这种情况下，发送端口组将订阅 MSMQ 消息 ID 为 1 或发自名为 MyServer 的 SMTP 服务器的所有消息。  
  
> [!NOTE]
>  如果您在一个应用程序中为发送端口创建了筛选器，此应用程序使用另一个应用程序中的属性架构，然后将第一个应用程序导入到新 BizTalk 组中，则您将收到缺少架构的警告，并且在安装和启动该应用程序时筛选功能将无法正常运行。 解决这个问题的方法是：先导入包含该架构的应用程序，然后再安装不包含该架构的应用程序。  
  
> [!NOTE]
>  应用程序开发人员可以通过使用本主题中的过程在开发过程中配置为发送端口的筛选器。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行本主题中的步骤，你必须以 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Administrators 组成员的帐户身份登录。 有关详细的权限的信息，请参阅[用于部署和管理 BizTalk 应用程序所需权限](../core/permissions-required-for-deploying-and-managing-a-biztalk-application.md)。  
  
### <a name="to-configure-filters-for-a-send-port"></a>为发送端口配置筛选器  
  
1. 单击**启动**，单击**所有程序**，单击[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]，然后单击**BizTalk Server 管理**。  
  
2. 在控制台树中，展开要为其配置发送端口筛选器的 BizTalk 组和 BizTalk 应用程序。  
  
3. 展开**发送端口**，右键单击发送端口，单击**属性**，然后单击**筛选器**。  
  
4. 下表中所述配置筛选器，然后单击**确定**。  
  
   |使用此选项|执行的操作|  
   |--------------|----------------|  
   |**删除**|单击此项可删除所选的筛选器表达式。|  
   |**上移**|单击此项可在筛选器表达式序列中向上移动所选的属性。|  
   |**“下移”**|单击此项可在筛选器表达式序列中向下移动所选的属性。|  
   |**属性**|在列表中，单击要在此筛选器表达式中使用的消息属性。|  
   |**“运算符”**|为表达式键入或选择运算符。|  
   |**ReplTest1**|键入要根据该属性验证的值。 不同属性类型可接受的值类型不同。 若要查看某个属性可接受哪些类型的值，请将鼠标悬停在该属性上。 下面是可接受的值：Int：(Integer) ，它必须是整数。 字符串： 一个字符串。 dateTime： 日期和/或时间。NET 支持的格式。 有关 .NET 支持的时间格式的详细信息，请参阅 .NET Frameworks 帮助中的“DateTimeFormatInfo 类”。|  
   |**分组依据**|选择**并**或**或**以指示这与其他筛选器表达式之间的关系。|  
  
## <a name="see-also"></a>请参阅  
 [创建和配置发送端口](../core/creating-and-configuring-send-ports.md)