---
layout: post
title:  "Giữ thứ tự truy vấn khi dùng mệnh đề WHERE IN()"
date:   2018-12-01 10:21:22 +0700
categories: MySQL
tags: MySQL Database CSDL
author: minhtang
description: "Khi truy vấn với mệnh đề WHERE IN() thì kết quả nào được tìm thấy trước sẽ cho ra trước. Vậy làm thế nào để có thể truy vấn mà giữ nguyên thứ tự record trong CSDL"
---

* content
{:toc}

Khi sử dụng truy vấn với mệnh đề WHERE IN() thì kết quả nào được tìm thấy trước sẽ cho ra trước, nó không quan tâm đến thứ tự record trong database. Vậy làm thế nào để có thể truy vấn mà giữ nguyên thứ tự với mệnh đề WHERE IN()





## Nội dung

Giả sử ta có table như sau:

| id | name |
|--|--|
| 1 | Thứ nhất |
| 2 | Thứ hai |
| 3 | Thứ ba |

Nếu như ta truy vấn `WHERE id IN (3 , 2 , 1)`, thì kết quả vẫn trả ra như sau:

| id | name |
|--|--|
| 1 | Thứ nhất |
| 2 | Thứ hai |
| 3 | Thứ ba |

Nhưng ta mong muốn phải trả ra đúng thứ tự mà ta truy vấn là 3, 2, 1 chứ không phải 1, 2,3. Với yêu cầu như vậy thì ta chỉ cần thêm `ORDER BY FIELD(id, 3, 2, 1)` hoặc `ORDER BY FIND_IN_SET(id, '3, 2, 1')`. Như vậy kết quả sẽ đảm bảo cho ta đầu ra sẽ đúng theo như mong muốn.

> **Tóm lại:** Muốn giữ nguyên thứ tự truy vấn thì ta có 2 cách. Cách 1 sử dụng `FILED`, cách 2 sử dụng `FIND_IN_SET`. Với `FIELD` ta truyền vào nó 1 dãy số, còn với `FIND_IN_SET` ta truyền vào nó 1 dãy số dưới dạng chuỗi.

## Ví dụ thực tế
Giả sử ta muốn export 1 file csv với dữ liệu đầu ra như sau:

| Japanese | English |
|--|--|
| こんにちは | Hello |
| さようなら | Goodbye |
| おはようございます | Good morning |

Dữ liệu trong Database:

_Table: Languages_

| id | name |
|--|--|
| 1 | English |
| 2 | Vietnamese |
| 3 | Japanese |


Dữ liệu cho sẵn:

| | |
|--|--|
| こんにちは | Hello |
| さようなら | Goodbye |
| おはようございます | Good morning |


_Yêu cầu:_ Hãy truy vấn ra 2 dòng tiếng Nhật và tiếng Anh để có thể gắn vào dữ liệu trên

Để giải quyết bài toán trên thì ta sẽ truy vấn để lấy ra ngôn ngữ tiếng Nhật và tiếng Anh với cú pháp như sau:
``` SELECT * FROM languges WHERE id IN (3, 1) ```

Sau khi chạy câu lệnh trên thì dữ liệu sẽ là:

| id | name |
|--|--|
| 1 | English |
| 3 | Japanese |


Ta nhận thấy rằng nếu đem dữ liệu truy vấn thế này mà gắn vào dữ liệu cho sẵn thì kết quả sẽ sai. Bởi vì cột đầu tiên sẽ là tiếng Nhật, cột thứ hai sẽ là tiếng Anh. Nhưng đằng này thì kết quả truy vấn cho ra thì tiếng Anh lại nằm trước tiếng Nhật, mặc dù ta truy vấn tiếng Nhật trước tiếng Anh `WHERE IN (3, 1)` (3: Nhật, 1: Anh)

_Kết quả sai:_

| English | Japanese |
|--|--|
| こんにちは | Hello |
| さようなら | Goodbye |
| おはようございます | Good morning |

Lúc này ta cần phải truy vấn đầu ra sao cho kết quả tiếng Nhật phải đảm bảo nằm trước tiếng Anh, với cú pháp như sau:

``` SELECT * FROM languges WHERE id IN (3, 1) ORDER BY FIND_IN_SET(id, '3, 1')```

hoặc

``` SELECT * FROM languges WHERE id IN (3, 1) ORDER BY FILED(id, 3, 1)```

Với câu lệnh trên thì kết quả trả ra sẽ là:

| id | name |
|--|--|
| 3 | Japanese |
| 1 | English |

Cho nên ta cần lưu ý khi sử dụng truy vấn WHERE IN đối với các bài toán yêu cầu cần sự chính xác thứ tự cho kết quả đầu ra.
