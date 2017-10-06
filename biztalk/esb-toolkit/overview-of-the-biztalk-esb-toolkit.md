---
title: "BizTalk Server 中的 ESB 工具包概述 |Microsoft 文档"
description: "ESB 工具包中，以及它能做什么 BizTalk Server 中的说明"
caps.latest.revision: "6"
author: MandiOhlinger
manager: anneta
ms.custom: 
ms.date: 08/10/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3e190b34-40bc-4f27-9b4f-56e98591e1d4
ms.author: mandia
ms.openlocfilehash: 9ce0bbe3710530a63127701447db87b0a3135b4a
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="what-is-the-biztalk-esb-toolkit"></a><span data-ttu-id="398a6-103">BizTalk ESB 工具包是什么</span><span class="sxs-lookup"><span data-stu-id="398a6-103">What is the BizTalk ESB Toolkit</span></span>

## <a name="overview"></a><span data-ttu-id="398a6-104">概述</span><span class="sxs-lookup"><span data-stu-id="398a6-104">Overview</span></span>
<span data-ttu-id="398a6-105">[!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]扩展的 BizTalk Server 功能，以支持松散耦合的消息传递体系结构。</span><span class="sxs-lookup"><span data-stu-id="398a6-105">The [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)] extends the capabilities of BizTalk Server to support a loosely coupled messaging architecture.</span></span> <span data-ttu-id="398a6-106">大多数开发人员熟悉面向代码，过程，或面向对象的开发范例。</span><span class="sxs-lookup"><span data-stu-id="398a6-106">Most developers are familiar with code-oriented, procedural, or object-oriented development paradigms.</span></span> <span data-ttu-id="398a6-107">但是，在开始开发 BizTalk 解决方案，开发人员往往会忽略 BizTalk Server 的面向消息的功能。</span><span class="sxs-lookup"><span data-stu-id="398a6-107">However, when starting to develop BizTalk solutions, developers tend to overlook the message-oriented capabilities of BizTalk Server.</span></span>  
  
 <span data-ttu-id="398a6-108">BizTalk Server 包括的功能强大发布/订阅机制，用于创建和填充订阅。</span><span class="sxs-lookup"><span data-stu-id="398a6-108">BizTalk Server includes a powerful publish/subscribe mechanism that works by creating and filling subscriptions.</span></span> <span data-ttu-id="398a6-109">当一条新消息到达时 BizTalk 消息框数据库中时，消息代理标识订阅服务器，并将消息发送到有订阅的任何终结点。</span><span class="sxs-lookup"><span data-stu-id="398a6-109">When a new message arrives in the BizTalk Message Box database, a message agent identifies subscribers and sends the message to any endpoints that have subscriptions.</span></span> <span data-ttu-id="398a6-110">可以在几个方面，包括绑定到接收端口，具有关联的接收等待一条消息，或创建具有筛选器条件相匹配的属性 （如类型，接收消息的发送端口业务流程创建订阅点或可路由的属性的值）。</span><span class="sxs-lookup"><span data-stu-id="398a6-110">Subscriptions can be created in several ways, including binding an orchestration to a receive port, having a correlated receive waiting for a message, or creating a send port with a filter condition that matches a property of the message (such as the type, the receive point, or the value of a routable property).</span></span>  
  
 <span data-ttu-id="398a6-111">通过提供此高效且可伸缩的方法，BizTalk Server 使开发人员创建一系列的离散的子进程、 定义触发其调用，而不用担心序列的消息的类型。</span><span class="sxs-lookup"><span data-stu-id="398a6-111">By providing this efficient and scalable approach, BizTalk Server enables developers to create a series of discrete sub-processes, define the types of messages that trigger their invocation, and not worry about the sequence.</span></span> <span data-ttu-id="398a6-112">由消息的到达启动的进程执行其处理的消息;处理该消息后，它可以将这个或另一个消息传递到消息框中的数据库，而又可以激活一个或多个子进程。</span><span class="sxs-lookup"><span data-stu-id="398a6-112">A process initiated by the arrival of a message performs its processing on the message; after it processes the message, it can deliver this or another message to the Message Box database, which, in turn, may activate one or more sub-processes.</span></span>  
  
 <span data-ttu-id="398a6-113">Microsoft 提供了所需的构建全面的面向服务基础结构，包括 Windows Server、.NET Framework 和 BizTalk Server 中的关键构建基块。</span><span class="sxs-lookup"><span data-stu-id="398a6-113">Microsoft provides key building blocks that are required for building comprehensive Service-Oriented Infrastructures, including Windows Server, the .NET Framework, and BizTalk Server.</span></span> <span data-ttu-id="398a6-114">[!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]由于其提供的最常见的 ESB 服务，包括以下基础基于 BizTalk Server:</span><span class="sxs-lookup"><span data-stu-id="398a6-114">The [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)] is based on BizTalk Server because it provides the basis for the most common ESB services, including the following:</span></span>  
  
