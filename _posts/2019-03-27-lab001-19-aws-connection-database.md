---
layout: post
title: 'LAB001-19: AWS - Kết nối database thông qua bastion'
date: 2019-03-27 11:00:00 +0700
categories: AWS
tags: AWS LAB RDS Bastion
author: minhtang
description: 'LAB001-19: AWS - Kết nối database thông qua bastion'
permalink: /lab001-19-aws-ket-noi-database-thong-qua-bastion
image: https://i.imgur.com/je9uyhx.png
---

* content
{:toc}
Ta sẽ dùng 2 cách để kiểm tra kết nối đến database thành công hay chưa. Cách 1 ta sẽ dùng phần mềm TablePlus với giao diện console sẽ dễ dàng connect đến PostgreSQL thông qua Bastion. Cách 2 là login vào EC2 và cài đặt PostgreSQL client và sử dụng lệnh trong terminal để connect đến PostgreSQL





**1. Dùng TablePlus để connect từ bastion đến RDS**

![image](https://user-images.githubusercontent.com/27756008/54800902-d2fb4a00-4c96-11e9-8aab-49b595370a8d.png)

**2. Login bằng ssh từ ec2**

[Hướng dẫn](https://stackoverflow.com/questions/49573258/installing-postgresql-client-v10-on-aws-amazon-linux-ec2-ami)
Cần phải cài đặt postgresql client để connect tới RDS
```bash
sudo yum update
sudo yum install -y  https://download.postgresql.org/pub/repos/yum/10/redhat/rhel-7-x86_64/pgdg-redhat10-10-2.noarch.rpm
sudo sed -i "s/rhel-\$releasever-\$basearch/rhel-latest-x86_64/g" "/etc/yum.repos.d/pgdg-10-redhat.repo"
sudo yum install -y postgresql10
psql --version
#psql (PostgreSQL) 10.7
```

Remote đến RDS
```bash
psql -h <host_end_point> -U <username> -d <database>
# Password for user route53xyz:
# psql (10.7, server 10.6)
# SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
```
![image](https://user-images.githubusercontent.com/27756008/54806720-79eae080-4cad-11e9-8ddb-9595ed4d64f8.png)

**3. Một số lệnh cơ bản**

show databases: `\l`
select database: `\c <database>`
show tables: `\dt`
select table: `SELECT * FROM <table_name>`
