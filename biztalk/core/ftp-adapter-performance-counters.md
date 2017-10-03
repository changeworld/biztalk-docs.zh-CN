---
title: "FTP 适配器性能计数器 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ca5cbe67-9aa3-4194-816e-fab4eb551c07
caps.latest.revision: "12"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 9349e0d58671c783b9e1691c3bbcd4080e7f4b7b
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="ftp-adapter-performance-counters"></a>FTP 适配器性能计数器
使用性能计数器可以监视服务在站点或系统上执行的工作的特定方面。 性能计数器能够帮助您标识和解决有关服务器性能的问题。  
  
 以下性能计数器进行访问每个主机实例下**BizTalk:FTP 接收适配器**和**BizTalk:FTP 发送适配器**性能对象类别：  
  
|**类别**|**计数器**|**Description**|  
|------------------|-----------------|---------------------|  
|BizTalk:FTP Receive Adapter|Bytes received|FTP 接收适配器接收到的字节总数。 FTP 接收适配器从 FTP 服务器中完整读取一个消息后，该计数器的值才会增加。|  
||Bytes received/Sec|FTP 接收适配器每秒接收到的字节数。 该计数器只计入 FTP 接收适配器已从 FTP 服务器中完整读取的消息。|  
||收到的消息|FTP 接收适配器接收到的消息总数。 FTP 接收适配器从 FTP 服务器中完整读取一个消息后，该计数器的值才会增加。|  
||每秒接收的消息数|FTP 接收适配器每秒接收到的消息数。 该计数器只计入 FTP 接收适配器已从 FTP 服务器中完整读取的消息。|  
|BizTalk:FTP Send Adapter|Bytes sent|FTP 发送适配器发送的字节总数。 此计数器只对已写入到目标 FTP 服务器的消息时递增。|  
||Bytes sent/Sec|FTP 发送适配器每秒发送的字节数。 计数器仅适用于已写入到目标 FTP 服务器的消息。|  
||发送的消息|FTP 发送适配器已发送的消息总数。 此计数器只对已写入到目标 FTP 服务器的消息时递增。|  
||每秒发送的消息数|FTP 发送适配器每秒发送的消息数。 该计数器只计入已写入目标 FTP 服务器的消息。|  
  
## <a name="to-access-performance-counters"></a>访问性能计数器  
 依照下述步骤访问性能计数器。  
  
#### <a name="if-you-are-using-windows-2008"></a>如果您使用的是 Windows 2008  
  
1.  单击**启动**，指向**管理工具**，然后单击**性能监视器**。  
  
2.  在**性能监视器**对话框框中，展开**监视工具**，选择**性能监视器**，然后单击**添加**。  
  
3.  在**添加计数器**对话框中，从**可用计数器**列表中，展开**BizTalk:FTP**性能计数器对象，然后选择要监视的计数器  
  
4.  在**实例的所选对象**列表中，选择要监视的所选计数器，然后单击的特定实例**添加**。  若要选择的所有可用的计数器实例，选择\<**所有实例**>。  
  
5.  添加计数器后, 单击**确定**。  
  
     所选的性能计数器显示在**性能监视器**屏幕。  
  
## <a name="see-also"></a>另请参阅  
 [监视 BizTalk Server](../core/monitoring-biztalk-server.md) [运行在群集主机内的适配器处理程序的注意事项](../core/considerations-for-running-adapter-handlers-within-a-clustered-host1.md)