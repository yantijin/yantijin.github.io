---
title: CloudSim Structure
date: 2018-11-09 21:01:33
tags: CloudSim toolkit introduction
categories: Cloud Workflow Scheduling
---

## Basic Concepts and Terminologies

### Layered Design

![StructureofCloudPlatform](CloudSim-Structure\StructureofCloudPlatform.png)

* **User-Level Middleware**: providing PaaS capabilities

  (1) Includes the software frameworks such as Web 2.0 Interfaces 

  (2) provides the programming environments and composition tools that ease the creation, deployment, and execution of applications in Clouds 

* **Core Middleware**:

  (1) Implements the platform level services that provide runtime environment enabling Cloud computing capabilities to application services built using User-Level Middlewares 

  (2) Core services at this layer includes Dynamic SLA(Service Level-Agreement) Management, Accounting, Billing, Execution monitoring and management, and Pricing.  

* **System Level**:

  (1) Exist massive physical resources (storage servers and application servers) that power the data centers.

  (2) Servers are transparently managed by the higher level virtualization

  (3) VMs are isolated from each other.


### Federation (Inter-Networking) of Clouds

* 现有系统不支持用于动态协调不同数据中心之间的负载分解的机制和策略，以便确定用于托管应用服务的最佳位置以实现合理的服务满意度水平。

* 云服务提供商无法预测消费其服务的用户的地理分布，因此负载协调必须自动发生，并且服务的分配必须根据负载行为的变化而变化。

  ![StructureofCloudPlatform](CloudSim-Structure\2.png)

  *  **Cloud coordinator**的作用
    * (1)提供云服务：包括基础设施和平台级别的
    * (2)跟踪数据中心的负载，并且承担与其他云服务商在需求高峰期的时候进行服务的动态规划的协调
    * (3)检测应用的执行和约定的SLAs(服务等级协议)被传送
  * **Cloud Exchange(CEx)**的作用
    * bring together service providers and consumers
    * 汇总云代理的基础需求，并根据Cloud Coordinators发布的可用的资源进行评估

## CloudSim Architecture

![3](CloudSim-Structure\3.png)

* **SimJava discrete event simulation engine**: that implements the core functionalities required for higher-level simulation frameworks.
* **GridSim**
  * 用于建模多个网格基础设施的高级软件组件，包括网络和相关的流量配置文件;

