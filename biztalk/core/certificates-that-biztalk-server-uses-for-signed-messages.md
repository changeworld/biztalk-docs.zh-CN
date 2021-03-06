---
title: BizTalk Server 使用的证书签名消息 |Microsoft Docs
ms.custom: ''
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- messages, signed messages
- messages, message flow [digital signatures]
- S/MIME messages
- signed messages
- digital signatures, message flow
- messages, certificates
ms.assetid: 0b521e11-73ef-424f-9e6a-4fb42dc263ff
caps.latest.revision: 13
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 1cc45411d19bc23a2985dbd60fc68bc8de58594c
ms.sourcegitcommit: 266308ec5c6a9d8d80ff298ee6051b4843c5d626
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/27/2018
ms.locfileid: "36979846"
---
# <a name="certificates-that-biztalk-server-uses-for-signed-messages"></a>BizTalk Server 用于签名消息的证书
BizTalk Server 支持对出站消息进行签名以及对安全多用途 Internet 邮件扩展 (S/MIME) 入站消息进行签名验证。 BizTalk Server 使用 S/MIME 版本 2 和 3 对出站消息进行签名并验证入站消息的签名。 同样，您可以将 BizTalk Server 配置为对其发送到合作伙伴的消息进行签名和加密。  
  
- BizTalk Server 支持使用 SHA-1 和 MD5 签名算法验证数字签名。 BizTalk Server 使用 SHA-1 签名算法对出站消息进行签名。  
  
- BizTalk Server 支持的用于签名密钥的密钥交换系统是 RSA (Rivest-Shamir-Adleman) 算法和数字签名标准 (Digital Signature Standard, DSS)。 BizTalk Server 不支持将高级加密标准 (Advanced Encryption Standard, AES) 交换系统用于签名密钥。  
  
- BizTalk Server 支持的签名证书是 x.509 版本 3。  
  
  下图显示了 BizTalk Server 接收数字签名消息并选择使用签名将合作伙伴标识解析为 BizTalk Server 环境中某个参与方时的消息流。  
  
  ![发送签名的消息时消息流](../core/media/6fd1674d-5a21-4272-83ca-608d7b400de7.gif "6fd1674d-5a21-4272-83ca-608d7b400de7")  
  
  BizTalk Server 接收数字签名消息时的消息流如下所示：  
  
1. 合作伙伴向 BizTalk Server 发送消息。 合作伙伴使用其私钥证书对该消息进行签名。  
  
2. 相应的 BizTalk Server 接收处理程序接收该消息。  
  
3. 在接收管道的执行过程中，MIME/SMIME 解码器管道组件使用合作伙伴的公钥来验证数字签名。  
  
4. 如果配置了参与方解析组件，则在接收管道参与方解析组件的执行过程中，合作伙伴的公钥证书将用于标识 BizTalk Server 系统中的参与方。  
  
5. 进行其他处理。  
  
   下图显示了 BizTalk Server 发送数字签名消息时的消息流。  
  
   ![](../core/media/bts-bpi-sp-msgsec-outboundsigning-r2c.gif "bts_BPI_SP_MSGSEC_OutboundSigning_R2c")  
  
   BizTalk Server 向合作伙伴发送数字签名消息时的消息流如下所示：  
  
6. 相应的 BizTalk Server 发送处理程序将消息发送给合作伙伴。  
  
7. 在发送管道的执行过程中，MIME/SMIME 编码器管道组件使用 BizTalk Server 私钥对消息进行签名。  
  
8. 合作伙伴接收来自 BizTalk Server 的消息。 合作伙伴使用 BizTalk Server 公钥验证数字签名。  
  
   BizTalk Server 将验证与传入签名消息相关联通过验证的证书颁发机构 (CA) 信任链的证书并验证证书尚未过期的证书的有效性。 验证 CA 信任链的过程涉及遍历证书上的信任链，直至到达根证书颁发机构。 这样可检验用于对消息进行签名的证书是否确实来自标识的参与方。 在运行时将对每个签名的消息进行此验证。  
  
   此外，BizTalk Server 还可以验证证书颁发机构是否尚未吊销用于对消息进行签名或加密的证书。 为此，必须从证书颁发机构下载证书吊销列表 (CRL)，然后使用 Windows 资源管理器进行安装。 有关如何验证证书的详细信息，请参阅[如何配置 MIME-SMIME 解码器管道组件](../core/how-to-configure-the-mime-smime-decoder-pipeline-component.md)。  
  
## <a name="see-also"></a>请参阅  
 [BizTalk Server 用来加密消息的证书](../core/certificates-that-biztalk-server-uses-for-encrypted-messages.md)   
 [BizTalk Server 使用的证书存储](../core/certificate-stores-that-biztalk-server-uses.md)   
 [加密和签名证书](../core/encryption-and-signing-certificates.md)   
 [发送和接收签名消息](../core/sending-and-receiving-signed-messages.md)