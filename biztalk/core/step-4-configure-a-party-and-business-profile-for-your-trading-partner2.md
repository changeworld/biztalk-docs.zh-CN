---
title: 步骤 4： 配置参与方和业务配置文件贸易 Partner2 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ce07a1a6-4d5d-44ea-b1cb-04d7ae85747f
caps.latest.revision: 3
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 1d0ecc92a435455d15db31e2de454ff935c1504f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36977926"
---
# <a name="step-4-configure-a-party-and-business-profile-for-your-trading-partner"></a>步骤 4： 为贸易合作伙伴配置参与方和业务配置文件
![步骤 4 11](../core/media/tut-step4-of-11.gif "Tut_Step4_of_11")  
  
 在此步骤中，您将为您的贸易合作伙伴 Fabrikam 配置参与方和业务配置文件，以便向组织发送 864 消息，并接收返回的 997 确认消息和异步 MDN。  
  
## <a name="prerequisites"></a>必要條件  
 你必须以 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理员组成员的身份登录。  
  
### <a name="to-configure-a-party-and-business-profile-for-your-trading-partner"></a>为你的贸易合作伙伴配置参与方和业务配置文件  
  
1. 打开[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]通过单击管理控制台**启动**，依次指向**所有程序**，指向[!INCLUDE[btsBizTalkServerStartMenuItemui](../includes/btsbiztalkserverstartmenuitemui-md.md)]，然后单击**BizTalk Server 管理**.  
  
2. 在中[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]管理控制台中，展开[!INCLUDE[btsBizTalkServerAdminConsoleui](../includes/btsbiztalkserveradminconsoleui-md.md)]，然后展开**BizTalk 组**。 右键单击**参与方**，依次指向**新建**，然后单击**参与方**。  
  
3. 在中**参与方属性**对话框框中，输入**Fabrikam**中**名称**字段。  
  
4. 清除**本地 BizTalk 处理参与方或支持来自此参与方发送消息的接收的消息**复选框。 通过清除复选框指定的参与方 (在这种情况下， **Fabrikam**) 不托管 BizTalk Server。  
  
5. 单击“确定” 。  
  
6. 右键单击参与方名称，指向**新建**，然后单击**业务配置文件**。  
  
7. 在中**配置文件属性**对话框中，在**常规**页上，输入`Fabrikam_Profile`中**名称**文本框。  
  
   > [!NOTE]
   >  创建一个参与方时，还创建配置文件。 可以重命名，并使用该配置文件而不是创建一个新。 若要重命名配置文件，请右键单击该配置文件，然后选择**属性**。 在中**常规**页上，指定配置文件的名称。  
  
8. 单击“确定” 。  
  
## <a name="next-steps"></a>后续步骤  
 配置 BTS ISAPI 筛选器和 Fabrikam 和 Contoso Web 页[步骤 5： 配置贸易合作伙伴网页](../core/step-5-configure-the-trading-partner-web-pages.md)。  
  
## <a name="see-also"></a>请参阅  
 [配置 EDI 属性](../core/configuring-edi-properties.md)