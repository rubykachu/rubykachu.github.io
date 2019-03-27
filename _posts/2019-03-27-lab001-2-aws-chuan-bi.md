---
layout: post
title: 'LAB001-2: AWS - Lên ý tưởng giải quyết bài tập'
date: 2019-03-27 09:30:00 +0700
categories: AWS
tags: AWS
author: minhtang
description: 'LAB001-2: AWS - Lên ý tưởng giải quyết bài tập'
permalink: /lab001-2-aws-len-y-tuong-giai-quyet-bai-tap
image: https://i.imgur.com/je9uyhx.png
---

* content
{:toc}
![LAB001](https://i.imgur.com/T0RgBGN.jpg)
1. Tạo VPC và Internet gateway: Với subnet 10.0.0.0/16
2. Tạo Security Group:
	- 2.1. SG-Internet: Gồm các port ssh, http, https, icmp.
	- 2.2. SG-Private: Gồm các port trên (hoặc gán ID của SG trên, để các EC2 follow trong SG Internet có thể nói chuyện với EC2 trong group Private) và port NFS để sử dụng Elastic File System




3. Tạo 4 subnets ( 2 public - 2private) chia đều cho 2 zones: Với subnet 10.0.0.0/24
	- 3.1. Subnet Public có Route table: Add record 0.0.0.0/0 -> Internet gateway
	- 3.2. Subnet Private có Route table: Add record 0.0.0.0/0 -> NatInstance
4. Add Role Access Route 53 cho IAM user: Để có quyền update đến Route53
5. Tạo NatInstance, con này cũng dùng để làm bastion. Đặt ở subnet Public. Disabled check Source/Dest
	- Sau khi Instance được tạo ra thì login vào viết Script để tự động update IP đến Route53. Mục đích để SSH bằng Domain và IP tự update đến Route53.
6. Tạo Elastic File System (EFS)
7. Tạo Certificate Manager (SSL)
	- Sau khi tạo thì Public đến Route53. Chờ Status chuyển từ Pending sang Issued
8. Tạo Load Balancing
	- 8.1. Tạo Group Load Balancer: Group sẽ nói chuyện với EC2 thông qua port mà ta cấu hình.
	- 8.2. Tạo Application Load Balancer: Browser sẽ nói chuyện với ALB thông qua port mà ta cấu hình.
9. Tạo AutoScaling
	- 9.1. Launch Configuration: Tạo 1 template cấu hình cho EC2 sẽ được tạo ra
	- 9.2. Tạo Meta User để khi EC2 được launch thì sẽ tự động chạy các script bên dưới
	```bash
	#!/bin/bash
	sudo su
	yum update -y
	yum install -y httpd amazon-efs-utils
	service httpd start
	chkconfig httpd on
	mkdir efs
	mount -t efs <<<ID_EFS>>>:/ efs
	echo "Welcome to $(curl http://169.254.169.254/latest/meta-data/local-ipv4)" > /var/www/html/index.html
	```
	- 9.3.  Auto Scaling Group: Nhớ chọn Load balacing
