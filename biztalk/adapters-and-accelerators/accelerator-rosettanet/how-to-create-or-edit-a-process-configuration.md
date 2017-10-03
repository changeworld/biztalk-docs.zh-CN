---
title: "如何创建或编辑过程配置 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- process configuration, modifying
- process configuration, creating
- authorization properties
- non-repudiation, properties
- creating, process configuration
- modifying, process configuration
ms.assetid: ef6160f1-f2f0-42ff-a516-7818c9d79d26
caps.latest.revision: "4"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: e4c9c9be5e9f3361683e495febbd98a05156399d
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="how-to-create-or-edit-a-process-configuration"></a>如何创建或编辑过程配置
本主题讲述如何创建或编辑流程配置。  
  
 流程配置中的设置如下表所示（按选项卡进行排列）。创建和编辑流程配置的过程在下表之后介绍。  
  
 授权属性和不可否认性属性是相互依赖的。 有关如何设置这些属性的详细信息，请参阅[授权和不可否认性属性](../../adapters-and-accelerators/accelerator-rosettanet/authorization-and-non-repudiation-properties.md)。  
  
|选项卡|设置|用法|  
|---------|-------------|-----------|  
|**常规**|**显示的代码**|合作伙伴接口流程 (PIP) 显示代码。 它可对应于 RosettaNet PIP 名称或自定义架构的名称。 建议您使用标准命名约定，如包含流程代码和版本的名称，例如“STD_3A2_R02.00.00A”。 这将简化您维护同一 PIP 的不同版本的工作。<br /><br /> 必填字段。|  
|**常规**|**进程代码**|由三位数字构成的 PIP 代码。 例如“3A2”。<br /><br /> 必填字段。|  
|**常规**|**版本**|PIP 的版本。 例如“V02.02”或“R02.00.00A”。<br /><br /> 必填字段。|  
|**常规**|**进程名称**|PIP 的名称。 例如“价格与可用性请求操作”。<br /><br /> 必填字段。|  
|**常规**|**Description**|有关符合 PIP 的消息的说明。|  
|**常规**|**Standard**|标准的类型。<br /><br /> 可能的值： RosettaNet （默认值） 或 CIDX|  
|**常规**<br /><br /> （非 RosettaNet 内容区域）|**标准的消息**|对于非 RosettaNet 内容，为非 RosettaNet 标准的名称。 如果没有使用 RosettaNet PIP，而定义了一个自定义架构，请使用此设置。 此设置仅适用于 RNIF 2.0，不适用于 RNIF 1.1 或 CIDX。|  
|**常规**<br /><br /> （非 RosettaNet 内容区域）|**标准版本**|对于非 RosettaNet 内容，为非 RosettaNet 标准的版本。 如果没有使用 RosettaNet PIP，而定义了一个自定义架构，请使用此设置。 此设置仅适用于 RNIF 2.0，不适用于 RNIF 1.1 或 CIDX。|  
|**常规**<br /><br /> （非 RosettaNet 内容区域）|**负载绑定 ID**|对于非 RosettaNet 内容，为负载内容的标识号。 如果没有使用 RosettaNet PIP，而定义了一个自定义架构，请使用此设置。 实现自定义 PIP 的一方应定义此值。 此设置仅适用于 RNIF 2.0，不适用于 RNIF 1.1 或 CIDX。|  
|**活动**<br /><br /> （确认收到区域）|**不可否认性所需**|确定是否必须 （使用确认消息中包含的消息摘要） 签名并存储在其原始形式的 MessageStorageIn 或 MessageStorageOut 表中的接收方信号消息[!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)]存档数据库用于不可否认性目的。 接收方必须存储段中指定信号**的原点的不可否认性**合作伙伴配置中的属性。<br /><br /> 可能的值： `True` （默认值） 或`False`<br /><br /> 如果为 `False`，则不会存储信号消息来确保不可否认性。 可以对信号消息进行签名，也可以不进行签名。<br /><br /> 如果为 `True`，则入站信号消息将以原始格式存储在 MessageStorageIn 表中。 出站信号消息将以原始格式存储在 MessageStorageOut 表中。 必须对信号消息进行签名。<br /><br /> 有关详细信息，请参阅[授权和不可否认性属性](../../adapters-and-accelerators/accelerator-rosettanet/authorization-and-non-repudiation-properties.md)。|  
|**活动**<br /><br /> （确认收到区域）|**确认时间 （秒）**|发起方必须接收确认的时间（以秒为单位）。 如果发起方未收到它按此时间，发起方将重试，如果没有超出重试**重试**计数 (在**行为**此选项卡的部分)。<br /><br /> [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)]度量值**时间确认**值从时间成功发送出操作消息的发起程序。 该值包含在传递头中。 值不能小于零或大于**时间执行**同一页设置的值。<br /><br /> 将此设置用于 RNIF 1.1 和 2.01 处理过程中返回的信号消息（应用程序确认）。 还可以将此设置用于 RNIF 1.1 处理过程中返回的接受确认。<br /><br /> 默认值为 7200 秒（两小时）。|  
|**活动**<br /><br /> （行为区域）|**要求授权**|确定任何传入的信号或操作消息是否必须进行签名。 [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)]如果未授权的个人/角色执行活动，将不会接受业务文档。<br /><br /> 可能的值： `True` （默认值） 或`False`<br /><br /> 如果为 `False`，则出站操作和信号消息不经过签名。 可以对入站操作和信号消息进行签名。 如果未对这些消息进行签名，则系统将使用传递头为合作伙伴授权。<br /><br /> 如果为 `True`，则必须对传入消息进行签名。 可以对传出消息进行签名。 仅当对传出消息进行签名**的起点和内容的不可否认性**设置为`True`。<br /><br /> 有关详细信息，请参阅[授权和不可否认性属性](../../adapters-and-accelerators/accelerator-rosettanet/authorization-and-non-repudiation-properties.md)。|  
|**活动**<br /><br /> （行为区域）|**要求永久保密**|确定是否需要加密。<br /><br /> 可能的值：**无**（默认值） 表示无加密是必需。 **负载**指示该服务的内容和附件的加密是必需的。 **负载容器**指示该加密标头是必需的服务内容、 附件和服务。<br /><br /> 在 RNIF 2.0 中，不会对前导头和传递头进行加密。 在 RNIF 1.1 中，不会对任何消息部分进行加密。 只对它们进行签名。|  
|**活动**<br /><br /> （行为区域）|**是所需的安全传输**|确定是否需要 HTTPS 传输。<br /><br /> 可能的值： `True` （默认值） 或`False`|  
|**活动**<br /><br /> （行为区域）|**是单个操作**|确定消息是单一操作还是双操作。<br /><br /> 可能的值： `True` （默认值） 或`False`<br /><br /> 单一操作消息是信息分发或通知。 双操作消息是业务交易、请求确认、请求/响应或查询/响应。<br /><br /> 如果标准是 CIDX，**是否为单一操作**必须**True**。|  
|**活动**<br /><br /> （行为区域）|**是同步**|确定贸易合作伙伴是否同步或异步交换操作消息。<br /><br /> 可能的值：`True`或`False`（默认值）<br /><br /> 不适用于 RNIF 1.1。|  
|**活动**<br /><br /> （行为区域）|**不可否认性的源和内容**|确定操作消息是否必须经过签名并由接收方以原始接收格式将其存储在 BTARNArchive 数据库的 MessageStorageIn 或 MessageStorageOut 表中，以确保不可否认性。 接收方必须存储段中指定的操作的消息**的原点的不可否认性**不可否认性目的的合作伙伴配置中的属性。 如有必要，必须对操作消息进行签名。<br /><br /> 可能的值： `True` （默认值） 或`False`<br /><br /> 如果为 `False`，则不存储操作消息来确保不可否认性。 可以对操作消息进行签名，也可以不进行签名。<br /><br /> 如果为 `True`，则入站操作消息将以原始格式存储在 MessageStorageIn 表中。 出站操作消息将以原始格式存储在 MessageStorageOut 表中。 必须对操作消息进行签名。<br /><br /> 有关详细信息，请参阅[授权和不可否认性属性](../../adapters-and-accelerators/accelerator-rosettanet/authorization-and-non-repudiation-properties.md)。|  
|**活动**<br /><br /> （行为区域）|**重试计数**|一旦传输或处理失败，该流程应重试活动的次数。 如果重试次数为 3，该流程将尝试四次。<br /><br /> 默认值为 3。<br /><br /> 如果通信为同步通信，则 [!INCLUDE[btaBTARN3.3abbrevnonumber](../../includes/btabtarn3-3abbrevnonumber-md.md)] 不使用此字段，因为重试不会在同步交易中应用。|  
|**活动**<br /><br /> （行为区域）|**执行时间**|流程必须完成该活动的时间段（以秒为单位）。 此时间段始于发起方发送第一个文档之时。 发起方（不是响应方）必须确保活动在此时间段内完成。 此值在传递头中。<br /><br /> 默认值为 86400 秒 （24 小时）。<br /><br /> **时间执行**值必须大于**时间确认**中设置的值**回执确认**的同一页上的部分。|  
|**活动**<br /><br /> （常规区域）|**类型**|确定活动的类型。<br /><br /> 可能的值：**业务事务**，**信息分发**（默认值）、**通知**，**查询/响应**， **确认请求/**，或**请求/响应**|  
|**发起程序**<br /><br /> （业务文档区域）|**Description**|有关发起方操作的业务文档的说明。|  
|**发起程序**<br /><br /> （业务文档区域）|**名称**|发起方操作的业务文档的名称。 例如“价格与可用性请求”。|  
|**发起程序**<br /><br /> （业务文档区域）|**版本**|业务文档的版本。 例如，“V02_02_00”或“R02.00.00A”。<br /><br /> 您可以在 RosettaNet XML 消息指南文件（格式为 .htm）的开始部分找到此版本号，此 .htm 文件是随 PIP 规范文件（格式为 .doc）和 PIP DTD 一起从 RosettaNet 组织下载的。|  
|**发起程序**<br /><br /> （常规区域）|**操作**|有关发起方操作的说明。 例如，“同步测试查询操作”。|  
|**发起程序**<br /><br /> （常规区域）|**角色**|发起方的角色。 例如，“买方”或“支付方”。<br /><br /> 默认值为“发起方”。|  
|**发起程序**<br /><br /> （常规区域）|**角色描述**|有关发起方角色的说明。 例如，“付款的一方”。|  
|**发起程序**<br /><br /> （常规区域）|**角色类型**|发起方的角色的类型。<br /><br /> 可能的值：**组织**，**员工**，或**功能**（默认值）|  
|**发起程序**<br /><br /> （常规区域）|**服务**|发起方服务。 例如，“买方服务”或“支付方服务”。|  
|**发起程序**<br /><br /> （常规区域）|**服务分类**|发起方服务的类型。 例如，“业务服务”。|  
|**响应方**<br /><br /> （业务文档区域）|**Description**|有关响应方操作的业务文档的说明。 例如，“正式确认采购订单中的项目条目的状态”。|  
|**响应方**<br /><br /> （业务文档区域）|**名称**|响应方操作的业务文档的名称。 例如，“采购订单确认”。|  
|**响应方**<br /><br /> （业务文档区域）|**版本**|业务文档的版本。 例如，“V02.02.00”或“R02.00.00A”。 您可以在 RosettaNet XML 消息指南文件（格式为 .htm）的开始部分找到此版本号，此 .htm 文件是随 PIP 规范文件（格式为 .doc）和 PIP DTD 一起从 RosettaNet 组织下载的。|  
|**响应方**<br /><br /> （常规区域）|**操作**|有关响应方操作的说明。 例如，“采购订单确认操作”。|  
|**响应方**<br /><br /> （常规区域）|**角色**|响应方的角色。 例如，“卖方”。<br /><br /> 默认值为“响应方”。|  
|**响应方**<br /><br /> （常规区域）|**角色描述**|有关响应方角色的说明。 例如，“收款的一方”。|  
|**响应方**<br /><br /> （常规区域）|**角色类型**|响应方的角色的类型。<br /><br /> 可能的值：**组织**（默认值）、**员工**，或**功能**|  
|**响应方**<br /><br /> （常规区域）|**服务**|响应方服务。 例如，“卖方服务”。|  
|**响应方**<br /><br /> （常规区域）|**服务分类**|响应方服务的类型。 例如，“业务服务”。|  
  
### <a name="to-implement-a-new-process-configuration"></a>实现新流程配置  
  
1.  单击**启动**，指向**所有程序**，指向**Microsoft** [!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]，然后单击[!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]**管理控制台**.  
  
2.  在 BTARN 管理控制台中，展开 [!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]。  
  
3.  右键单击**过程配置设置**，指向**新建**，然后单击**过程配置**。  
  
4.  在新进程配置属性对话框中，在**常规**，**活动**，**发起程序**，和**响应方**选项卡中，键入在前面列出的设置值表，并依次**确定**。  
  
### <a name="to-edit-a-process-configuration"></a>编辑流程配置  
  
1.  单击**启动**，指向**所有程序**，指向**Microsoft** [!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]，然后单击[!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]**管理控制台**.  
  
2.  在 BTARN 管理控制台中，展开 [!INCLUDE[btaBTARNNoVersionui](../../includes/btabtarnnoversionui-md.md)]。  
  
3.  单击**处理配置设置**。  
  
4.  右键单击你想要编辑，然后单击的过程配置**属性**。  
  
5.  在*\<过程配置 >*属性对话框中，在**常规**和**联系人属性**选项卡，更改为所需的设置。 有关这些设置的信息，请参阅上表。  
  
6.  单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [使用 PIP 规范创建过程配置](../../adapters-and-accelerators/accelerator-rosettanet/using-the-pip-specification-to-create-a-process-configuration.md)   
 [授权和不可否认性属性](../../adapters-and-accelerators/accelerator-rosettanet/authorization-and-non-repudiation-properties.md)   
 [设置向上 CIDX eStandards 消息交换](../../adapters-and-accelerators/accelerator-rosettanet/setting-up-cidx-estandards-message-exchange.md)   
 [管理 BTARN 配置](../../adapters-and-accelerators/accelerator-rosettanet/administering-the-btarn-configuration.md)