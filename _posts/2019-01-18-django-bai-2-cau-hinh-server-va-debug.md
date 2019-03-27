---
layout: post
title: 'Bài 2: Django - Cấu hình server và debug'
date: 2019-01-17 21:00:00 +0700
categories: Django
tags: Django Framework Debug
author: minhtang
description: Hướng dẫn cấu hình server django và cách debug code
permalink: /bai-2-django-cau-hinh-server-va-debug-code
image: https://i.imgur.com/6npLaDl.jpg
---

* content
{:toc}

![Cài đặt Python](https://i.imgur.com/6npLaDl.jpg)



## Cài đặt server plus
Mục đích ta cài đặt server plus để có thể debug code tốt hơn và có thể autoreload module tại màn hình shell một cách realtime khi có sự thay đổi.

Đầu tiên chúng ta hãy cài đặt gói `django-extensions`

`$ pipenv install django-extensions` hoặc `pip install django-extensions`

Việc sử dụng `pipenv` hay `pip` là tuỳ các bạn. Ở đây mình sẽ sử dụng `pipenv`

Sau khi cài đặt chúng ta sẽ vào file `settings.py` và bổ sung:

```python
INSTALLED_APPS = (
    # others app
    'django_extensions',
)
```

Để kiêm tra version chúng ta vào màn hình shell

```
>>> import django_extensions
>>> django_extensions.VERSION
(0, 8)
```



