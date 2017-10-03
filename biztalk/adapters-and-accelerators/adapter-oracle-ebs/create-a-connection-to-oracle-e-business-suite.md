---
title: "创建与 Oracle E-business Suite 的连接 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eeeab604-155e-4806-b77a-45319a3f8cc0
caps.latest.revision: "15"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 5ffdfdc8810024e331598211529f3a594e0169f5
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="create-a-connection-to-oracle-e-business-suite"></a>创建与 Oracle E-business Suite 的连接
[!INCLUDE[adapteroracleebusinesslong](../../includes/adapteroracleebusinesslong-md.md)]是[!INCLUDE[firstref_btsWinCommFoundation](../../includes/firstref-btswincommfoundation-md.md)]自定义绑定。 在这种情况下，它使到 Oracle E-business Suite 通过 WCF 终结点地址的通信。 在 WCF 中的终结点地址标识服务的网络位置，并通常表示为统一资源标识符 (URI)。 [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]表示此位置作为连接 URI，其中包含属性的[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]用于建立与 Oracle E-business Suite 的连接。 必须指定连接 URI 时你：  
  
-   创建通道工厂或通道侦听器使用 WCF 通道模型或当你创建使用 WCF 服务模型的 WCF 客户端或服务主机。  
  
-   创建中的物理端口绑定[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]解决方案。  
  
-   使用[!INCLUDE[addadapterservreflong](../../includes/addadapterservreflong-md.md)]生成 WCF 客户端类或 WCF 服务模型解决方案的 WCF 服务接口。  
  
-   使用[!INCLUDE[consumeadapterservlong](../../includes/consumeadapterservlong-md.md)]检索消息架构从[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]BizTalk Server 解决方案。  
  
-   使用 ServiceModel 元数据实用工具 (svcutil.exe) 生成 WCF 客户端类或 WCF 服务模型解决方案的 WCF 服务接口。  

## <a name="ways-to-connect-to-oracle"></a>如何连接到 Oracle  
 [!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]支持两种方法来建立与基础的 Oracle 数据库的连接：  
  
-   **使用 tnsnames.ora**。 在此方法中，连接由适配器客户端提供的 URI 包含仅输入 tnsnames.ora 文件中的 net 服务名称。 适配器从文件中的 net 服务名称条目中提取的连接参数，如服务器名称、 服务名称、 端口号等。 若要使用此方法，必须配置运行 Oracle 客户端的计算机为 tnsnames.ora 文件中包括 Oracle 数据库的 net 服务名称。  
  
    > [!IMPORTANT]
    >  由于 Oracle 客户端存在的限制， **DataSourceName**中的参数 （net 服务名称）[创建 Oracle E-business Suite 连接 URI](../../adapters-and-accelerators/adapter-oracle-ebs/create-the-oracle-e-business-suite-connection-uri.md)不能包含超过 39 个字符，如果你是在事务中执行操作。 因此，如果你在事务中执行操作，请确保**DataSourceName**参数的值是否小于或等于 39 个字符。  
  
-   **而无需使用 tnsnames.ora**。 在此方法中，适配器客户端输入直接在连接 URI 中的连接参数。 这不需要的 net 服务名称必须包含在客户端计算机上的 tnsnames.ora 文件中。 此方法甚至不需要在客户端计算机上显示的 tnsnames.ora 文件。  
  
    > [!IMPORTANT]
    >  如果你在事务中执行操作，则不支持这种模式的连接。 这是因为 Oracle 客户端的限制。  

## <a name="in-this-section"></a>在本节中    
 以下主题介绍如何之间建立连接[!INCLUDE[adapteroraclebusinessshort](../../includes/adapteroraclebusinessshort-md.md)]和 Oracle E-business Suite:  
  
-   [配置 Oracle 客户端为 E-business Suite 适配器](../../adapters-and-accelerators/adapter-oracle-ebs/configure-the-oracle-client-for-the-e-business-suite-adapter.md)： 有关使用 tnsnames.ora 到 cconfiguring Oracle 客户端 （仅在使用 tnsnames.ora 以建立连接时，才需要） 的信息  
  
-   [创建 Oracle E-business Suite 连接 URI](../../adapters-and-accelerators/adapter-oracle-ebs/create-the-oracle-e-business-suite-connection-uri.md)： 有关连接属性和 Oracle E-business Suite 连接 URI 的结构信息
  
-   [将连接到使用 Windows 身份验证的 Oracle E-business Suite](../../adapters-and-accelerators/adapter-oracle-ebs/connect-to-oracle-e-business-suite-using-windows-authentication.md)： 有关连接到 Oracle 使用 Windows 身份验证信息
  