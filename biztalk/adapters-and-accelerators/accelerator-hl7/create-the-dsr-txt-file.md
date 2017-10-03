---
title: "创建 DSR.txt 文件 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b6947af7-c5ce-4ee6-9fe9-5c1094d0aee0
caps.latest.revision: "6"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: eef9f107b01c8e86d466cb1fb0a202e1aa5b0b54
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="create-the-dsrtxt-file"></a>创建 DSR.txt 文件
使用以下过程创建响应 DSR.txt 消息文件。 你将更高版本使用此文件来验证教程的方案。  
  
### <a name="to-create-the-dsrtxt-file"></a>若要创建 DSR.txt 文件  
  
1.  打开编辑器，如记事本，并将以下文本复制到编辑器：  
  
    ```  
    MSH|^~\&|HIS||ADT||19990505||DSR^Q01|ZXT23469|P|2.4  
    MSA|AA|MSG00003  
    QRD|200307231012|D|I|4387|||20^LI|12233|RES|ALL  
    DSP|||RESULTS FOR PATIENT#12233 SMITH, JOHN H. 07/23/03  
    DSP|||SPECIMEN#H85 COLLECTED 07/22/03 /07/0/0  
    DSP|||ELECTROLYTES  
    DSP||| SODIUM 136 [135-148] MEQ/L STAT  
    DSP||| POTASSIUM 4.2 [3.5-5.0] MEQ/L STAT  
    DSP||| CHLORIDE 91 [95-111] MEQ/L STAT  
    DSP||| CO2 25 [20-30] MEQ/L STAT  
    DSP|||CO2 25 [20-30] MEQ/L STAT|LB  
    ```  
  
2.  将文件另存**DSR.txt**中\<*驱动器*: > files\microsoft BizTalk\<版本 > 为 HL7\SDK\Interrogative 教程文件夹，然后关闭的快捷键编辑器。  
  
 继续执行[步骤 1： 创建和部署常见标头和确认架构](../../adapters-and-accelerators/accelerator-hl7/step-1-create-and-deploy-common-header-and-acknowledgment-schemas.md)。