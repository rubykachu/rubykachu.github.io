---
layout: post
title: 'LAB001-16: AWS - Hạn chế quyền truy cập website'
date: 2019-03-27 11:00:00 +0700
categories: AWS
tags: AWS LAB
author: minhtang
description: 'LAB001-16: AWS - Hạn chế quyền truy cập website'
permalink: /lab001-16-aws-truy-cap-website
image: https://i.imgur.com/je9uyhx.png
---

* content
{:toc}
Việc giới hạn quyền truy cập là rất cần thiết trong việc dựng website. Cụ thể ở đây ta sẽ giới hạn người dùng truy cập vào trang admin. Nếu như ai đó truy cập vào trang admin thì sẽ hiện lỗi 503





![image](https://user-images.githubusercontent.com/27756008/54742822-fd94c680-4bf4-11e9-89cb-feba449dfa8a.png)

![image](https://user-images.githubusercontent.com/27756008/54742881-29b04780-4bf5-11e9-9455-c4a3f46326a8.png)

Vào Route53, tạo record có subdomain `admin.route53.xyz`

![image](https://user-images.githubusercontent.com/27756008/54743066-b78c3280-4bf5-11e9-8173-21ef51ff90ab.png)

Sau khi config xong thì chờ vài phút để update record.

Tiến hành truy cập vào website `admin.route53.xyz`
![image](https://user-images.githubusercontent.com/27756008/54797099-675cb100-4c85-11e9-87be-3e02aa4973e8.png)
