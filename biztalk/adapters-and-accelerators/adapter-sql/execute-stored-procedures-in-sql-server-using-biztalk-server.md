---
title: "在 SQL Server 使用 BizTalk Server 中执行存储的过程 |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4329a5c1-4df9-4bf7-8a9f-e3c19cb368fb
caps.latest.revision: "16"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: 1eb15c4993476f14c59294e7f5d291c4df503aa3
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="execute-stored-procedures-in-sql-server-using-biztalk-server"></a>在 SQL Server 使用 BizTalk Server 中执行存储的过程
[!INCLUDE[adaptersql](../../includes/adaptersql-md.md)]呈现中 SQL Server 数据库作为操作的过程。 适配器客户端可以通过调用过程[!INCLUDE[adaptersqlshort](../../includes/adaptersqlshort-md.md)]与[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]。 有关如何适配器支持这些操作的详细信息，请参阅[中使用的 SQL 适配器的 SQL Server 执行存储过程](../../adapters-and-accelerators/adapter-sql/execute-stored-procedures-in-sql-server-using-the-sql-adapter.md)。 有关这些操作的 SOAP 消息结构的信息，请参阅[过程和函数的消息架构](../../adapters-and-accelerators/adapter-sql/message-schemas-for-procedures-and-functions.md)。  
  
 [!INCLUDE[adaptersqlshort](../../includes/adaptersqlshort-md.md)]此外允许适配器客户端调用：  
  
-   SQL Server 数据库中的标量函数。 请参阅[调用中使用 BizTalk Server 的 SQL Server 的标量函数](../../adapters-and-accelerators/adapter-sql/invoke-scalar-functions-in-sql-server-using-biztalk-server.md)。  
  
-   SQL Server 数据库中的表值函数。 请参阅[Invoke Table-Valued 函数中使用 BizTalk Server 的 SQL Server](../../adapters-and-accelerators/adapter-sql/invoke-table-valued-functions-in-sql-server-using-biztalk-server.md)。  
  
> [!NOTE]
>  如果您正在执行包含的用户定义类型的列的表上的操作，请确保您参考[对表和视图使用了 SQL 适配器的用户定义类型的操作](../../adapters-and-accelerators/adapter-sql/operations-on-tables-and-views-with-user-defined-types-using-the-sql-adapter.md)开始开发你的应用程序之前。  
  
## <a name="how-to-invoke-procedures-in-sql-server-database"></a>如何以调用 SQL Server 数据库中的过程  
 使用 SQL Server 数据库上执行操作[!INCLUDE[adaptersqlshort](../../includes/adaptersqlshort-md.md)]与[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]涉及过程中所述的任务[开发与 SQL 适配器的 BizTalk 应用程序的构建基块](../../adapters-and-accelerators/adapter-sql/building-blocks-to-develop-biztalk-applications-with-the-sql-adapter.md)。 若要调用 SQL Server 数据库中的过程，这些任务包括：  
  
-   创建 BizTalk 项目，并生成你想要调用 SQL Server 数据库中的过程的架构。  
  
-   在从 SQL Server 数据库发送和接收消息的 BizTalk 项目中创建消息。  
  
-   创建业务流程来调用 SQL Server 数据库中的过程。  
  
-   生成和部署 BizTalk 项目。  
  
-   配置的 BizTalk 应用程序创建的物理发送和接收端口。  
  
-   启动 BizTalk 应用程序。  
  
 本主题提供执行这些任务的说明。  
  
## <a name="sample-based-on-this-topic"></a>基于本主题的示例  
 示例中，ExecuteStoredProcedure，基于本主题提供与[!INCLUDE[adapterpacknoversion](../../includes/adapterpacknoversion-md.md)]。 有关详细信息，请参阅[SQL 适配器的示例](../../adapters-and-accelerators/adapter-sql/samples-for-the-sql-adapter.md)。  
  
