《Prometheus监控技术与实践》配套资料


前言
==========

## 为何要写这本书

从互联网、移动计算到云计算、大数据、人工智能，再到虚拟现实/增强现实，近十多年来，信息技术的日新月异催生了不断涌现的互联网新业态，也推动了传统行业投身于数字化转型的创新浪潮。云计算是IT信息技术发展和服务模式创新的集中体现，是信息化发展的重大变革和必然趋势。

日益迫切的数字化转型，使得IT架构在与互联网融合中面临着海量用户和快速迭代的巨大挑战。通过云端部署开发平台进行软件全生命周期管理，能够快速构建开发、测试、运行环境，规范开发流程和降低成本，提升研发效率和创新水平，已逐渐成为软件行业新主流。伴随着基础设施代码化产生了SRE（系统可靠性工程）、DevOps（运维开发）等新型模式对软件产业产生了深远影响，更多关注客户体验。国外的Netflix、Google、微软等依靠强大的技术实力和人才储备的，从其技术架构、组织架构和企业文化等方面造就了优秀的技术理念和最佳实践。国内的华为、阿里、腾讯、百度等企业也实现了DevOps落地，并取得很好的示范效应。

在这个过程中，利用一些经验以及对服务的理解来定义一些服务质量指标（SLI）、服务质量目标（SLO）、服务质量协议（SLA）反映服务质量的重要指标。建立完善的监控体系达到长期趋势分析、关联分析、运行告警、故障分析与定位、数据可视化等能力。在IT运维中，实现“运筹帷幄之中，决胜千里之外”。

Prometheus（普罗米修斯，有时简称Prom）是Google BorgMon监控系统的开源版本，支持容器和微服务的监测和预警工具集。它提供了丰富度量指标、不影响目标系统性能设计、高度可定制的云原生监控系统。Prometheus由Go语言编写而成，采用Pull方式抓取监控信息，并提供了多维度的数据模型和灵活的查询接口。Prometheus不仅可以通过静态文件配置监控对象，还支持自动发现机制，能够通过Kubernetes、Consul、DNS等多种方式动态获取监控对象。借助Go语言的高并发特性，单机Prometheus可以采集数百个节点的监控数据，每秒可采集数百万个指标。

Prometheus已具有与监控密切关联告警等第三方集成的完整生态，成为容器和微服务监控的主流监控告警平台，受到了大量组织的欢迎。Prometheus与CNCF的Kubernetes完美协同，是DevOps工作流的关键组件，为云原生应用程序和基础设施保驾护航。

## 如何阅读本书

本书从运维（Ops）角度对Prometheus监控的各项功能进行了详细介绍，对Prometheus的系统架构、Exporter、服务发现、PromQL数据查询、告警处理、Grafana可视化等进行了深入浅出的探讨。

本书主要分3部分：第1部分为概述，包括第1\~2章。重点阐述了云计算时代监控系统的特点及其面临的挑战，Prometheus监控的基本概念、组成、部署。第2部分是Prometheus技术基础，包括第3\~8章。重点Prometheus生态系统涉及的Exporter、发现、PromQL数据查询、告警处理、Grafana可视化、pushgateway各监控组件，详细讲解了各组件的相关概念、实现原理、具体使用等。第3部分是监控综合实践，包括第9~15章。从常用的监控需求出发，分别讲解了OpenStack云计算监控、Docker容器监控、Kubernetes监控、微服务及业务监控、日志监控设计与实现，最后讲解了Prometheus在生产环境中部署的实践以及如何构建统一监控平台。

全书第1、9、10、12\~15章由陈金窗编写，第2~8章由刘政委编写，第11章由张其栋编写，最后由陈金窗、刘政委共同进行修订。

## 读者对象

本书主要读者对象包括：
	Linux系统管理员
	系统运维工程师、运维开发工程师、运维架构师
	运维监控系统工程师、监控系统软件开发（设计）人员

## 勘误和支持

因作者的水平有限，编写时间仓促，同时本书在创作过程中参考了大量的国内外技术，并结合实践经验进行了系统性梳理、总结。由于技术的发展非常迅速，书中难免会出现一些错误或者不准确的地方，恳请读者批评指正。

本书采用的Prometheus版本为当前最新的2.4.0，采用的操作系统为RHEL（CentOS）、Windows为主，对其他系统，其配置方法类似，请读者举一反三。本书对部分不重要的内容只是简略地介绍，希望能起到抛砖引玉的作用。

本书所有的代码和安装软件将放在Github中托管，地址为https://github.com/aiopstack/prometheus-book/，读者可以自行下载并使用。另外，本书的勘误也会在该链接中得到反馈。同时欢迎加入QQ群（838152818，Prometheus监控中国用户组）进行交流。

## 致谢

首先感谢Google创造性开发了BorgMon监控系统，之后马特·T·普劳德（Matt T.Proud，前Google员工）、Proud、Julius Volz共同合作，于2015年1月发布了第一个Prometheus开源版本。是他们辛勤的劳动和乐于分享，才使得Prometheus产生巨大的威力，在他们身上闪烁着开源精神的绚丽光芒。

感谢机械工业出版社的编辑们一年来始终如一的支持、积极的鼓励、耐心的帮助，并逐字审阅、校正，引导我们克服诸多困难完成全部书稿。

本书写作过程中参考了众多网友有关Prometheus的网络论坛、博客文章，每章最后都有提供一些主要的参考资料，可以作为本书内容进一步学习的参考材料。但由于参考资料众多，有些时间久远无法了解确切出处，在此对无私分享知识的网友们表示深深的谢意。

最后，感谢作者们家人的支持和鼓励，让我们时刻拥有信心与力量!

谨以此书献给我们最亲爱的家人和自己，以及众多热爱开源技术的朋友们！


本书作者
2019年7月
