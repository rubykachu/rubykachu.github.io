---
layout: post
title: 'LAB001-10: AWS - Tự động cập nhập route53 khi EC2 reboot'
date: 2019-03-27 11:00:00 +0700
categories: AWS
tags: AWS LAB route53 EC2
author: minhtang
description: 'LAB001-10: AWS - Tự động cập nhập route53 khi EC2 reboot'
permalink: /lab001-10-aws-tu-dong-cap-nhap-route53-khi-ec2-reboot
image: https://i.imgur.com/je9uyhx.png
---

* content
{:toc}
Hướng dẫn: [https://blog.zoph.me/cloud/Update53/#](https://blog.zoph.me/cloud/Update53/#)

**Bước 1:** Tạo 1 Role có quyền truy cập vào Route53. Sau đó gắn vào IAM user. Ở đây ta tạo Role với quyền AmazonRoute53FullAccess
*Hoặc có thể gán trực tiếp IAM Role vào trong EC2*

**Bước 2:** Tạo 1 file JSON với format mà Route53 đã cung cấp. Ở đây ta tạo file có tên `update-route53-A.json`
[https://docs.aws.amazon.com/cli/latest/reference/route53/change-resource-record-sets.html](https://docs.aws.amazon.com/cli/latest/reference/route53/change-resource-record-sets.html)




```json
{
  "Comment": "Update the A record set",
  "Changes": [
    {
      "Action": "UPSERT",
      "ResourceRecordSet": {
        "Name": "test.lambrospetrou.com",
        "Type": "A",
        "TTL": 60,
        "ResourceRecords": [
          {
            "Value": "127.0.0.1"
          }
        ]
      }
    }
  ]
}
```

**Chú ý:** `Value: "127.0.0.1"` Ở đây chỉ là dữ liệu giả để ta dùng regex thay đổi địa chỉ IP thực vào đây

**Bước 3:** Tạo 1 file `.sh` để update Route53. Ở đây ta tạo file có tên `route53_EC2Pub.sh`
![image](https://user-images.githubusercontent.com/27756008/54666862-7fb1bc00-4b1d-11e9-82d1-4e63ff351cce.png)

```bash
#!/bin/sh
if [ -z "$1" ]; then
    echo "IP not given...trying EC2 metadata...";
    IP=$( curl http://169.254.169.254/latest/meta-data/public-ipv4 )
else
    IP="$1"
fi
echo "IP to update: $IP"

HOSTED_ZONE_ID="Nhập Hosted Zone ID"
echo "Hosted zone being modified: $HOSTED_ZONE_ID"

INPUT_JSON=$( cat ./update-route53-A.json | sed "s/127\.0\.0\.1/$IP/" )

# http://docs.aws.amazon.com/cli/latest/reference/route53/change-resource-record-sets.html
# We want to use the string variable command so put the file contents (batch-changes file) in the following JSON
INPUT_JSON="{ \"ChangeBatch\": $INPUT_JSON }"

aws route53 change-resource-record-sets --hosted-zone-id "$HOSTED_ZONE_ID" --cli-input-json "$INPUT_JSON"
```
> Sau khi tạo 2 file thì nhớ `chmod 777 file-name`
> Để test xem lệnh `.sh` của ta chạy đươc chưa thì thực thi nó như sau: `./update53_EC2Pub.sh` hoặc có thể dùng lệnh `bash update53_EC2Pub.sh`

**Bước 4:** Tạo crontab để mỗi khi reboot thì nó tự động update
```bash
crontab -e
@reboot /home/ec2-user/update53-EC2Pub.sh >> /tmp/update53-EC2Pub.log 2>&1
```
Thực thi lệnh `sh` và lưu thông tin vào file log
2>&1: Tức là đẩy lỗi từ file 1(update53-EC2Pub.sh) vào file 2(update53-EC2Pub.log)
1: stdout
2: stderr

Cuối cùng ta sử dụng lệnh `sudo reboot` để chạy lại server và chờ kết quả.