-   <span data-ttu-id="398a6-115">消息路由</span><span class="sxs-lookup"><span data-stu-id="398a6-115">Message routing</span></span>  
  
-   <span data-ttu-id="398a6-116">消息验证</span><span class="sxs-lookup"><span data-stu-id="398a6-116">Message validation</span></span>  
  
-   <span data-ttu-id="398a6-117">消息转换</span><span class="sxs-lookup"><span data-stu-id="398a6-117">Message transformation</span></span>  
  
-   <span data-ttu-id="398a6-118">可扩展适配器框架，用于连接</span><span class="sxs-lookup"><span data-stu-id="398a6-118">Extensible adapter framework for connectivity</span></span>  
  
-   <span data-ttu-id="398a6-119">服务业务流程</span><span class="sxs-lookup"><span data-stu-id="398a6-119">Service orchestration</span></span>  
  
-   <span data-ttu-id="398a6-120">业务规则引擎</span><span class="sxs-lookup"><span data-stu-id="398a6-120">Business rules engine</span></span>  
  
-   <span data-ttu-id="398a6-121">业务活动监视</span><span class="sxs-lookup"><span data-stu-id="398a6-121">Business activity monitoring</span></span>  
  
-   <span data-ttu-id="398a6-122">Web 服务和 WS-* 集成 （WCF 适配器）</span><span class="sxs-lookup"><span data-stu-id="398a6-122">Web service and WS-* integration (WCF adapter)</span></span>  

## <a name="core-capabilities"></a><span data-ttu-id="398a6-123">核心功能</span><span class="sxs-lookup"><span data-stu-id="398a6-123">Core capabilities</span></span>  
 <span data-ttu-id="398a6-124">[!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]扩展 BizTalk Server 提供一系列上构建强大、 连接、 面向服务的应用程序的已设定焦点的新功能的功能。</span><span class="sxs-lookup"><span data-stu-id="398a6-124">The [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)] extends the functionality of BizTalk Server to provide a range of new capabilities focused on building robust, connected, service-oriented applications.</span></span> <span data-ttu-id="398a6-125">[!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)] BizTalk 服务器组件将其视为单独的可连接的工作单元根据需要，以形成松散耦合解决方案。</span><span class="sxs-lookup"><span data-stu-id="398a6-125">The [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)] treats BizTalk Server components as individual units of work that can be connected, as desired, to form loosely coupled solutions.</span></span> <span data-ttu-id="398a6-126">以下是一些核心功能，[!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]提供增强的 BizTalk Server 功能：</span><span class="sxs-lookup"><span data-stu-id="398a6-126">The following are some of the core capabilities that the [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)] provides to enhance the capabilities of BizTalk Server:</span></span>  
  
