---
sidebar_position: 1
title: 概览
---

# LLMOS 概述
LLMOS 是一款开源的 AI 基础设施管理软件，专为加速 AI 应用开发并简化大型语言模型（LLM）的管理而设计。 它支持部署在公有云或私有的 AI 工作站和 GPU 服务器上。
通过LLMOS，您可以轻松部署、扩展并运行机器学习工作流，同时减少与AI开发和运维相关的复杂性。

<iframe width="99%" height="540" src="//player.bilibili.com/player.html?isOutside=true&aid=113860992309374&bvid=BV13CwWeUEvV&cid=25746675759&p=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>

## LLMOS 架构
下图展示了 LLMOS 的高级架构：

![LLMOS 架构](/img/docs/llmos-arch.svg)

- **管理节点**: 管理节点可以是运行在云端或本地的机器，主要负责运行 LLMOS 系统组件以及经过我们优化的 Kubernetes 集群。
- **工作节点**: 工作节点主要负责运行用户的工作负载和必要的节点组件（例如网络插件，节点监控等）。
- **LLMOS-Operator**: LLMOS-Operator 负责管理 LLMOS 平台的生命周期及其系统组件，包括 LLMOS API-Server、LLMOS-Controller 以及其他系统附加组件。
- **LLMOS-Controller**: LLMOS-Controller 主要负责大语言模型、Notebook、机器学习集群、以及其他任务的生命周期管理和配置参数。
- **Redis**: 一个用于存储 LLMOS 高可用配置和 API 聊天等信息的键值存储系统。
- **工作负载**: 工作负载是运行在 LLMOS 基础设施上的计算任务，需要请求不同的资源（例如 CPU、GPU、内存和存储卷等）。

:::note
服务器节点也可作为工作节点，但优先为系统组件分配资源。
:::

## 主要特性
- **[简单的安装](./quickstart)**：支持 x86_64 和 ARM64 架构、简单安装，提供即开即用的用户体验。
- **[GPU Stack 管理](./user_guide/gpu_management/enable-gpu-stack):** 提供虚拟 GPU (vGPU) 和多加速器支持，以提升 GPU 资源利用率和操作灵活性。
- **[机器学习集群](./user_guide/ml_clusters)**：支持分布式计算，具有并行处理能力，并包含领先的 AI 库，提升机器学习工作流的性能，尤其适用于大规模模型调优和数据集处理等任务。
- **[无缝的 Notebook 集成](./user_guide/notebooks.md)**：集成了流行的Notebook环境，如 **Jupyter**、**VSCode** 和 **RStudio**，让数据科学家和开发者无需复杂配置即可在熟悉的工具中高效工作。
- **[ModelService](./user_guide/modelservice.md) 用于 LLM 服务：** 提供 **OpenAI 兼容 API**，轻松从 [HuggingFace](https://huggingface.co/models)、[ModelScope](https://modelscope.cn/models) 或本地路径部署 LLM 服务。
- **[监控与告警](./user_guide/monitoring/enable-monitoring)：** 内置集成 Prometheus Operator，轻松了解集群和 GPU 指标，提供可视化的 Grafana 仪表板、Prometheus 规则、告警信息等。
- **[存储管理](./user_guide/storage/system-storage)**：提供高性能、高冗余的内置分布式存储，适用于 AI 和 LLM 应用的需求，具备强大的可扩展块存储和文件系统存储。
- **[用户](./user_and_auth/user)和[RBAC 管理](./user_and_auth/role-template)**：通过基于角色的访问控制（RBAC）和角色模板简化用户管理，确保资源分配的安全与效率。
- **针对边缘和分支部署进行了优化**：支持私有部署，优化了资源使用，使模型和工作负载能够在边缘和分支网络中运行，并支持横向扩展以满足未来的业务需求。

## 使用场景
- **AI 研究与开发**：简化 LLM 和 AI 基础设施管理，使研究人员能够专注于创新而非操作复杂性。
- **企业 AI 解决方案**：通过可扩展的基础设施简化 AI 应用的部署，使管理模型、存储和资源跨多个团队变得更容易。
- **数据科学工作流**：通过Notebook集成和强大的集群计算功能，LLMOS 非常适合需要大规模运行复杂实验的数据科学家。
- **AI 驱动的产品**：从聊天机器人到自动化内容生成，LLMOS 简化了部署 LLM 驱动产品的流程，使其能够为数百万用户提供服务，并支持横向扩展。

## 下一步

要开始使用 LLMOS，请参考[快速开始](./quickstart)指南。
