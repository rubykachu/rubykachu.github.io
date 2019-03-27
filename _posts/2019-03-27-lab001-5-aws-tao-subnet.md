---
layout: post
title: 'LAB001-5: AWS - Tạo Subnet'
date: 2019-03-27 10:30:00 +0700
categories: AWS
tags: AWS LAB
author: minhtang
description: 'LAB001-5: AWS - Tạo Subnet'
permalink: /lab001-5-aws-tao-subnet
image: https://i.imgur.com/je9uyhx.png
---

* content
{:toc}
**Subnet** được hiểu là 1 sub network (mạng con ảo). Sau khi tạo 1 VPC, ta có thể thêm một hoặc nhiều subnet (mạng con) trong mỗi Availability Zone. Khi ta tạo 1 subnet, ta cần chỉ định khối CIDR cho subnet đó. Mỗi subnet phải nằm hoàn toàn trong 1 Availability Zone và không thể kéo dài tới các zone khác. Các Availability Zone là các vị trí riêng biệt được thiết kế để cách ly để tránh bị ảnh hưởng khi các zone khác gặp vấn đề.

Có thể tạo 1 hoặc nhiều subnet trên một VPC. Tuy nhiên ta sẽ bị giới hạn số VPC trên AWS




Có 2 loại subnet
- Public Subnet: là 1 subnet được định tuyến tới 1 internet gateway. 1 instance trong public subnet có thể giao tiếp với internet thông qua địa chỉ IPv4 (public IPv4 address hoặc Elastic IP address).
- Private Subnet: Ngược với Public Subnet, Private Subnet là một subnet không được định tuyến tới một internet gateway. Ta không thể truy cập vào các instance trên một Private Subnet từ internet.
**1. Tạo Public Subnet (10.0.1.0/24) ở Zone us-east-1a và tương tự cho (10.0.2.0/24) ở Zone us-east-1b**

![image](https://user-images.githubusercontent.com/27756008/54731626-ebe5fb80-4bc1-11e9-88d2-73e69d5ad0b5.png)

![image](https://user-images.githubusercontent.com/27756008/54731704-5c8d1800-4bc2-11e9-8f42-cf576f69f310.png)

![image](https://user-images.githubusercontent.com/27756008/54731887-5d727980-4bc3-11e9-840a-455126bcfc0c.png)

**2. Tạo Private Subnet (10.0.3.0/24) ở Zone us-east-1a và tương tự cho (10.0.4.0/24) ở Zone us-east-1b**

![image](https://user-images.githubusercontent.com/27756008/54731912-7418d080-4bc3-11e9-9154-132d25ef44e3.png)

![image](https://user-images.githubusercontent.com/27756008/54731920-872ba080-4bc3-11e9-9641-6ed7d1f1c539.png)
