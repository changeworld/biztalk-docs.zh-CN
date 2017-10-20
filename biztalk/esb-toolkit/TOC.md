# [Microsoft BizTalk ESB 工具包](microsoft-biztalk-esb-toolkit.md)
## [安装和配置](install-and-configure-the-microsoft-biztalk-esb-toolkit.md)
## [BizTalk ESB 工具包简介](introduction-to-the-biztalk-esb-toolkit.md)
### [BizTalk ESB 工具包概述](overview-of-the-biztalk-esb-toolkit.md)
### [BizTalk ESB 工具包内容](contents-of-the-biztalk-esb-toolkit.md)
#### [ESB Web 服务](esb-web-services.md)
#### [ESB 管理门户](esb-management-portal.md)
#### [ESB 管道互操作组件](esb-pipeline-interop-components.md)
#### [异常管理框架](exception-management-framework.md)
#### [ESB 解析程序和适配器提供程序框架](esb-resolver-and-adapter-provider-framework.md)
#### [基于路线的路由和处理](itinerary-based-routing-and-processing.md)
## [BizTalk ESB 工具包入门](getting-started-with-the-biztalk-esb-toolkit.md)
### [BizTalk ESB 工具包体系结构](architecture-of-the-biztalk-esb-toolkit.md)
### [了解消息流](understanding-message-flow.md)
#### [BizTalk ESB 工具包消息生命周期](biztalk-esb-toolkit-message-life-cycle.md)
#### [基于路线的路由](itinerary-based-routing.md)
#### [详细的处理指令](processing-instructions-in-detail.md)
### [典型用例](typical-use-cases.md)
#### [终结点的点到点解决方案和转换需求](point-to-point-resolution-of-endpoints-and-transformation-requirements.md)
#### [终结点的请求 - 响应解决方案和转换需求](request-response-resolution-of-endpoints-and-transformation-requirements.md)
#### [转换但不保存到 BizTalk Message Box 数据库](transformation-without-persisting-to-the-biztalk-message-box-database.md)
#### [使用路线定义路由和消息转换服务调用](define-routing-and-message-transformation-service-invocations-using-itineraries.md)
#### [使用路线通过多业务流程定义路由和消息转换](define-routing-and-message-transformation-through-multiple-orchestrations.md)
#### [使用路线定义自定义业务流程服务执行](defining-custom-orchestration-service-execution-using-itineraries.md)
#### [将消息转换和路由到磁盘文件夹、队列或 FTP 文件夹](transforming-and-routing-a-message-to-disk-folder-queue-or-ftp-folder.md)
#### [为修复和重新提交收集异常和路由消息](collecting-exceptions-and-routing-messages-for-repair-and-resubmit.md)
#### [使用 ESB 异常处理器收集异常并保留有效负载](collect-exceptions-and-persist-the-payload-using-the-esb-exception-processor.md)
#### [使用 ESB 管理门户修复和重新提交消息](repairing-and-resubmitting-messages-using-the-esb-management-portal.md)
#### [路由经过业务流程时保留 JMS 标头](preserving-jms-headers-when-routing-through-an-orchestration.md)
#### [使用自定义处理程序处理外部提交的异常](handling-externally-submitted-exceptions-using-a-custom-handler.md)
#### [添加和删除 XML 消息文档中的命名空间](adding-and-removing-namespaces-in-an-xml-message-document.md)
#### [为多个 Web 服务调用实现“分散-集中”模式](implementing-the-scatter-gather-pattern-for-multiple-web-service-invocations.md)
#### [将消息转换和路由到多个终结点](transforming-and-routing-a-message-to-multiple-endpoints.md)
## [主要方案和开发任务](key-scenarios-and-development-tasks.md)
### [使用基于路线的路由](using-itinerary-based-routing.md)
#### [ESB 路线管理](esb-itinerary-management.md)
#### [接入点和接出点](on-ramps-and-off-ramps.md)
#### [在消息传递和业务流程路线服务之间进行选择](choosing-between-messaging-and-orchestration-itinerary-services.md)
#### [使用管道组件选择现有路线](using-a-pipeline-component-to-select-an-existing-itinerary.md)
#### [使用管道组件读取路线](using-a-pipeline-component-to-read-an-itinerary.md)
##### [ESB 路线架构](the-esb-itinerary-schema.md)
#### [使用管道组件缓存“要求-响应”路线](using-a-pipeline-component-to-cache-an-itinerary-for-solicit-response.md)
#### [创建路线订阅方](creating-itinerary-subscribers.md)
##### [将发送端口用作路线服务订阅方](using-a-send-port-as-an-itinerary-service-subscriber.md)
##### [将业务流程用作路线服务订阅方](using-an-orchestration-as-an-itinerary-service-subscriber.md)
#### [执行路线服务](executing-an-itinerary-service.md)
#### [基于路线的路由项目](itinerary-based-routing-artifacts.md)
### [使用动态解析和路由](using-dynamic-resolution-and-routing.md)
#### [动态解析和路由概述](dynamic-resolution-and-routing-overview.md)
#### [解析程序和适配器提供程序框架](the-resolver-and-adapter-provider-framework.md)
#### [在代码中使用解析程序组件](using-the-resolver-components-in-your-code.md)
#### [使用动态路由](using-dynamic-routing.md)
### [使用动态转换](using-dynamic-transformation.md)
### [使用 ESB 异常管理](using-esb-exception-management.md)
#### [ESB 异常管理框架设计](design-of-the-esb-exception-management-framework.md)
#### [异常管理框架组件](the-components-of-the-exception-management-framework.md)
##### [ESB 故障业务流行异常路由机制](the-esb-failed-orchestration-exception-routing-mechanism.md)
##### [ESB 故障处理器管道](the-esb-fault-processor-pipeline.md)
##### [ESB 管理门户和故障消息查看器](the-esb-management-portal-and-fault-message-viewer.md)
##### [InfoPath 消息模板](the-infopath-message-template.md)
#### [使用异常管理框架](using-the-exception-management-framework.md)
##### [ESB 异常 API 成员](the-esb-exception-api-members.md)
##### [创建并发布故障消息](creating-and-publishing-fault-messages.md)
##### [订阅消息和提取消息](subscribing-to-and-extracting-messages.md)
##### [方案解决方案步骤](scenario-solution-steps.md)
#### [创建自定义异常处理程序](creating-custom-exception-handlers.md)
### [使用 BizTalk ESB 工具包 Web 服务](using-the-biztalk-esb-toolkit-web-services.md)
#### [路线接入点 Web 服务](the-itinerary-on-ramp-web-services.md)
#### [解析程序 Web 服务](the-resolver-web-service.md)
#### [转换 Web 服务](the-transformation-web-service.md)
#### [异常处理 Web 服务](the-exception-handling-web-service.md)
#### [BizTalk 操作 Web 服务](the-biztalk-operations-web-service.md)
### [使用管道支持组件](using-the-pipeline-support-components.md)
#### [ESB 路线选择器组件](the-esb-itinerary-selector-component.md)
#### [ESB 路线组件](the-esb-itinerary-component.md)
#### [ESB 路线转发器组件](the-esb-itinerary-forwarder-component.md)
#### [ESB JMS 编码器和解码器组件](the-esb-jms-encoder-and-decoder-components.md)
#### [ESB 添加命名空间和删除命名空间组件](the-esb-add-namespace-and-remove-namespace-components.md)
#### [ESB 调度程序组件](the-esb-dispatcher-component.md)
#### [ESB 调度程序反汇编组件](the-esb-dispatcher-disassemble-component.md)
### [使用 Helper 类](using-the-helper-classes.md)
#### [MapHelper 类](the-maphelper-class.md)
#### [Resolver 类](the-resolver-class.md)
#### [ResolverDictionary 类](the-resolverdictionary-class.md)
#### [Resolver Manager (ResolverMgr) 类](the-resolver-manager-resolvermgr-class.md)
### [使用 BizTalk ESB 工具包实用工具](using-the-biztalk-esb-toolkit-utilities.md)
## [使用路线设计器创建路线](creating-itineraries-using-itinerary-designer.md)
### [关于路线](about-itineraries.md)
### [使用路线设计器](working-in-itinerary-designer.md)
### [在路线中实现设计模式](implementing-design-patterns-in-itineraries.md)
#### [消息路由模式](message-routing-patterns.md)
#### [消息转换模式](message-transformation-patterns.md)
#### [服务介质模式](service-mediation-patterns.md)
#### [服务管理模式](service-management-patterns.md)
### [开发活动](development-activities.md)
#### [开发活动的先决条件](prerequisites-for-the-development-activities.md)
#### [如何：使用业务规则策略动态路由基于消息上下文的消息](dynamically-route-messages-based-on-message-context-using-business-rules-policy.md)
#### [如何：使用路线传送名单将单条消息路由至多个收件人](route-a-single-message-to-multiple-recipients-using-an-itinerary-routing-slip.md)
#### [如何：转换消息并使用路线传送名单将生成的消息路由至文件位置](transform-message-and-route-the-message-to-a-location-using-itinerary-routing.md)
#### [如何：转换消息并使用“请求-响应”消息交换模式将其路由至服务终结点](transform-message-and-route-to-service-endpoint-using-request-response-message.md)
#### [如何：使用业务规则策略选择路线](how-to-select-an-itinerary-using-a-business-rules-policy.md)
#### [如何：拆分交换并使用不同的路线将生成的消息路由至多个文件位置](split-an-interchange-and-route-messages-to-multiple-locations-using-itineraries.md)
#### [如何：将文本文档转换为 XML 并使用路线传送名单将其路由至文件位置](convert-text-document-to-xml-and-route-to-location-using-itinerary-routing-slip.md)
#### [如何：创建路线以便使用 LDAP 查询动态将消息路由至电子邮件地址](create-itinerary-to-dynamically-route-message-to-an-email-address-using-ldap.md)
#### [如何：使用已知消息类型的业务规则策略实现基于内容的路由](apply-content-based-routing-using-business-rules-policy-for-known-message-type.md)
#### [如何：使用 ESB 接入点验证消息](how-to-validate-a-message-using-an-esb-on-ramp.md)
#### [如何：将服务发布到 UDDI 3.0 注册表](how-to-publish-a-service-to-the-uddi-3-0-registry.md)
#### [如何：使用 UDDI 类别搜索解析服务终结点](how-to-resolve-a-service-endpoint-using-a-uddi-category-search.md)
#### [如何：使用 UDDI 绑定密钥搜索解析服务终结点](how-to-resolve-a-service-endpoint-using-a-uddi-binding-key-search.md)
#### [如何：在 ESB 路线服务中启用 BAM 跟踪](how-to-enable-bam-tracking-in-an-esb-itinerary-service.md)
#### [如何：使用消息上下文属性实现基于内容的路由](how-to-implement-content-based-routing-using-message-context-properties.md)
## [BizTalk ESB 工具包示例应用程序](biztalk-esb-toolkit-sample-applications.md)
### [安装异常管理示例](installing-the-exception-management-samples.md)
#### [使用安装脚本安装异常管理示例](installing-the-exception-management-samples-using-install-scripts.md)
#### [异常管理示例安装的程序集和项目](assemblies-and-artifacts-installed-by-the-exception-management-samples.md)
### [运行修复和重新提交自定义异常处理程序示例](running-the-repair-and-resubmit-custom-exception-handler-sample.md)
### [运行消息保留自定义异常处理程序示例](running-the-message-persisting-custom-exception-handler-sample.md)
### [运行 BizTalk 故障消息路由 ESB 处理示例](running-the-biztalk-failed-message-routing-esb-processing-sample.md)
### [安装和运行路线接入点示例](installing-and-running-the-itinerary-on-ramp-sample.md)
#### [安装路线接入点示例](installing-the-itinerary-on-ramp-sample.md)
##### [使用安装脚本安装路线接入点示例](install-the-itinerary-on-ramp-sample-using-the-install-scripts.md)
##### [路线接入点示例安装的程序集和项目](assemblies-and-artifacts-installed-by-the-itinerary-on-ramp-sample.md)
#### [运行路线接入点示例](running-the-itinerary-on-ramp-sample.md)
##### [运行预定义路线接入点示例](run-a-predefined-itinerary-on-ramp-sample.md)
##### [示例路线方案](the-sample-itinerary-scenarios.md)
##### [执行自定义路线方案](execute-a-custom-itinerary-scenario.md)
##### [路线接入点示例工作原理](how-the-itinerary-on-ramp-sample-works.md)
### [安装和运行 JMS MQRFH2 组件示例](installing-and-running-the-jms-mqrfh2-component-sample.md)
#### [安装 JMS MQRFH2 组件示例](installing-the-jms-mqrfh2-component-sample.md)
##### [使用安装脚本安装 JMS MQRFH2 示例](install-the-jms-mqrfh2-sample-using-the-install-scripts.md)
##### [JMS MQRFH2 组件示例安装的程序集和项目](assemblies-and-artifacts-installed-by-the-jms-mqrfh2-component-sample.md)
##### [测试 JMS MQRFH2 示例安装](test-the-jms-mqrfh2-sample-installation.md)
#### [JMS MQRFH2 示例依赖关系和强密钥名称定义](jms-mqrfh2-sample-dependencies-and-strong-key-name-definition.md)
#### [运行 JMS MQRFH2 组件示例](running-the-jms-mqrfh2-component-sample.md)
##### [运行 JMS MQRFH2 Header 保留示例](running-the-jms-mqrfh2-header-preservation-sample.md)
##### [从业务流程运行 Header 属性示例](running-the-header-property-access-from-an-orchestration-sample.md)
##### [运行大容量加载基于内容的路由示例](running-the-bulk-load-content-based-routing-sample.md)
### [安装和运行命名空间组件示例](installing-and-running-the-namespace-component-sample.md)
#### [安装命名空间组件示例](installing-the-namespace-component-sample.md)
##### [使用安装脚本安装命名空间组件示例](install-the-namespace-component-sample-using-the-install-scripts.md)
##### [命名空间组件安装的程序集和项目示例](assemblies-and-artifacts-installed-by-the-namespace-component-sample.md)
#### [运行命名空间组件示例](running-the-namespace-component-sample.md)
##### [运行命名空间组件测试](running-the-namespace-component-tests.md)
##### [添加命名空间示例工作原理](how-the-add-namespace-sample-works.md)
##### [删除命名空间示例工作原理](how-the-remove-namespace-sample-works.md)
### [安装和运行转换服务示例](installing-and-running-the-transformation-service-sample.md)
#### [安装转换服务示例](installing-the-transformation-service-sample.md)
##### [使用安装脚本安装转换服务示例](install-the-transformation-service-sample-using-the-install-scripts.md)
##### [转换服务示例安装的程序集和项目](assemblies-and-artifacts-installed-by-the-transformation-service-sample.md)
#### [运行转换服务示例](running-the-transformation-service-sample.md)
### [安装和运行动态解析示例](installing-and-running-the-dynamic-resolution-sample.md)
#### [安装动态解析示例](installing-the-dynamic-resolution-sample.md)
##### [使用安装脚本安装动态解析示例](install-the-dynamic-resolution-sample-using-the-install-scripts.md)
##### [动态解析示例安装的程序集和项目](assemblies-and-artifacts-installed-by-the-dynamic-resolution-sample.md)
#### [运行动态解析示例](running-the-dynamic-resolution-sample.md)
##### [动态解析示例的单向消息传送方案](one-way-messaging-scenarios-for-the-dynamic-resolution-sample.md)
##### [动态解析示例的双向消息传送方案](two-way-messaging-scenarios-for-the-dynamic-resolution-sample.md)
##### [动态解析示例工作原理](how-the-dynamic-resolution-sample-works.md)
### [安装和运行 BizTalk 操作示例](installing-and-running-the-biztalk-operations-sample.md)
#### [安装 BizTalk 操作示例](installing-the-biztalk-operations-sample.md)
#### [运行 BizTalk 操作示例](running-the-biztalk-operations-sample.md)
### [安装和运行解析程序服务示例](installing-and-running-the-resolver-service-sample.md)
#### [安装解析程序服务示例](installing-the-resolver-service-sample.md)
#### [运行解析程序服务示例](running-the-resolver-service-sample.md)
#### [解析程序服务示例工作原理](how-the-resolver-service-sample-works.md)
### [安装和运行“分散-集中”示例](installing-and-running-the-scatter-gather-sample.md)
#### [安装“分散-集中”示例](installing-the-scatter-gather-sample.md)
#### [“分散-集中”示例安装的程序集和项目](assemblies-and-artifacts-installed-by-the-scatter-gather-sample.md)
#### [运行“分散-集中”示例](running-the-scatter-gather-sample.md)
#### [工作原理](how-the-scatter-gather-sample-works.md)
### [安装和运行 SQL 适配器示例](installing-and-running-the-sql-adapter-sample.md)
#### [安装 SQL 适配器示例](installing-the-sql-adapter-sample.md)
#### [SQL 适配器示例安装的程序集和项目](assemblies-and-artifacts-installed-by-the-sql-adapter-sample.md)
#### [运行 SQL 适配器示例](running-the-sql-adapter-sample.md)
#### [SQL 适配器示例工作原理](how-the-sql-adapter-sample-works.md)
### [安装和运行消息充实示例](installing-and-running-the-message-enrichment-sample.md)
#### [安装消息充实示例](installing-the-message-enrichment-sample.md)
#### [消息充实示例安装的程序集和项目](assemblies-and-artifacts-installed-by-the-message-enrichment-sample.md)
#### [运行消息充实示例](running-the-message-enrichment-sample.md)
#### [消息充实示例工作原理](how-the-message-enrichment-sample-works.md)
### [安装和运行多个 Web 服务示例](installing-and-running-the-multiple-web-services-sample.md)
#### [安装多个 Web 服务示例](installing-the-multiple-web-services-sample.md)
#### [多个 Web 服务示例安装的程序集和项目](assemblies-and-artifacts-installed-by-the-multiple-web-services-sample.md)
#### [运行多个 Web 服务示例](running-the-multiple-web-services-sample.md)
#### [多个 Web 服务示例工作原理](how-the-multiple-web-services-sample-works.md)
#### [多个 Web 服务路线示例](the-sample-multiple-web-services-itineraries.md)
### [安装和运行设计器扩展性示例](installing-and-running-the-designer-extensibility-sample.md)
#### [安装设计器扩展性示例](installing-the-designer-extensibility-sample.md)
#### [运行设计器扩展性示例](running-the-designer-extensibility-sample.md)
#### [设计器扩展性示例工作原理](how-the-designer-extensibility-sample-works.md)
### [运行异常处理服务示例](running-the-exception-handling-service-sample.md)
#### [异常处理服务示例工作原理](how-the-exception-handling-service-sample-works.md)
## [修改和扩展 BizTalk ESB 工具包](modifying-and-extending-the-biztalk-esb-toolkit.md)
### [扩展解析程序和适配器提供程序框架](extending-the-resolver-and-adapter-provider-framework.md)
#### [创建自定义解析程序](creating-a-custom-resolver.md)
#### [使用 Unity 容器创建自定义解析程序](creating-a-custom-resolver-with-a-unity-container.md)
#### [创建自定义适配器提供程序](creating-a-custom-adapter-provider.md)
### [创建自定义路线服务](creating-a-custom-itinerary-service.md)
#### [使用 BizTalk 业务流程创建自定义路线服务](creating-a-custom-itinerary-service-using-a-biztalk-orchestration.md)
#### [创建自定义路线消息传递服务](creating-a-custom-itinerary-messaging-service.md)
### [扩展路线设计器](extending-the-itinerary-designer.md)
## [BizTalk ESB 工具包管理](administration-with-the-biztalk-esb-toolkit.md)
### [使用 ESB 管理门户进行管理](administration-using-the-esb-management-portal.md)
#### [使用异常和故障消息](working-with-exceptions-and-fault-messages.md)
##### [列出、搜索和排序故障消息](listing-searching-and-sorting-fault-messages.md)
##### [查看和下载原始消息](viewing-and-downloading-the-original-messages.md)
##### [修复和重新提交消息](repairing-and-resubmitting-messages.md)
###### [修复和重新提交消息](repairing-and-resubmitting-a-message.md)
###### [重新提交说明和限制](resubmission-notes-and-restrictions.md)
###### [重新提交问题疑难解答](troubleshooting-resubmission-issues.md)
#### [配置警报、通知和订阅](configuring-alerts-notifications-and-subscriptions.md)
##### [创建、查看和删除故障消息警报](creating-viewing-and-deleting-fault-message-alerts.md)
##### [订阅警报](subscribing-to-alerts.md)
##### [配置警报队列选项和通知](configuring-alert-queue-options-and-notifications.md)
#### [查看和管理审核和历史记录](viewing-and-managing-auditing-and-history.md)
##### [配置和查看审核日志](configuring-and-viewing-audit-logs.md)
##### [查看历史记录信息](viewing-history-information.md)
#### [使用图表和报表分析故障趋势](analyzing-fault-trends-using-charts-and-reports.md)
##### [应用程序或服务故障](faults-by-application-or-service.md)
##### [应用程序或服务警报](alerts-by-application-or-service.md)
##### [应用程序或服务故障错误类型](fault-error-types-by-application-or-service.md)
##### [应用程序或服务超时故障](faults-over-time-by-application-or-service.md)
##### [应用程序或服务超时重新提交](resubmissions-over-time-by-application-or-service.md)
##### [应用程序或服务超时订阅](subscriptions-over-time-by-application-or-service.md)
#### [查看和发布 UDDI 注册](viewing-and-publishing-uddi-registrations.md)
##### [发布 BizTalk 终结点](publishing-biztalk-endpoints.md)
##### [自动登记和审核流程](the-auto-enlist-and-approval-process.md)
##### [从 BizTalk Server 管理控制台发布](publishing-from-the-biztalk-server-administration-console.md)
### [ESB 管理门户功能参考](esb-management-portal-feature-reference.md)
#### [门户主页](portal-home-page.md)
#### [“门户故障”页](portal-faults-page.md)
#### [门户故障消息查看器](portal-fault-message-viewer.md)
##### [故障详细信息视图](fault-details-view.md)
##### [消息详细信息视图](message-details-view.md)
#### [“门户警报”页](portal-alerts-page.md)
##### [“添加警报”页](add-alert-page.md)
##### [“警报查看器”页](alert-viewer-page.md)
##### [“添加警报订阅”和“编辑订阅”页](add-alert-subscription-and-edit-subscription-pages.md)
#### [“门户报表”页](portal-reports-page.md)
#### [“门户注册表”页](portal-registry-pages.md)
##### [“新建注册表项”页](new-registry-entry-page.md)
##### [“管理挂起的请求”页](manage-pending-requests-page.md)
##### [“注册表详细信息”页](registry-details-page.md)
#### [“门户管理”页](portal-admin-pages.md)
##### [“审核日志”页](audit-log-page.md)
##### [“故障设置”页](fault-settings-page.md)
##### [管理警报（管理视图）](manage-alerts-administration-view.md)
##### [“注册表设置”页](registry-settings-page.md)
#### [门户中“我的设置”页](portal-my-settings-page.md)
## [SOA 管理集成](soa-governance-integration.md)
### [SOA BizTalk 管理点](soa-biztalk-management-point.md)
#### [SOA BizTalk 管理点概述](overview-of-the-soa-biztalk-management-point.md)
#### [BizTalk Server 集成](biztalk-server-integration1.md)
#### [监视策略和使用情况信息](monitoring-policies-and-usage-information.md)
### [AmberPoint BizTalk Nano 代理](amberpoint-biztalk-nano-agent.md)
#### [服务网络管理](service-network-management.md)
#### [服务级别管理](service-level-management.md)
#### [端到端事务跟踪](end-to-end-transaction-tracking.md)
#### [BizTalk Server 集成](biztalk-server-integration2.md)
## [BizTalk ESB 工具包疑难解答](troubleshooting-the-biztalk-esb-toolkit.md)