---
layout: post
title: 'LAB001-6: AWS - Tạo Route Table'
date: 2019-03-27 10:30:00 +0700
categories: AWS
tags: AWS LAB
author: minhtang
description: 'LAB001-6: AWS - Tạo Route Table'
permalink: /lab001-6-aws-tao-route-table
image: https://i.imgur.com/je9uyhx.png
---

* content
{:toc}

**1. Tạo Route Table cho Public Subnet**

![image](https://user-images.githubusercontent.com/27756008/54732322-bfcc7980-4bc5-11e9-9feb-d95eb9d7ede2.png)




![image](https://user-images.githubusercontent.com/27756008/54732355-dd99de80-4bc5-11e9-80ea-e92218d07c08.png)
![image](https://user-images.githubusercontent.com/27756008/54732363-eb4f6400-4bc5-11e9-9a6b-ae0f22f7b832.png)

Liên kết Route table vừa tạo đến Subnet Public

![image](https://user-images.githubusercontent.com/27756008/54732391-10dc6d80-4bc6-11e9-854a-cecbb373eecc.png)
![image](https://user-images.githubusercontent.com/27756008/54732399-1a65d580-4bc6-11e9-9bb8-c1b45a6d3941.png)

Sau khi liên kết thì add Routes

![image](https://user-images.githubusercontent.com/27756008/54732489-a677fd00-4bc6-11e9-9ce0-243e95803010.png)

![image](https://user-images.githubusercontent.com/27756008/54732617-58172e00-4bc7-11e9-9370-84f00065b484.png)

![image](https://user-images.githubusercontent.com/27756008/54732628-61a09600-4bc7-11e9-8c25-00e218c971c5.png)

**2. Tạo Route table cho Private**

Tương tự như trên, nhưng phần Association ta sẽ liên kết đến Subnet Private.
Phần Add Route thì chúng ta chưa setting được, bởi vì chưa có NatInstance. Nhưng tạm thời thì sẽ tạo ra và để đó (tức sẽ chưa đi được internet). Chúng ta sẽ qua phần 7.2 để sau khi tạo NatInstance thì sẽ add Route cho nó.