## <a name="generating-schema"></a>生成架构  
 本主题演示如何调用过程，通过调用 ADD_EMP_DETAILS 过程。 此过程是通过运行这些示例提供的脚本创建的。 ADD_EMP_DETAILS 过程采用某些参数，将记录插入到员工表中，并返回插入的记录的员工 ID。 有关示例和 SQL 脚本的信息，请参阅[架构示例](../../adapters-and-accelerators/accelerator-rosettanet/schema-samples.md)。  
  
 若要调用 ADD_EMP_DETAILS 过程，它，需要生成相同的过程的架构。 请参阅[检索元数据使用的 SQL 适配器的 Visual Studio 中的 SQL Server 操作](../../adapters-and-accelerators/adapter-sql/get-metadata-for-sql-server-operations-in-visual-studio-using-the-sql-adapter.md)有关如何生成架构的详细信息。  
  
## <a name="defining-messages-and-message-types"></a>定义消息和消息类型  
 你之前生成的架构描述了业务流程中的消息所需的“类型”。 一条消息通常是一个变量，为其类型由相应的架构定义。 你现在必须创建消息业务流程，并将它们链接到你在上一步中生成的架构。  
  
#### <a name="to-create-messages-and-link-to-schema"></a>创建消息并将链接到架构  
  
1.  BizTalk 项目中添加业务流程。 从解决方案资源管理器，右键单击 BizTalk 项目名称，指向**添加**，然后单击**新项**。 键入 BizTalk 业务流程的名称，然后单击**添加**。  
  
2.  如果尚未打开，请打开 BizTalk 项目的业务流程视图窗口。 若要执行此操作，请单击**视图**，指向**其他窗口**，然后单击**业务流程视图**。  
  
3.  在业务流程视图中，右键单击**消息**，然后单击**新消息**。  
  
4.  右键单击新创建的消息中，，然后选择**属性窗口**。  
  
5.  在**属性**窗格**Message_1**，执行以下操作：  
  
    |使用此选项|执行的操作|  
    |--------------|----------------|  
    |Identifier|类型`Request`|  
    |消息类型|从下拉列表中，展开**架构**，然后选择*ExecProcedure.Procedure_dbo。ADD_EMP_DETAILS*，其中 ExecProcedure 是 BizTalk 项目的名称。 Procedure_dbo 是为调用 ADD_EMP_DETAILS 过程生成的架构。|  
  
6.  重复步骤 2 创建一条新消息。 在**属性**窗格中，为新的消息中，执行以下操作：  
  
    |使用此选项|执行的操作|  
    |--------------|----------------|  
    |Identifier|类型`Response`|  
    |消息类型|从下拉列表中，展开**架构**，然后选择*ExecProcedure.Procedure_dbo。ADD_EMP_DETAILSResponse*。|  
  
## <a name="setting-up-the-orchestration"></a>设置业务流程  
 你必须创建要使用 BizTalk 业务流程[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]为 SQL Server 上执行操作。 此业务流程，在你删除时的请求消息的定义接收位置。 [!INCLUDE[adaptersqlshort](../../includes/adaptersqlshort-md.md)]使用此消息并将其传递到 SQL Server。 从 SQL Server 的响应保存到另一个位置。 你必须包括发送和接收形状来将消息发送到 SQL Server 和接收响应，分别。 调用过程示例业务流程如下所示：  
  
 ![业务流程调用过程](../../adapters-and-accelerators/adapter-sql/media/698730c1-6aa9-49f3-97b3-adb5e6537300.gif "698730c1-6aa9-49f3-97b3-adb5e6537300")  
  
### <a name="adding-message-shapes"></a>添加消息形状  
 请确保为每个消息形状指定以下属性。 刚提到业务流程中所示，形状列中列出的名称将是消息形状的名称。  
  
|形状|形状类型|属性|  
|-----------|----------------|----------------|  
|ReceiveMessage|Receive|-将设置**名称**到*ReceiveMessage*<br />-将设置**激活**到*True*|  
|发送消息|Send|-将设置**名称**到*SendMessage*|  
|ReceiveResponse|Receive|-将设置**名称**到*ReceiveResponse*<br />-将设置**激活**到*False*|  
|SendResponse|Send|-将设置**名称**到*SendResponse*|  
  
