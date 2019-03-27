---
layout: post
title: 'LAB001: AWS - Yêu cầu bài tập'
date: 2019-03-27 09:00:00 +0700
categories: AWS
tags: AWS
author: minhtang
description: Yêu cầu bài tập aws - LAB001
permalink: /lab001-yeu-cau-bai-tap-aws
image: https://i.imgur.com/je9uyhx.png
---

* content
{:toc}

![LAB001](https://i.imgur.com/iODHrKE.jpg)
Hãy tạo hệ thống aws như sau:
- 1 VPC.
- 2 subnet public, 2 subnet private, 2 subnet datastore (private) Chia đều 2 zone.
- Làm `t2.micro` làm NAT instance/vừa làm bastion. Sử dụng IP public động nhưng tự cập nhập IP tới record route53 mỗi khi stop/start. Tức dùng domain để connect tới bastion mà không sử dụng IP.




- Autoscaling hosting web server: `<name>.asiantech.vn` => Welcome to <Private IP>. Các instance tạo ra ở *private subnet*. Tạo target tracking để tăng và giảm size theo CPU.
- Có *Application* loadbalancer.
- Tự động redirect qua https://<name>.asiantech.vn (Màu xanh).
- Gõ `abc.<name>.asiatech.vn` cũng vào được website và tự tự chuyển https cũng phải màu xanh.
- Nếu gõ `admin.<name>.asiantech.vn` => Hiện lỗi *403*.
- *Tạo 1 autoscaling khác tạo instance ở Public subnet. Domain `dns.<name>.asiantech.vn` => Loadbalancing bằng DNS có healthcheck.*. Test xem khi tắt 1 instance thì thế nào nhé.
- Tự động gắn EFS để share file => Mount vào thư mục `/efs`. Tạo 1 file trên EFS từ instance thứ nhất, kiểm tra xem instance thứ 2 có xuất hiện hay ko?
- Tạo RDS Postgres: Kết nối tạo DB từ *bastion server*. RDS ở *datastore subnet*. Tạo 1 replicate ở zone khác. bật tính năng encryption sau khi đã tạo DB.
- Hoàn thành các ý xong thì tạo một Network Loadbalancer và thực hiện lại toàn bộ xem có được ko?
