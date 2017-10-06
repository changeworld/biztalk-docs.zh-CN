---
title: "清单： 配置 Internet Information Services |Microsoft 文档"
ms.custom: 
ms.date: 06/08/2017
ms.prod: biztalk-server
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 186f82c0-bd50-4c79-a403-8b0d91cc68d6
caps.latest.revision: "2"
author: MandiOhlinger
ms.author: mandia
manager: anneta
ms.openlocfilehash: bfb3323bd122fd9dba007321b4ffef90bdbe7214
ms.sourcegitcommit: cb908c540d8f1a692d01dc8f313e16cb4b4e696d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2017
---
# <a name="checklist-configuring-internet-information-services"></a><span data-ttu-id="b299e-102">清单： 配置 Internet Information Services</span><span class="sxs-lookup"><span data-stu-id="b299e-102">Checklist: Configuring Internet Information Services</span></span>
<span data-ttu-id="b299e-103">本主题列出了用于在生产中准备 Internet 信息服务 (IIS) 时应遵循的步骤[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]环境。</span><span class="sxs-lookup"><span data-stu-id="b299e-103">This topic lists steps that should be followed when preparing Internet Information Services (IIS) for use in a production [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] environment.</span></span>  
  
|<span data-ttu-id="b299e-104">步骤</span><span class="sxs-lookup"><span data-stu-id="b299e-104">Steps</span></span>|<span data-ttu-id="b299e-105">参考</span><span class="sxs-lookup"><span data-stu-id="b299e-105">Reference</span></span>|  
|-----------|---------------|  
|<span data-ttu-id="b299e-106">将 IIS 设置为发布[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]Web 服务和 WCF 服务</span><span class="sxs-lookup"><span data-stu-id="b299e-106">Set up IIS to publish [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Web services and WCF services</span></span>|<span data-ttu-id="b299e-107">-请参阅["启用 Web 服务"](http://go.microsoft.com/fwlink/?LinkId=153335) (http://go.microsoft.com/fwlink/?LinkId=153335) BizTalk Server 文档中。</span><span class="sxs-lookup"><span data-stu-id="b299e-107">-   See ["Enabling Web Services"](http://go.microsoft.com/fwlink/?LinkId=153335) (http://go.microsoft.com/fwlink/?LinkId=153335) in the BizTalk Server documentation.</span></span><br /><span data-ttu-id="b299e-108">-请参阅["配置 IIS 的独立 WCF 接收适配器"](http://go.microsoft.com/fwlink/?LinkId=202825)(http://go.microsoft.com/fwlink/?LinkId=202825) BizTalk Server 文档中。</span><span class="sxs-lookup"><span data-stu-id="b299e-108">-   See ["Configuring IIS for the Isolated WCF Receive Adapters"](http://go.microsoft.com/fwlink/?LinkId=202825)(http://go.microsoft.com/fwlink/?LinkId=202825) in the BizTalk Server documentation.</span></span>|  
|<span data-ttu-id="b299e-109">验证[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]Web 服务和 WCF 服务正常工作。</span><span class="sxs-lookup"><span data-stu-id="b299e-109">Verify that [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Web services and WCF services are working correctly.</span></span>|<span data-ttu-id="b299e-110">-请参阅["测试已发布的 Web 服务"](http://go.microsoft.com/fwlink/?LinkId=153336) (http://go.microsoft.com/fwlink/?LinkId=153336) BizTalk Server 文档中。</span><span class="sxs-lookup"><span data-stu-id="b299e-110">-   See ["Testing Published Web Services"](http://go.microsoft.com/fwlink/?LinkId=153336) (http://go.microsoft.com/fwlink/?LinkId=153336) in the BizTalk Server documentation.</span></span><br /><span data-ttu-id="b299e-111">-请参阅["如何创建.NET 应用程序到测试 WCF 服务发布与 BizTalk WCF 服务发布向导"](http://go.microsoft.com/fwlink/?LinkId=202830) (http://go.microsoft.com/fwlink/?LinkId=202830) BizTalk Server 文档中。</span><span class="sxs-lookup"><span data-stu-id="b299e-111">-   See ["How to Create a .NET Application to Test a WCF Service Published with the BizTalk WCF Service Publishing Wizard"](http://go.microsoft.com/fwlink/?LinkId=202830) (http://go.microsoft.com/fwlink/?LinkId=202830) in the BizTalk Server documentation.</span></span>|  
|<span data-ttu-id="b299e-112">锁定[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]Web 服务：</span><span class="sxs-lookup"><span data-stu-id="b299e-112">Lock down [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Web services:</span></span><br /><br /> <span data-ttu-id="b299e-113">-关闭 web.config 或 machine.config 文件中的调试开关。</span><span class="sxs-lookup"><span data-stu-id="b299e-113">-   Turn off the Debug switch in the web.config or machine.config file.</span></span><br /><span data-ttu-id="b299e-114">-配置以便仅允许的谓词的文章。</span><span class="sxs-lookup"><span data-stu-id="b299e-114">-   Configure so that POST is the only verb allowed.</span></span>|<span data-ttu-id="b299e-115">-请参阅 Microsoft 知识库文章 815145， ["HOW TO： 锁定 ASP.NET Web 应用程序或 Web 服务"](http://go.microsoft.com/fwlink/?LinkId=153337) (http://go.microsoft.com/fwlink/?LinkId=153337)。</span><span class="sxs-lookup"><span data-stu-id="b299e-115">-   See Microsoft Knowledge Base Article 815145, ["HOW TO: Lock Down an ASP.NET Web Application or Web Service"](http://go.microsoft.com/fwlink/?LinkId=153337) (http://go.microsoft.com/fwlink/?LinkId=153337).</span></span><br /><span data-ttu-id="b299e-116">-请参阅["ASP.NET 编辑规则对话框中"](http://go.microsoft.com/fwlink/?LinkID=64566) (http://go.microsoft.com/fwlink/?LinkID=64566) 中的.NET Framework 2.0 文档。</span><span class="sxs-lookup"><span data-stu-id="b299e-116">-   See ["ASP.NET Edit Rule Dialog Box"](http://go.microsoft.com/fwlink/?LinkID=64566) (http://go.microsoft.com/fwlink/?LinkID=64566) in the .NET Framework 2.0 documentation.</span></span>|  
|<span data-ttu-id="b299e-117">配置负载平衡使用 NLB （或其他负载平衡器） 可负载分摊 BizTalk 服务器 Web 服务和 WCF 服务。</span><span class="sxs-lookup"><span data-stu-id="b299e-117">Configure load balancing by using NLB (or other load balancer) to balance load across BizTalk Server Web services and WCF services.</span></span>|<span data-ttu-id="b299e-118">-   **对于 Windows Server 2008**： 请参阅["网络负载平衡部署指南"](http://go.microsoft.com/fwlink/?LinkId=153139) (http://go.microsoft.com/fwlink/?LinkId=153139)。</span><span class="sxs-lookup"><span data-stu-id="b299e-118">-   **For Windows Server 2008**: See ["Network Load Balancing Deployment Guide"](http://go.microsoft.com/fwlink/?LinkId=153139) (http://go.microsoft.com/fwlink/?LinkId=153139).</span></span><br /><span data-ttu-id="b299e-119">-   **对于 Windows Server 2003**： 请参阅["网络负载平衡： 配置 Windows 2000 和 Windows Server 2003 最佳做法"](http://go.microsoft.com/fwlink/?LinkID=69529) (http://go.microsoft.com/fwlink/?LinkID=69529)。</span><span class="sxs-lookup"><span data-stu-id="b299e-119">-   **For Windows Server 2003**: See ["Network Load Balancing: Configuration Best Practices for Windows 2000 and Windows Server 2003"](http://go.microsoft.com/fwlink/?LinkID=69529) (http://go.microsoft.com/fwlink/?LinkID=69529).</span></span>|  
|<span data-ttu-id="b299e-120">更改 IIS 和 ASP.NET 设置，以优化 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="b299e-120">Change IIS and ASP.NET settings for tuning Web services.</span></span> <span data-ttu-id="b299e-121">**注意：** ASP.NET 2.0 包括自动优化，因此修改这些设置应不需要为 ASP.NET 2.0 Web 站点自动配置在何处启用网站的 web.config 文件\<processModel > 部分。</span><span class="sxs-lookup"><span data-stu-id="b299e-121">**Note:**  ASP.NET 2.0 includes auto-tuning, so modifying these settings should not be needed for the web.config file of ASP.NET 2.0 Web sites where autoConfig is enabled in the \<processModel> section.</span></span> <span data-ttu-id="b299e-122">"autoConfig = true"是默认设置。</span><span class="sxs-lookup"><span data-stu-id="b299e-122">“autoConfig=true” is the default setting.</span></span>|<span data-ttu-id="b299e-123">查看"ASP.NET 设置可能会影响 HTTP 或 SOAP 适配器性能"主题的部分["配置参数，影响适配器性能"](http://go.microsoft.com/fwlink/?LinkId=153338) (http://go.microsoft.com/fwlink/?LinkId=153338) BizTalk Server 文档中。</span><span class="sxs-lookup"><span data-stu-id="b299e-123">Review the "ASP.NET settings that can impact HTTP or SOAP Adapter performance” section of the topic ["Configuration Parameters that Affect Adapter Performance"](http://go.microsoft.com/fwlink/?LinkId=153338) (http://go.microsoft.com/fwlink/?LinkId=153338) in the BizTalk Server documentation.</span></span>|  
|<span data-ttu-id="b299e-124">实现一种方法来发布[!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)]Web 服务和 WCF 服务。</span><span class="sxs-lookup"><span data-stu-id="b299e-124">Implement an approach for publishing [!INCLUDE[btsBizTalkServerNoVersion](../includes/btsbiztalkservernoversion-md.md)] Web services and WCF services.</span></span>|<span data-ttu-id="b299e-125">-请参阅[发布的面向 Internet 的 Web 服务和 WCF 服务](../technical-guides/publishing-internet-facing-web-services-and-wcf-services.md)。</span><span class="sxs-lookup"><span data-stu-id="b299e-125">-   See [Publishing Internet-facing Web Services and WCF Services](../technical-guides/publishing-internet-facing-web-services-and-wcf-services.md).</span></span><br /><span data-ttu-id="b299e-126">-请参阅["发布 WCF 服务"](http://go.microsoft.com/fwlink/?LinkId=202827) (http://go.microsoft.com/fwlink/?LinkId=202827) BizTalk Server 文档中。</span><span class="sxs-lookup"><span data-stu-id="b299e-126">-   See ["Publishing WCF Services"](http://go.microsoft.com/fwlink/?LinkId=202827) (http://go.microsoft.com/fwlink/?LinkId=202827) in the BizTalk Server documentation.</span></span>|  
|<span data-ttu-id="b299e-127">遵循有关优化 IIS 性能的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="b299e-127">Follow best practices for optimizing IIS performance.</span></span>|<span data-ttu-id="b299e-128">请参阅["排名靠前的 10 个方面与 IIS 性能泵"](http://go.microsoft.com/fwlink/?LinkId=109107) (http://go.microsoft.com/fwlink/?LinkId=109107)。</span><span class="sxs-lookup"><span data-stu-id="b299e-128">See ["Top Ten Ways To Pump Up IIS Performance"](http://go.microsoft.com/fwlink/?LinkId=109107) (http://go.microsoft.com/fwlink/?LinkId=109107).</span></span>|  
|<span data-ttu-id="b299e-129">按照编写为 IIS 的 web 应用程序的高性能的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="b299e-129">Follow best practices for writing high performance web applications for IIS.</span></span>|<span data-ttu-id="b299e-130">请参阅["编写高性能的 10 个提示 Web 应用程序"](http://go.microsoft.com/fwlink/?LinkId=98290) (http://go.microsoft.com/fwlink/?LinkId=98290)。</span><span class="sxs-lookup"><span data-stu-id="b299e-130">See ["10 Tips for Writing High-Performance Web Applications"](http://go.microsoft.com/fwlink/?LinkId=98290) (http://go.microsoft.com/fwlink/?LinkId=98290).</span></span>|  
  
## <a name="in-this-section"></a><span data-ttu-id="b299e-131">本节内容</span><span class="sxs-lookup"><span data-stu-id="b299e-131">In This Section</span></span>  
  
-   [<span data-ttu-id="b299e-132">发布的面向 Internet 的 Web 服务和 WCF 服务</span><span class="sxs-lookup"><span data-stu-id="b299e-132">Publishing Internet-facing Web Services and WCF Services</span></span>](../technical-guides/publishing-internet-facing-web-services-and-wcf-services.md)