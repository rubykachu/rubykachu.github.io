---
layout: post
title: 'LAB001-13: AWS - Tạo Application Load balancing (ALB)'
date: 2019-03-27 11:00:00 +0700
categories: AWS
tags: AWS LAB
author: minhtang
description: 'LAB001-13: AWS - Tạo Application Load balancing (ALB)'
permalink: /lab001-13-aws-tao-application-load-balancing
image: https://i.imgur.com/je9uyhx.png
---

* content
{:toc}
**Application Load balancing (ALB)** là một trong những dịch vụ của **Elastic Load Balancing (ELB)**, được dùng để tự động phân phối lưu lượng truy cập đến của ứng dụng trên nhiều đích chẳng hạn như EC2





**1. Tạo target group**

![image](https://user-images.githubusercontent.com/27756008/54738500-1bf3c580-4be7-11e9-85b9-f8bf0f33d628.png)

Target Group sẽ dùng Port 80 để giao tiếp với EC2

![image](https://user-images.githubusercontent.com/27756008/54738520-2f069580-4be7-11e9-985e-d915e1df48ef.png)

**2. Tạo Load balancer**

![image](https://user-images.githubusercontent.com/27756008/54738628-a2100c00-4be7-11e9-87a6-102bf9084c06.png)

![image](https://user-images.githubusercontent.com/27756008/54738637-aa684700-4be7-11e9-8cd3-047ae94defab.png)

![image](https://user-images.githubusercontent.com/27756008/54738651-ba802680-4be7-11e9-905c-f101a7a63e3b.png)

**Chú ý: Load balancer phải nằm trên Subnet Public**

![image](https://user-images.githubusercontent.com/27756008/54738680-ccfa6000-4be7-11e9-9e16-68736b61334d.png)

Security Group phải cho phép port 80 và 443

![image](https://user-images.githubusercontent.com/27756008/54738691-d8e62200-4be7-11e9-93f3-33c980823fad.png)

Load Balancer sẽ listen port 80 từ Browser.
**Chú ý: Ý nghĩa của Port 80 ở Load Balancer khác với port trong Target Group.**
Nếu như ở trong Server EC2 listen port 443 hoặc 1 port bất kỳ nào đó thì Target Group sẽ listen trên port đó.
Còn nếu như ở bên ngoài browser gọi vào thì Load Balancer sẽ listen trên Port mà browser gọi vào. Ngoài ra ta có thể set add listener để điều hướng theo ý mà ta muốn.

![image](https://user-images.githubusercontent.com/27756008/54738699-e1d6f380-4be7-11e9-98d9-fb430ea4ce36.png)

![image](https://user-images.githubusercontent.com/27756008/54738710-e9969800-4be7-11e9-8e64-c9439c98b15e.png)

![image](https://user-images.githubusercontent.com/27756008/54738720-ee5b4c00-4be7-11e9-8698-c55ba3f785e5.png)

**3. Add listener port 443**

Ở đây ta muốn người dùng gõ domain `http://route53.xyz` thì sẽ forward sang `https://route53.xyz`

![image](https://user-images.githubusercontent.com/27756008/54738918-c0c2d280-4be8-11e9-8c52-67dfba572692.png)

![image](https://user-images.githubusercontent.com/27756008/54738977-fcf63300-4be8-11e9-89be-533cfa4bb5e8.png)

![image](https://user-images.githubusercontent.com/27756008/54738996-097a8b80-4be9-11e9-982a-7a9ba2b4bd75.png)

![image](https://user-images.githubusercontent.com/27756008/54739012-16977a80-4be9-11e9-9c40-c8213ff4f591.png)

**4. Tự động Redirect qua port 443 nếu như end user nhập port 80**

![image](https://user-images.githubusercontent.com/27756008/54745036-261fbf00-4bfb-11e9-8173-a2668af173d0.png)
