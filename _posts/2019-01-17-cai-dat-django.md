---
layout: post
title: Cài đặt Django
date: 2019-01-17 21:34:00 +0700
categories: Django
tags: Django framework
author: minhtang
description: Hướng dẫn cài đặt Django và quản lý các thư viện trong Django
permalink: /cai-dat-django
image: https://i.imgur.com/DFfcfkM.jpg
---

* content
{:toc}

![Cài đặt Django](https://i.imgur.com/DFfcfkM.jpg)




## Cài đặt Python

Để cài đặt được Django yêu cầu chúng ta phải có python. Ở bài trước mình đã hướng dẫn các bạn cách cài đặt Python, chúng ta hãy xem qua bài [Hướng dẫn cài đặt Python](https://rubykachu.github.io/cai-dat-python-va-moi-truong)

## Pipenv là gì và hoạt động như thế nào?

**Pipenv** tạm gọi nó là một chương trình dùng để quản lý các gói thư viện (dependencies) của Django. Thay vì sử dụng file `requirements.txt` trong project và quản lý bằng môi trường ảo `virtualenvs`. Bây giờ bạn sẽ sử dụng `Pipfile` trong project để làm tất cả điều đó một cách tự động.

Bắt đầu cài đặt thông qua `pip`

`$ pip install -U pipenv`

## Sử dụng pipenv
Tạo thư mục dự án và sử dụng pipenv để tạo Pipfile
```
$ mkdir my_project
$ cd my_project
$ pipenv install
```
Chúng ta sẽ được 2 file `Pipfile` và `Pipfile.lock`

Nội dung cảu Pipfile:
```
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"
[packages]
[dev-packages]
[requires]
python_version = "3.7"
```

## Cài đặt Django

```
$ pipenv install django
Installing django
...
Installing collected packages: pytz, django
Successfully installed django-2.1.2 pytz-2018.5
Adding django to Pipfile's [packages]…
Pipfile.lock (4f9dd2) out of date, updating to (a65489)…
Locking [dev-packages] dependencies…
Locking [packages] dependencies…
Updated Pipfile.lock (4f9dd2)!
Installing dependencies from Pipfile.lock (4f9dd2)…
🐍   ▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉▉ 2/2 — 00:00:01
To activate this project's virtualenv, run pipenv shell.
Alternatively, run a command inside the virtualenv with pipenv run.
```

Kiểm tra `Pipfile` sẽ thấy nội dung chứa `django = "*"` đã được thêm vào

Nếu chúng ta muốn cài đặt các gói phụ thuộc cho môi trường DEV thì gõ lệnh

`$ pipenv install --dev <ten_package>`

### Chạy môi trường ảo
Chạy môi trường ảo: `pipenv shell`

Chạy server django: `pipenv run python manage.py runserver` hoặc `pipenv ./manage.py runserver`

Chúng ta có thể chạy script thông qua Pipfile, giống với npm package.json

```
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"


django = "*"
[dev-packages]
yapf = "*"

[scripts]
server = "python manage.py runserver"

[requires]m
python_version = "3.7"
```

Bây giờ ta có thể sử dụng script như sau: `pipenv run server`

### Code trên màn hình shell

Chúng ta có thể sử dụng màn hình shell để có thể test code trực tiếp, ví dụ như thực hiện các phép toán hay truy vấn dữ liệu. Vậy cách vào màn hình shell như sau: `pipenv run python manage.py shell`

Tại đây ta có thể làm mọi thứ liên quan đến python và django

```
a = 1
b = 2
a + b
>>> 3
```
[Tài liệu pipenv](https://pipenv.readthedocs.io/en/latest/)

_[Dịch từ nguồn hackernoon](https://hackernoon.com/reaching-python-development-nirvana-bb5692adf30c)_










