---
layout: post
title: 'LAB001-9: AWS - Cấp quyền cho phép chỉnh sửa Route53'
date: 2019-03-27 10:30:00 +0700
categories: AWS
tags: AWS LAB
author: minhtang
description: 'LAB001-9: AWS - Cấp quyền cho phép chỉnh sửa Route53'
permalink: /lab001-9-aws-cap-quyen-cho-phep-chinh-sua-route53
image: https://i.imgur.com/je9uyhx.png
---

* content
{:toc}
Trong bài này có 2 cách để cấp quyền:
- Cách thứ nhất ta có thể gán IAM User vào trong EC2. Bằng cách gõ lệnh `aws configure` để gán IAM user với quyền mà ta cho phép
- Cách thứ hai ta không cần `aws configure` thay vào đó ta sẽ gán trực tiếp quyền cho EC2




**Cách 1: Gán IAM User vào trong EC2**

Tại IAM User assign vào Group có quyền access route53. Ở đây ta đã tạo trước Group là Developers.

![image](https://user-images.githubusercontent.com/27756008/54733501-8f3c0e00-4bcc-11e9-8c4c-c5a3646b6a0f.png)

![image](https://user-images.githubusercontent.com/27756008/54733507-97944900-4bcc-11e9-8252-83fa2003856f.png)

![image](https://user-images.githubusercontent.com/27756008/54733528-ada20980-4bcc-11e9-8d55-b466912be334.png)

![image](https://user-images.githubusercontent.com/27756008/54733535-b397ea80-4bcc-11e9-9ab0-d6cd615b9ddf.png)


*Configure aws cho Bastion*
```bash
[root@ip-10-0-1-83 ec2-user]# aws configure
AWS Access Key ID [None]: ***
AWS Secret Access Key [None]: ***
Default region name [None]: us-east-1 #Virginia
Default output format [None]: text
```
Như vậy là ta đã gán IAM User vào trong Bastion


**Cách 2: Thêm quyền trực tiếp cho EC2**

![image](https://user-images.githubusercontent.com/27756008/55050070-7bd3eb80-5081-11e9-8f6d-165828364a79.png)

![image](https://user-images.githubusercontent.com/27756008/55050107-94dc9c80-5081-11e9-9bcb-3974339dab90.png)

