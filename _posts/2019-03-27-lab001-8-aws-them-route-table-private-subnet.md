---
layout: post
title: 'LAB001-8: AWS - Thêm route table cho private subnet'
date: 2019-03-27 10:30:00 +0700
categories: AWS
tags: AWS LAB subnet route-table
author: minhtang
description: 'LAB001-8: AWS - Thêm route table cho private subnet'
permalink: /lab001-8-aws-them-route-table-cho-private-subnet
image: https://i.imgur.com/je9uyhx.png
---

* content
{:toc}
Sau khi tạo Nat Instance thì để các EC2 trong private subnet đi được internet thì ta cần update lại route table của private subnet. Ta cần phải add 1 record `0.0.0.0/0` đến con Nat Instnace



![image](https://user-images.githubusercontent.com/27756008/54733040-d83e9300-4bc9-11e9-9e69-cd54286236e4.png)


![image](https://user-images.githubusercontent.com/27756008/54733050-ec829000-4bc9-11e9-8b98-aa13f7e5aa83.png)

![image](https://user-images.githubusercontent.com/27756008/54733052-f60bf800-4bc9-11e9-9370-79f77a3f7367.png)

