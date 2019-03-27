---
layout: post
title: 'LAB001-11: AWS - Tạo Elastic File Systen (EFS)'
date: 2019-03-27 11:00:00 +0700
categories: AWS
tags: AWS LAB EFS
author: minhtang
description: 'LAB001-11: AWS - Tạo Elastic File System (EFS)'
permalink: /lab001-11-aws-tao-elastic-file-system
image: https://i.imgur.com/je9uyhx.png
---

* content
{:toc}
Dùng *Elastic File Systen (EFS)* mục đích để các EC2 dùng chung 1 block storage




**1. Tạo EFS**
![image](https://user-images.githubusercontent.com/27756008/54738001-f2399f00-4be4-11e9-8aff-b18e6bb61199.png)

![image](https://user-images.githubusercontent.com/27756008/54738077-4c3a6480-4be5-11e9-92a5-be0bb8a64ca0.png)
![image](https://user-images.githubusercontent.com/27756008/54738088-565c6300-4be5-11e9-8086-ebe27d019db3.png)

![image](https://user-images.githubusercontent.com/27756008/54738246-fe722c00-4be5-11e9-8d03-9751a13f8f1c.png)

Chạy lệnh mount để mount efs vào ec2
![image](https://user-images.githubusercontent.com/27756008/54738261-1053cf00-4be6-11e9-9cd8-b3f75b0b2ccf.png)

**2. Enable DNS trên VPC**
![image](https://user-images.githubusercontent.com/27756008/54738166-adface80-4be5-11e9-818f-eb24f39e1c59.png)

![image](https://user-images.githubusercontent.com/27756008/54738181-b6eba000-4be5-11e9-8868-c5c6c54211bc.png)

![image](https://user-images.githubusercontent.com/27756008/54738190-be12ae00-4be5-11e9-97f9-4d2a2a230632.png)

![image](https://user-images.githubusercontent.com/27756008/54738213-e0a4c700-4be5-11e9-8d2c-e4f4c8deeea6.png)
