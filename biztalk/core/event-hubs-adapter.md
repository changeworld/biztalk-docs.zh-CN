---
title: 使用事件中心适配器 |Microsoft Docs
description: 发送和接收消息在 BizTalk Server 中使用 Azure 事件中心适配器
ms.custom: ''
ms.date: 11/16/2017
ms.prod: biztalk-server
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: MandiOhlinger
ms.author: plarsen
manager: anneta
ms.openlocfilehash: a1e30b1ab1aacc1c5134d1dd5b44744bd670b308
ms.sourcegitcommit: c3070a7a3f332857357f056dc632829b43869c17
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/14/2018
ms.locfileid: "51630330"
---
# <a name="event-hub-adapter-in-biztalk"></a>在 BizTalk 中的事件中心适配器

## <a name="overview"></a>概述
**从开始[!INCLUDE[bts2016_md](../includes/bts2016-md.md)]功能包 2**，可以发送和接收 BizTalk Server 和 Azure 事件中心之间的消息。 

Azure 事件中心是高度可缩放的数据流平台，并可以接收和处理数以百万计的每秒事件数。 [什么是事件中心？](https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs)提供了更多详细信息。

## <a name="prerequisites"></a>必要條件

* 创建[Azure 事件中心命名空间和事件中心](https://docs.microsoft.com/azure/event-hubs/event-hubs-create)
* 创建[Azure blob 存储帐户的容器](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)
* 安装[功能包 2](https://aka.ms/bts2016fp2) BizTalk 服务器上

现在创建事件中心，并且你有连接字符串需要发送和接收事件。

## <a name="send-messages-to-event-hubs"></a>将消息发送到事件中心

1.  在 BizTalk Server 管理控制台中，右键单击**发送端口**，选择**新建**，然后选择**静态单向发送端口**。

    [创建发送端口](../core/how-to-create-a-send-port2.md)提供一些指导。

2. 输入**名称**。 在**传输**，请设置**类型**到**EventHub**，然后选择**配置**。 

3. 配置**Azure 帐户**属性： 

    |使用此选项|执行的操作|  
    |---|---|  
    | **单一登录** | 登录到 Azure 帐户 |
    | **订阅** | 选择具有 EventHubs 命名空间的订阅 |
    | **资源组** | 选择资源组具有 EventHubs 命名空间 |

4. 配置**终结点**属性： 

    |使用此选项|执行的操作|  
    |---|---|  
    | **Namespace** | 选择事件中心命名空间，这是类似于 sb: / /*youreventhubnamespace*.servicebus.windows.net/ |
    | **名称** | 选择事件中心 （这创建事件中心命名空间中的） 的名称 |
    | **默认分区键** | 可选。 [事件中心编程指南](https://docs.microsoft.com/azure/event-hubs/event-hubs-programming-guide)提供有关此密钥的更多详细信息。 |
    | **身份验证** | **Namespace 访问签名**是默认设置，并自动使用在创建事件中心命名空间时创建 RootManageSharedAccessKey。<br/><br/>**实体访问签名**是可以在事件中心的级别 （不是事件中心命名空间的级别） 创建的 SAS 策略。 <br/><br/>[事件中心功能概述](https://docs.microsoft.com/azure/event-hubs/event-hubs-features)说明的详细信息。 |

    完成后，您的属性类似于以下： 

    ![终结点属性](../core/media/event-hub-endpoint-properties.png)


5. 可选。 配置**消息**属性。 **用户定义的消息属性的 Namespace**值表示 BizTalk 消息架构映射到事件中心消息属性。

6. 选择**确定**以保存所做的更改。 


### <a name="test-your-send-port"></a>测试您的发送端口

可以使用简单文件接收端口和位置将消息发送到 Azure 事件中心。 

1. 创建使用文件适配器的接收端口。 在你接收位置，则设置**接收文件夹**到**C:\Temp\In\\**，并将文件掩码设置为 **\*.xml**。
2. 在事件中心将发送端口属性，设置**筛选器**到`BTS.ReceivePortName == FileReceivePort`。
3. 将以下粘贴到文本编辑器中，并将该文件作为**EventHubMessage.xml**。 这是您的示例消息。 

    ```xml
    <Data>
      <DataID>DataID_0</DataID>
      <DataDetails>DataDetails_0</DataDetails>
    </Data>
    ```

4. 启动文件接收位置和事件中心发送端口。
5. 复制**EventHubMessage.xml**到接收文件夹的示例消息 (C:\Temp\In\)。 发送端口将 XML 文件发送到事件中心。

## <a name="receive-messages-from-event-hubs"></a>从事件中心接收消息

1. 在 BizTalk Server 管理控制台中，右键单击**接收端口**，选择**新建**，然后选择**单向接收端口**。 

    [创建接收端口](../core/how-to-create-a-receive-port.md)提供一些指导。

2. 输入一个名称，并选择**接收位置**。 

3. 选择**新建**，并**名称**接收位置。 在中**传输**，选择**EventHub**从**类型**下拉列表，然后选择**配置**。 

4. 配置**Azure 帐户**属性： 

    |使用此选项|执行的操作|  
    |---|---|  
    | **单一登录** | 登录到 Azure 帐户 |
    | **订阅** | 选择具有 EventHubs 命名空间的订阅 |
    | **资源组** | 选择资源组具有 EventHubs 命名空间 |

4. 配置**终结点**属性： 

    |使用此选项|执行的操作|  
    |---|---|  
    | **Namespace** | 选择事件中心命名空间，这是类似于 sb: / /*youreventhubnamespace*.servicebus.windows.net/ |
    | **名称** | 选择事件中心 （这创建事件中心命名空间中的） 的名称 |
    | **使用者组** | 选择在事件中心内的使用者组。 自动创建默认组。 <br/><br/>[事件中心功能概述](https://docs.microsoft.com/azure/event-hubs/event-hubs-features)提供了更多详细信息。 |
    | **身份验证** | **Namespace 访问签名**是默认设置，并自动使用在创建事件中心命名空间时创建 RootManageSharedAccessKey。<br/><br/>**实体访问签名**是可以在事件中心的级别 （不是事件中心命名空间的级别） 创建的 SAS 策略。 <br/><br/>[事件中心功能概述](https://docs.microsoft.com/azure/event-hubs/event-hubs-features)说明的详细信息。 |

    完成后，您的属性类似于以下： 

    ![终结点属性](../core/media/event-hub-endpoint-receive-properties.png)

5. 配置**检查点**属性。 此适配器使用的 Azure blob 存储帐户以可靠地读取事件使用检查点，并从中重新启动恢复。 

    **存储身份验证**   
    选择身份验证方法。 通常情况下，建议使用共享访问签名。 以下链接是有用的资源以帮助您决定哪种适合你的方案：<br/><br/>[关于 Azure 存储帐户](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account)<br/>[使用共享的访问签名 (SAS)](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1)

    完成后，您的属性类似于以下： 

    ![检查点属性](../core/media/event-hub-receive-checkpoint.png)

6. 配置**消息**属性： 

    |使用此选项|执行的操作|  
    |---|---|  
    | **Namespace 为用户定义消息属性** | `http://schemas.microsoft.com/BizTalk/EventHubAdapter/EventData/User` 为默认架构，但您可以输入另一个架构。 此值表示 BizTalk 消息架构映射到事件中心消息属性。 |
    | **将提升用户定义的属性** | 可选。 如果您愿意，可以升级这些属性。 <br/><br/>**注意**<br/>需要提升的属性应具有部署的 porperty 架构*之前*接收事件。|

7. 选择**确定**以保存所做的更改。 

### <a name="test-your-receive-settings"></a>测试在接收设置

可以使用简单的 File 发送端口以从 Azure 事件中心接收消息。 

1. 创建使用文件适配器的发送端口。 在发送端口的属性，设置**目标文件夹**到**C:\Temp\Out\\**，并将设置和**文件的名称**到 **%MessageID%.xml**.
2. 在你的文件将发送端口属性，设置**筛选器**到`BTS.ReceivePortName == EHReceivePort`。
3. 开始事件中心接收位置和 File 发送端口。
4. 查找目标文件夹 (c:\temp\out) 中的消息。

## <a name="do-more"></a>执行更多操作
事件中心被视为"前门"到其他 Azure 服务，包括 Azure Data Lake、 HD Insight 和的详细信息的很多。 它旨在处理大量消息，并在快速进行处理。 了解有关事件中心和及其功能的更多信息： 

[事件中心功能概述](https://docs.microsoft.com/azure/event-hubs/event-hubs-features)  
[什么是事件中心？](https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs)
