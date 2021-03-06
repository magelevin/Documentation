
---
title: 产品简介
description: 
platform: All Platforms
updatedAt: Thu Oct 22 2020 02:34:37 GMT+0800 (CST)
---
# 产品简介
在你使用 Agora 实时音视频服务时，你可以使用金山智能语音审核对音频内容进行多样化场景检测，帮助你对内容进行管控，规避内容违规风险。

## 应用场景

娱乐直播平台的用户数日益增长，用户传播的内容可能存在各种不可控的风险因素，例如色情、暴恐和涉政等。随着政府监管的日趋严格，娱乐直播平台为了对内容进行管控，需要投入大量人力进行内容审核。金山智能语音审核可对音频内容进行有效的判别和筛选，大大降低人力投入。

## 技术架构

当你调用金山智能语音审核 RESTful API 发起审核时，审核服务器会获取频道内的音频流并进行审核，然后将审核结果以 HTTP 请求的形式发送到你指定的服务器地址。

![](https://web-cdn.agora.io/docs-files/1603178506290)

## 功能描述

金山智能语音审核采用自研的降噪技术，结合丰富的特征数据与文本特征分析，准确识别违规音频。 

- 基于海量音频训练，实现智能音频转文本语义分析，对音频中的涉政、涉黄、辱骂、灌水、广告等内容进行识别。
- 基于多种类色情音频的数据训练，通过声纹识别，可精准识别音频中的娇喘内容。

## 产品特性

金山智能语音审核主要有以下特性：

| <span style="white-space:nowrap;">&emsp;&emsp;特性&emsp;&emsp;</span>     | 描述                                                         |
| :-------: | :----------------------------------------------------------- |
| 实时审核 | 采用 RTMP 协议实时拉取频道内的音频流。                       |
| 高准确率 | 根据不同内容特点，提供定制化算法模型，内容理解标签体系丰富。基于海量训练数据，确保识别的高准确率。 |
| 简单易用 | 和 Agora 的实时音视频服务无缝对接，通过 4 个 RESTful API 调用就可以开始、结束和查询审核。 |
| 全球覆盖 | 全球分布式集群部署，可根据业务需要重点覆盖某区域，提供高可用服务。 |

## 计费

在使用金山智能语音审核之前，你需要在 [Agora 控制台](https://console.agora.io/)购买套餐包。套餐包计费标准见[计费说明](../../cn/null/billing_kingsoft_audio.md)。

## 相关文档和示例代码

- [快速开始](../../cn/null/quickstart_kingsoft_audio.md)展示如何通过 RESTful API 对频道内的音频进行实时审核。
- [金山语音智能审核 RESTful API](../../cn/Interactive%20Broadcast/restful_api_kingsoft_audio.md) 展示了使用金山智能语音审核的过程中，你可以调用的 RESTful API 及其功能。
