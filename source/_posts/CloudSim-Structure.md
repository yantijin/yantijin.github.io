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

### Basic architecture

![3](CloudSim-Structure\3.png)

* **SimJava discrete event simulation engine**: 
  * Implements the core functionalities required for higher-level simulation frameworks, creation of system components.(services, host, data center, broker, virtual machines), communication between components and management of the simulation clock.
* **GridSim**
  * 用于建模多个网格基础设施的高级软件组件，包括网络和相关的流量配置文件;
  * 基础网格组件，比如 resources, data sets, workflow traces, and information services.
* **CloudSim**
  * 拓展了Gridsim的公开的核心函数
  * 赋予虚拟云端的数据中心环境的模型和仿真提供了很好的支持，比如，虚拟机，内存和带宽的专用管理界面
  * 可以实例化和透明管理数千个系统组成的云计算基础系统架构
  * 可以配置VMs，管理应用的运行，并且可以动态监视
  * 云服务商可以研究：不同分配hosts方法的效益等
* **User Code**
  * exposes configuration related functionalities for **hosts**(number of machines, their specifications and so on), **applications**(number of tasks and their requirements), **VMs**, number of **users** and their **application types** and **broker** scheduling policies.

### Modeling the clouds

* 与云相关的核心硬件基础架构服务由**数据中心组件**在模拟器中建模，用于处理服务请求，请求是在VM中沙箱化的应用程序元素，需要在Datacenter的主机组件上分配一部分处理能力。 
* **NOTE**:VM的处理包括VM整个生命周期的一些列操作：为VM配置一个主机，VM的创建，VM的销毁和VM的移植。
* Datacenter是由一系列的的主机(host)构成，主机可以管理VMs，主机在云中代表一个物理计算节点。 Host提供了支持单核和多核节点的建模与仿真的接口
* 分配VMs到Hosts是**虚拟机配置**部分的功能： 这一部分有很多方法，从用户角度的，从系统角度的，默认的是FCFS(First Come First Service)  
* The allocation of cores to VMs is done based on a host allocation. Each host components instantiates a VM scheduler component that implements the space-shared or time shared policies for allocating cores to VMs. 

### Modeling the VM allocation

* 云计算与网格计算最大的一个不同之处就是采用了大量的虚拟化技术和工具。

* 需要考虑的因素就是：避免创建需要比主机中可用处理能力更强的处理能力的VM

* CloudSim支持VM调度两种层级的操作，一种是host level(主机层)，确定给每个VM分配多少计算能力；一种是VM level(虚拟机层)，给存储在他的execution engine的特定的task分配可用处理资源。每一个层级都包含time-shared and space-shared resource allocation policies.

  ![4](E:\GIT_repo\yantijin.github.io\source\_posts\CloudSim-Structure\4.png)

  **note**:

  * **space-shared for VMs**: only one VM can run at a given instance of time

    **time-shared for VMs**: the core is shared, the amount of processing power available to the VM is lesser than space-shared

  * **space-shared for tasks**: a VM has two cores, so it sun two at a time but the other two are queued until the completion of the earlier task units

    **time-shared for tasks**: enable the task to be scheduled at an earlier time, but significantly affecting the completion time of task units that are ahead the queue