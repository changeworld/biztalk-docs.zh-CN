---
title: 协议解析和架构确定传出 EDI 消息的 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e37aeb9d-1e95-464d-bb71-73653c1d4674
caps.latest.revision: 24
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: a718f386686b8a23bc8c97108b94b5fba717ee90
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36992022"
---
# <a name="agreement-resolution-and-schema-determination-for-outgoing-edi-messages"></a>传出 EDI 消息的协议解析和架构确定
若要向贸易合作伙伴生成 EDI 消息，EDI 发送管道必须执行下列操作：  
  
-   确定消息解析为的协议  
  
-   确定要用于验证消息的架构  
  
## <a name="agreement-resolution"></a>协议解析  
 EDI 发送管道执行一系列步骤，确定传出交换和协议属性是否匹配，进而查找协议。 一旦 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 确定协议，便可确定适用于交换的文档架构（见下文）。 它使用与匹配协议关联的属性及相关架构来生成并验证传出消息。  
  
 若要执行协议解析，[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 将按照以下方式继续进行操作：  
  
1. 通过将 AgreementPartIDForSend 上下文属性与单向协议的 ID 相匹配来解析协议。 此属性应为整数类型，此属性可以在自定义组件中进行设置，它并不是由 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 设置的。  
  
2. 如果第 1 步不成功，通过与协议属性的所有以下三个上下文属性进行匹配来解析协议： AgreementNameForSend、 SenderPartyNameForSend、 ReceiverPartyNameForSend。 请注意，要成功解析为协议，这三个属性都必须要设置。 这些属性可以在自定义组件中进行设置，它们并不是由 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 设置的。  
  
3. 如果第 2 步不成功，则解析协议通过匹配的参与方名称与 DestinationPartyName 属性设置为中的其他协议解析程序将消息上下文属性中**标识符**选项卡协议属性。  
  
4. 如果第 3 步不成功，则通过将消息上下文中的下列属性与协议属性中的这些属性进行匹配来解析协议：DestinationPartySenderIdentifier、DestinationPartySenderQualifier、DestinationPartyReceiverIdentifier 和 DestinationPartyReceiverQualifier。 请注意，要成功解析为协议，所有这四个属性都必须设置。 这些属性可以设置在自定义组件;它们不通过设置[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]。 有关详细信息，请参阅下面。  
  
   > [!NOTE]
   >  如果上述任何上下文属性集经过升级，且 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 无法找到与这些上下文属性关联的协议，则 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 将挂起此消息。  
   > 
   >  如果用户有意编写一组上下文属性的协议解析和冲突解决程序不能确定 OnewayAgreement，则挂起消息。 失败时要解析为协议根据一组上下文属性，相应的警告消息引发的事件日志中。  
  
5. 如果步骤 4 没成功，或上述上下文属性均未升级，则通过将订阅该消息的发送端口与协议关联的发送端口进行匹配，EDI 消息会解析为一条协议。  
  
   > [!NOTE]
   >  如果同一发送端口与多个协议关联，[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 将生成错误。  
  
6. 如果在步骤 1、2、3 或 4 中找不到协议，则发送管道将使用备用协议设置生成传出消息。  
  
   **通过匹配发送方和接收方上下文属性的协议解析**  
  
   在上面第二个步骤中，在匹配中使用的四个上下文属性是 EDI。DestinationPartySenderIdentifier，EDI。DestinationPartySenderQualifier，EDI。DestinationPartyReceiverIdentifier 和 EDI。DestinationPartyReceiverQualifier。 这些上下文属性的命名空间是 `http://schemas.microsoft.com/Edi/PropertySchema`。 [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] 尝试进行匹配的相关发送方和接收方的标识符和限定符的单向协议属性中使用这些值。 对于 X12，这些字段为 ISA05、 ISA06、 ISA07 和在 ISA08**标识符**页中的单向协议选项卡**协议属性**对话框; 对于 EDIFACT，这些字段为 UNB2.1、 UNB2.2，UNB3.1 和 UNB3.2 中的**标识符**页中的单向协议选项卡**协议属性**对话框。  
  
   若要使用所有四个发送方和接收方的标识符和限定符启用发送端协议解析，必须设置所有四个上下文属性。 以唯一方式执行此操作可标识协议。 使用上述协议查找方法可以更灵活地执行发送端处理。 例如，此方法可以让您以避免在某些情况下，创建多个发送端口并避免复杂的发送端口筛选器。 同时，您还可以根据需要避免设置 OneWayAgreementId 属性。  
  
   如果已将所有四个上下文属性设置为一条消息，并且这些上下文属性和属性属性之间不存在任何匹配，则挂起消息。 仅在尚未设置所有四个上下文属性时，才会使用与协议关联的发送端口解析该协议。  
  
> [!NOTE]
>  EDI 管道中的消息将转到协议解析中的后续步骤，直到该消息在协议处于启用状态的情况下通过相应步骤得到解析。 例如，如果消息在协议解析的第一步中得到解析，但协议处于禁用状态，则消息将转到后续步骤进行解析。  
  
## <a name="schema-determination"></a>架构确定  
 EDI 发送管道可确定适用于消息的架构名称和每个事务集 （作为文档类型信息或在根节点） 的中间 XML 文件中包含的架构命名空间中的架构。  
  
 对于交换，已被预留，发送管道使用中间 XML 文件的完整交换的设置在单个事务中的文档类型信息。 它使用控制段架构进行处理的信封段。  
  
## <a name="see-also"></a>请参阅  
 [BizTalk Server 如何发送 EDI 消息](../core/how-biztalk-server-sends-edi-messages.md)