-   <span data-ttu-id="398a6-127">**策略驱动的中介。**</span><span class="sxs-lookup"><span data-stu-id="398a6-127">**Policy driven mediation.**</span></span> <span data-ttu-id="398a6-128">[!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]执行下列任务：</span><span class="sxs-lookup"><span data-stu-id="398a6-128">The [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)] does the following:</span></span>  
  
    -   <span data-ttu-id="398a6-129">它提供了基于路线的路由支持在发布消息时的轻型服务组合。</span><span class="sxs-lookup"><span data-stu-id="398a6-129">It provides itinerary-based routing that supports lightweight service composition at the time of message publication.</span></span> <span data-ttu-id="398a6-130">这种方法可以动态发现的服务终结点和中介邮件路由使用服务注册表或业务规则策略的要求。</span><span class="sxs-lookup"><span data-stu-id="398a6-130">This approach allows dynamic discovery of service endpoints and mediation requirements for message routing using a service registry or the business rules policy.</span></span>  
  
    -   <span data-ttu-id="398a6-131">收到了基于路线的使用服务器端路线，可动态解析并添加到消息上下文后面的消息进行路由，它会添加的策略集中的支持。</span><span class="sxs-lookup"><span data-stu-id="398a6-131">It adds support for policy centralization for itinerary-based routing using server-side itineraries that are dynamically resolved and added to the message context after a message is received.</span></span> <span data-ttu-id="398a6-132">利用管理路线在一个中心位置，从完全不能识别如何路由其请求的客户端的消息的处理。</span><span class="sxs-lookup"><span data-stu-id="398a6-132">Managing itineraries in a central location enables the processing of messages from clients that are completely unaware of how their requests are being routed.</span></span>  
  
    -   <span data-ttu-id="398a6-133">它使用的增强的版本[!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]冲突解决程序和适配器的提供程序框架，从而使动态解析终结点以及转换要求; 这可以有效地将从服务的使用者脱耦。</span><span class="sxs-lookup"><span data-stu-id="398a6-133">It uses an enhanced version of the [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)] Resolver and Adapter Provider Framework, which enables dynamic resolution of endpoints and transformation requirements; this effectively decouples the consumer from the services.</span></span>  
  
-   <span data-ttu-id="398a6-134">**将系统的连接。**</span><span class="sxs-lookup"><span data-stu-id="398a6-134">**Connecting systems.**</span></span> <span data-ttu-id="398a6-135">[!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]执行下列任务：</span><span class="sxs-lookup"><span data-stu-id="398a6-135">The [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)] does the following:</span></span>  
  
    -   <span data-ttu-id="398a6-136">它提供了规范化 XML 消息命名空间的管道组件。</span><span class="sxs-lookup"><span data-stu-id="398a6-136">It provides pipeline components that normalize XML message namespaces.</span></span>  
  
    -   <span data-ttu-id="398a6-137">它与集成 JMS 通过 WebSphere MQ 适配器的 BizTalk Server。</span><span class="sxs-lookup"><span data-stu-id="398a6-137">It integrates with JMS through the WebSphere MQ adapter for BizTalk Server.</span></span>  
  
    -   <span data-ttu-id="398a6-138">它便于启用动态服务聚合、 消息路由、 消息验证，以及消息转换的消息交换模式。</span><span class="sxs-lookup"><span data-stu-id="398a6-138">It facilitates message exchange patterns that enable dynamic service aggregation, message routing, message validation, and message transformation.</span></span>  
  
    -   <span data-ttu-id="398a6-139">它支持从注册表和使用 UDDI 3.0 的存储库集成的服务终结点发现。</span><span class="sxs-lookup"><span data-stu-id="398a6-139">It supports service endpoint discovery from registry and repository integration using UDDI 3.0.</span></span>  
  
    -   <span data-ttu-id="398a6-140">它支持通过业务线 (LOB) 适配器路由通过 WCF 自定义 BizTalk 适配器用于 BizTalk Server 的消息。</span><span class="sxs-lookup"><span data-stu-id="398a6-140">It supports message routing through line-of-business (LOB) adapters by using the WCF-Custom BizTalk Adapter for BizTalk Server.</span></span>  
  
