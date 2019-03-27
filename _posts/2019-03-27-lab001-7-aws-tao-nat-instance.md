---
layout: post
title: 'LAB001-7: AWS - Tạo Nat Instance'
date: 2019-03-27 10:30:00 +0700
categories: AWS
tags: AWS LAB Bastion EC2 NatInstance
author: minhtang
description: 'LAB001-7: AWS - Tạo Nat Instance'
permalink: /lab001-7-aws-tao-nat-instance
image: https://i.imgur.com/je9uyhx.png
---

* content
{:toc}

**1. Tạo NatInstance, đồng thời cũng là Bastion**

Chúng ta có thể sử dụng NAT Gateway thay cho NAT Instance. Nhưng để tiết kiệm chi phí thì ta sẽ tạo NAT Instance.
Việc tạo Nat Instance giúp các EC2 trong private subnet có thể đi ra ngoài internet. Để các EC2 trong private subnet đi được internet thì Nat Instance phải nằm trong Public Subnet



![image](https://user-images.githubusercontent.com/27756008/54732768-1dfa5c00-4bc8-11e9-8dcc-c5ce5bb59f37.png)

![image](https://user-images.githubusercontent.com/27756008/54732781-35d1e000-4bc8-11e9-8076-212872982c03.png)

![image](https://user-images.githubusercontent.com/27756008/54732787-3e2a1b00-4bc8-11e9-981e-2dffa7e7fb44.png)

![image](https://user-images.githubusercontent.com/27756008/54732821-7598c780-4bc8-11e9-8509-c5632ea583dd.png)

![image](https://user-images.githubusercontent.com/27756008/54732830-80ebf300-4bc8-11e9-847f-b042d6894e25.png)

![image](https://user-images.githubusercontent.com/27756008/54732845-abd64700-4bc8-11e9-8b32-79b51cf13a60.png)

![image](https://user-images.githubusercontent.com/27756008/54732870-cb6d6f80-4bc8-11e9-9692-8e965edcaf8a.png)

![image](https://user-images.githubusercontent.com/27756008/54732881-d45e4100-4bc8-11e9-8719-28c7be12ef4d.png)

**2. Disabled Check Source/Dest**

![image](https://user-images.githubusercontent.com/27756008/54732909-0374b280-4bc9-11e9-9b86-4dc3322e6c52.png)

![image](https://user-images.githubusercontent.com/27756008/54732912-08d1fd00-4bc9-11e9-82a6-9d1caef734af.png)

![image](https://user-images.githubusercontent.com/27756008/54733012-b5ac7a00-4bc9-11e9-9e17-c8e6674bb36b.png)

Cuối cùng ta sẽ SSH vào Natinstance để kiểm tra xem đi được internet chưa

![image](https://user-images.githubusercontent.com/27756008/54732955-5e0e0e80-4bc9-11e9-93cb-6babe97b0e22.png)

Bây giờ ta sẽ quay lại phần Add Route cho Route Table Private Subnet.
