---
title: 配置 AS2 管道属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- bts10.edir2.AS2.pipeline.properties
ms.assetid: 7faf6b05-710a-4d00-8c77-590ce9d9f962
caps.latest.revision: 7
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 0d2bb679e4e150382cd8ff3e80c838d269ba908f
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36988870"
---
# <a name="configuring-as2-pipeline-properties"></a>配置 AS2 管道属性
当 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 无法确定解析为已发送交换或已接收交换的协议时，将使用管道属性来处理传入或传出的 AS2 消息。  
  
## <a name="prerequisites"></a>必要條件  
 必须以 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理员组或 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] B2B Operators 组成员的身份登录。  
  
## <a name="as2-pipeline-properties"></a>AS2 管道属性  
 可在 AS2 管道中设置以下属性：  
  
|“属性”|改用|值|管道/阶段|  
|--------------|---------|------------|---------------------|  
|ContentTransferEncoding|指示将采用何种方法以 ASCII 文本格式表示二进制数据。|8bit（默认值）<br /><br /> 7bit<br /><br /> 8bit|AS2EdiSend/编码<br /><br /> AS2Send/编码|  
  
### <a name="to-set-a-pipeline-property"></a>设置管道属性  
  
1. 在 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 管理控制台中，右键单击使用你要设置其属性的管道的接收位置或发送端口。 单击 **“属性”**。  
  
2. 单击你要设置其属性的管道旁的省略号按钮 (…)。  
  
3. 为属性输入值，然后单击**确定**。  
  
## <a name="see-also"></a>请参阅  
 [开发和配置 BizTalk Server AS2 解决方案](../core/developing-and-configuring-biztalk-server-as2-solutions.md)