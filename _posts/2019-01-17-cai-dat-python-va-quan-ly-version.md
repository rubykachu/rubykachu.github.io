---
layout: post
title: Cài đặt Python và quản lý version
date: 2019-01-17 21:34:00 +0700
categories: Python
tags: Python Pyenv
author: minhtang
description: Hướng dẫn cài đặt Python và quản lý các version trong python
permalink: /cai-dat-python-va-moi-truong
image: https://i.imgur.com/InAI9ul.jpg
---

* content
{:toc}

![Cài đặt Python](https://i.imgur.com/ppw5nzV.jpg)



## Cài đặt môi trường
3 bước sau đây dùng để cài đặt môi trường `pyenv` và `python`

**Bước 1:** Đầu tiên ta sẽ cập nhập homebrew

`$ brew update`

**Bước 2:** Cài đặt pyenv thông qua github

` $ git clone https://github.com/pyenv/pyenv.git ~/.pyenv`

Khai báo biến môi trường **`PYENV_ROOT`**
```
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
```

> **Lưu ý đối với Zsh**: Chỉnh sửa `~/.zshenv` thay cho file `~/.bash_profile`

>**Lưu ý đối với Ubuntu và Fedora**: Chỉnh sửa `~/.bashrc` thay cho file `~/.bash_profile`

**Bước 3:** Thêm `pyenv init`

`$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile`


Cuối cùng thì khởi động lại và kiểm tra phiên bản `pyenv` bằng lệnh `pyenv version`

Từ giờ nếu như ta muốn cài python phiên bản nào thì với cú pháp sau:

`pyenv install 3.7.2`

Trong đó `3.7.2` là version của python. Nếu như muốn xoá phiên bản của python thì gõ lệnh:

`pyenv uninstall 3.7.2`

Sau khi cài đặt python thi hãy kiểm tra version của python vừa cài đặt `python --version`

## Cập nhập pyenv

```
$ cd $(pyenv root)
$ git pull
```

Để chỉ định phiên bản cập nhập thì ta sẽ checkout đến tag có version tương ứng:

```
$ cd $(pyenv root)
$ git fetch
$ git tag
v0.1.0
$ git checkout v0.1.0
```

## Xoá Pyenv
Sử dụng lệnh remove trong Linux để xoá thư mục Pyenv
`rm -rf $(pyenv root)`

## Cài đặt bằng Homebrew
Chúng ta củng có thể cài đặt pyenv bằng cách sử dụng Homebrew

```
$ brew update
$ brew install pyenv
```

Hoặc xoá pyenv bằng homebrew

` brew uninstall pyenv`
