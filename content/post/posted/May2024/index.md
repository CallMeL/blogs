---
title: "不固定记录203"
slug: "2024-08"
description: 四五六七，
date: 2024-07-23T10:33:32+02:00
image: 
math: 
license: 
comments: true
draft: true
---

## 动起来了
### 户外集体跑
### 
## 夏天诶
### 野餐
### 烟火
### 聚会
## 一日游客
### 基尔
### 柏林

## 上头追星

## 在学校
### 非常喜欢的一些课

## 持续装修
### 失效链接加跳转
因为之前给网站加了多语言，新的博文链接多了`zh-cn`的字段，所以原本发在毛象上的链接都失效了。最快的解决方法是在根目录下添加`vercel.json`文件，并添加如下跳转。更加详细的官方示例可参考[此链接](https://vercel.com/docs/projects/project-configuration#redirects)。如果不是用vercel部署的话，可以搜寻部署平台对应的文档。
```
{
  "redirects": [
    { "source": "/p/:path*/", "destination": "/zh-cn/p/:path*/", "permanent": true },
    { "source": "/index.xml", "destination": "/zh-cn/index.xml", "permanent": true }
  ]
}
```
## 看过的

愚者之夜
致銀河的不死孩童 
明亮的夜晚
迷宮飯
我開始做AV男優了
電影少女
島並黃昏
SIX
Finding Neverland
The OA 
喀耳刻
The Biggest Little Farm