### <a name="adding-ports"></a>添加端口  
 请确保为每个逻辑端口指定以下属性。 端口列中列出的名称是在业务流程中显示的端口的名称。  
  
|端口|属性|  
|----------|----------------|  
|MessageIn|-将设置**标识符**到*MessageIn*<br />-将设置**类型**到*MessageInType*<br />-将设置**通信模式**到*单向*<br />-将设置**通信方向**到*接收*|  
|LOBPort|-将设置**标识符**到*LOBPort*<br />-将设置**类型**到*LOBPortType*<br />-将设置**通信模式**到*请求-响应*<br />-将设置**通信方向**到*发送接收*|  
|ResponseOut|-将设置**标识符**到*ResponseOut*<br />-将设置**类型**到*ResponseOutType*<br />-将设置**通信模式**到*单向*<br />-将设置**通信方向**到*发送*|  
  
### <a name="specify-messages-for-action-shapes-and-connect-them-to-ports"></a>对于操作形状，指定消息并将其连接到端口  
 下表指定的属性和用于指定操作形状的消息，并链接到的端口的消息应设置其值。 前面提到的业务流程中所示，形状列中列出的名称将是消息形状的名称。  
  
|形状|属性|  
|-----------|----------------|  
|ReceiveMessage|-将设置**消息**到*请求*<br />-将设置**操作**到*MessageIn.Procedure.Request*|  
|发送消息|-将设置**消息**到*请求*<br />-将设置**操作**到*LOBPort.Procedure.Request*|  
|ReceiveResponse|-将设置**消息**到*响应*<br />-将设置**操作**到*LOBPort.Procedure.Response*|  
|SendResponse|-将设置**消息**到*响应*<br />-将设置**操作**到*ResponseOut.Procedure.Request*|  
  
 指定这些属性后，连接的消息形状和端口，您的业务流程已完成。  
  
 现在必须生成 BizTalk 解决方案，并将其部署到[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]。 有关详细信息，请参阅[生成和运行业务流程](../../core/building-and-running-orchestrations.md)。
  