-   <span data-ttu-id="398a6-141">**管理和监视。**</span><span class="sxs-lookup"><span data-stu-id="398a6-141">**Management and monitoring.**</span></span> <span data-ttu-id="398a6-142">[!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]执行下列任务：</span><span class="sxs-lookup"><span data-stu-id="398a6-142">The [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)] does the following:</span></span>  
  
    -   <span data-ttu-id="398a6-143">它提供异常管理框架和工具。</span><span class="sxs-lookup"><span data-stu-id="398a6-143">It provides exception management framework and tools.</span></span>  
  
    -   <span data-ttu-id="398a6-144">它便于消息修复并重新提交使用管理门户中，作为示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="398a6-144">It facilitates message repair and resubmission using a management portal, shipped as a sample application.</span></span> <span data-ttu-id="398a6-145">一个特定的错误发生时，此 Web 应用程序还支持可自定义电子邮件通知。</span><span class="sxs-lookup"><span data-stu-id="398a6-145">This Web application also supports customizable e-mail notifications when a specific error occurs.</span></span>  
  
    -   <span data-ttu-id="398a6-146">它允许 BizTalk Server 终结点和注册表的集成、 管理和发布。</span><span class="sxs-lookup"><span data-stu-id="398a6-146">It allows BizTalk Server endpoint and registry integration, management, and publication.</span></span>  
  
    -   <span data-ttu-id="398a6-147">它提供了已进行版本管理的服务器端路线的集中式存储库。</span><span class="sxs-lookup"><span data-stu-id="398a6-147">It provides a centralized repository of versioned server-side itineraries.</span></span>  
  
    -   <span data-ttu-id="398a6-148">它报告和分析 BizTalk Server 应用程序支持。</span><span class="sxs-lookup"><span data-stu-id="398a6-148">It supports reporting and analytics for BizTalk Server applications.</span></span>  
  
    -   <span data-ttu-id="398a6-149">它包括要跟踪路线服务执行，包括开始时间、 结束时间和服务中介序列的业务活动监视的组件。</span><span class="sxs-lookup"><span data-stu-id="398a6-149">It includes Business Activity Monitoring components to track itinerary service execution, including start time, end time, and service mediation sequence.</span></span>  
  
-   <span data-ttu-id="398a6-150">**SOA 监管。**</span><span class="sxs-lookup"><span data-stu-id="398a6-150">**SOA governance.**</span></span> <span data-ttu-id="398a6-151">[!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)]执行下列任务：</span><span class="sxs-lookup"><span data-stu-id="398a6-151">The [!INCLUDE[esbToolkit](../includes/esbtoolkit-md.md)] does the following:</span></span>  
  
    -   <span data-ttu-id="398a6-152">它与第三方 SOA 管理解决方案，包括嵌入的管理代理从 AmberPoint 和 SOA 软件的 BizTalk Server 的集成。</span><span class="sxs-lookup"><span data-stu-id="398a6-152">It integrates with third-party SOA governance solutions, including embedded management agents for BizTalk Server from AmberPoint and SOA Software.</span></span>  

> [!TIP]
> <span data-ttu-id="398a6-153">[了解 BizTalk Server](../core/understanding-biztalk-server.md)提供了消息传送的引擎，以及更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="398a6-153">[Understanding BizTalk Server](../core/understanding-biztalk-server.md) provides more details on the messaging engine, and more.</span></span>

## <a name="get-some-help"></a><span data-ttu-id="398a6-154">获取帮助</span><span class="sxs-lookup"><span data-stu-id="398a6-154">Get some help</span></span>
<span data-ttu-id="398a6-155">获取帮助，并帮助其他人在[BizTalk ESB 工具包论坛](http://go.microsoft.com/fwlink/?LinkID=185951&clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="398a6-155">Get some help, and help others at the [BizTalk ESB Toolkit forums](http://go.microsoft.com/fwlink/?LinkID=185951&clcid=0x409).</span></span>

## <a name="next-steps"></a><span data-ttu-id="398a6-156">后续步骤</span><span class="sxs-lookup"><span data-stu-id="398a6-156">Next steps</span></span>
[<span data-ttu-id="398a6-157">BizTalk ESB 工具包的内容</span><span class="sxs-lookup"><span data-stu-id="398a6-157">Contents of the BizTalk ESB Toolkit</span></span>](contents-of-the-biztalk-esb-toolkit.md)  