## <a name="configuring-the-biztalk-application"></a>配置 BizTalk 应用程序  
 部署 BizTalk 项目后，将先前创建的业务流程下列出的业务流程窗格中[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理控制台。 必须使用[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理控制台配置该应用程序。 有关演练，请参阅[演练： 将基本的 BizTalk 应用程序部署](Walkthrough:%20Deploying%20a%20Basic%20BizTalk%20Application.md)。
  
 配置应用程序涉及：  
  
-   选择应用程序的主机。  
  
-   映射到中的物理端口业务流程中创建的端口[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理控制台。 对于此业务流程，您必须：  
  
    -   硬盘和放置请求消息的位置的相应文件端口上定义的位置。 BizTalk 业务流程将使用请求消息，并将其发送到 SQL Server 数据库。  
  
    -   硬盘和 BizTalk 业务流程放置包含从 SQL Server 数据库响应的响应消息的位置的相应文件端口上定义的位置。  
  
    -   定义物理 WCF 自定义或 WCF SQL 发送端口将消息发送到 SQL Server 数据库。 你必须在发送端口中指定的操作。 有关如何创建端口的信息，请参阅[手动配置到 SQL 适配器的物理端口绑定](../../adapters-and-accelerators/adapter-sql/manually-configure-a-physical-port-binding-to-the-sql-adapter.md)。
  
        > [!NOTE]
        >  生成架构使用[!INCLUDE[consumeadapterservlong](../../includes/consumeadapterservlong-md.md)]还会创建包含有关端口以及要为这些端口设置的操作信息绑定文件。 你可以导入此绑定文件与[!INCLUDE[btsBizTalkServerNoVersion](../../includes/btsbiztalkservernoversion-md.md)]管理控制台来创建发送端口 （对于出站调用），或接收 （对于入站调用） 的端口。 有关详细信息，请参阅[配置使用的端口绑定文件以使用 SQL 适配器的物理端口绑定](../../adapters-and-accelerators/adapter-sql/configure-a-physical-port-binding-using-a-port-binding-file-to-sql-adapter.md)。
  
## <a name="starting-the-application"></a>启动应用程序  
 必须在 SQL Server 数据库中启动过程的调用的 BizTalk 应用程序。 有关启动 BizTalk 应用程序的说明，请参阅[如何启动 Orchestration](../../core/how-to-start-an-orchestration.md)。
  
 在此阶段，请确保：  
  
-   FILE 接收端口，以便运行业务流程的是接收请求消息。  
  
-   要从业务流程接收响应消息的文件发送端口正在运行。  
  
-   正在运行的 WCF 自定义或 WCF SQL 发送端口将消息发送到 SQL Server 数据库。  
  
-   BizTalk 业务流程操作正在运行。  
  
## <a name="executing-the-operation"></a>执行该操作  
 运行应用程序后，必须放到该文件的请求消息接收位置。 请求消息的架构必须符合你先前生成的过程的架构。 例如，要调用 GET_EMP_DETAILS 的请求消息是：  
  
```  
<ADD_EMP_DETAILS xmlns="mssql://Microsoft.LobServices.Sql/2008/01/Procedures/dbo">  
  <emp_name>John</emp_name>  
  <emp_desig>Developer</emp_desig>  
  <salary>100000</salary>  
</ADD_EMP_DETAILS>  
```  
  
 请参阅[过程和函数的消息架构](../../adapters-and-accelerators/adapter-sql/message-schemas-for-procedures-and-functions.md)有关调用 SQL Server 中的过程的请求消息架构的详细信息数据库使用[!INCLUDE[adaptersqlshort](../../includes/adaptersqlshort-md.md)]。  
  
 业务流程使用该消息，并将其发送到 SQL Server 数据库。 从 SQL Server 数据库响应保存在定义为业务流程的一部分的其他文件位置中。 例如，来自 SQL Server 数据库中的前面的请求消息的响应是：  
  
```  
\<?xml version="1.0" encoding="utf-8" ?>   
<ADD_EMP_DETAILSResponse xmlns="mssql://Microsoft.LobServices.Sql/2008/01/Procedures/dbo">  
  <ADD_EMP_DETAILSResult>  
    <DataSet xmlns="http://schemas.datacontract.org/2004/07/System.Data">  
      \<xs:schema id="NewDataSet" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
        \<xs:element msdata:IsDataSet="true" name="NewDataSet">  
          \<xs:complexType>  
            \<xs:sequence>  
              \<xs:element minOccurs="0" maxOccurs="unbounded" name="NewTable">  
                \<xs:complexType>  
                  \<xs:sequence>  
                    \<xs:element minOccurs="0" name="Employee_ID" type="xs:int" />   
                  \</xs:sequence>  
                \</xs:complexType>  
              \</xs:element>  
            \</xs:sequence>  
          \</xs:complexType>  
        \</xs:element>  
      \</xs:schema>  
      \<diffgr:diffgram xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
        <NewDataSet xmlns="">  
          <NewTable>  
            <Employee_ID>10001</Employee_ID>   
          </NewTable>  
        </NewDataSet>  
      \</diffgr:diffgram>  
    </DataSet>  
  </ADD_EMP_DETAILSResult>  
  <ReturnValue>0</ReturnValue>   
</ADD_EMP_DETAILSResponse>  
```  
  
 在上面的响应中`<Employee_ID>`元素包含插入的记录的员工 ID。  
  
## <a name="best-practices"></a>最佳实践  
 已部署并配置 BizTalk 项目之后，你可以将配置设置导出到 XML 文件称为绑定文件。 后生成绑定文件，你可以导入的配置设置文件，以便不需要创建诸如发送端口和接收相同的业务流程的端口。 有关绑定文件的详细信息，请参阅[重用适配器绑定](../../adapters-and-accelerators/adapter-sql/reuse-sql-adapter-bindings.md)。
  
## <a name="see-also"></a>另请参阅  
[开发使用 SQL 适配器的 BizTalk 应用程序](../../adapters-and-accelerators/adapter-sql/develop-biztalk-applications-using-the-sql-adapter.md)