---
layout: post
title: Instance method - Class method và Static method trong Python khác nhau như thế nào
date: 2018-12-20 21:32:00 +0700
categories: Python
tags: Python OOP Instance Class Static
author: minhtang
description: Sự khác nhau giữa instnace method, class method và static method trong Python
permalink: /su-khac-nhau-giua-instance-method-class-method-va-static-method-trong-python.html
image: https://i.imgur.com/InAI9ul.jpg
---

* content
{:toc}


Trong lập trình hướng đối tượng nói chung instance method và class method đều rất quan trọng. Một số ngôn ngữ như Python cung cấp thêm một loại method nữa là static method. Trong bài viết này, chúng ta sẽ tìm hiểu các loại phương này trong ngôn ngữ Python.

![Instance method - Class method - Static method](https://i.imgur.com/InAI9ul.jpg)



## Mở đầu
Hãy xem xét ví dụ là một class sau để hiểu rõ hơn về các loại phương thức này:

```python
>>> class Foo:
...     def instance_bar(self, x):
...         print("executing instance_bar(%s, %s)" % (self, x))
...     @classmethod
...     def class_bar(cls, x):
...         print("executing class_bar(%s, %s)" % (cls, x))
...     @staticmethod
...     def static_bar(x):
...         print("executing static_bar(%s)" % x)
...
>>> foo = Foo()
```

Dưới đây là cách đơn giản nhất để thực thi một phương thức:

```python
>>> foo.instance_bar('args')
executing instance_bar(<__main__.Foo object at 0x7fef22567518>, args)
```

**Instance method là một method thuộc về một đối tượng**, đây là một phương thức phổ biến nhất. Một đối tượng (instance của class) được ngầm truyền thành tham số thứ nhất (self) của phương thức này.

**Class method là phương thức thuộc về cả class. Khi thực thi, nó không dùng đến bất cứ một instance nào của class đó**. Thay vào đó, cả class sẽ được truyền thành tham số thứ nhất (cls) của phương thức này:

```python
>>> Foo.class_bar('args')
executing class_bar(<class '__main__.Foo'>, args)
```

> **Chú ý:** Một điều thú vị là class method cũng có thể gọi từ instance mà không gặp trở ngại gì.
Mặc dù vậy nhưng chúng ta nên sử dụng đúng chức năng với tên gọi của nó.

```python
>>> foo.class_bar('args')
executing class_bar(<class '__main__.Foo'>, args)
```

**Static method là một phương thức đặc biệt, nó không sử dụng bất cứ thứ gì liên quan đến class hay instance của class đó**. Cả self hay cls đều không xuất hiện trong tham số của loại phương thức này. Và static method hoạt động không khác gì một hàm thông thường.

```python
>>> foo.static_bar('args')
executing static_bar(args)

>>> Foo.static_bar('args')
executing static_bar(args)
```

Về cơ bản, phương thức cũng giống như hàm. Tuy nhiên, instance_bar là một instance method, và khi bạn gọi foo.instance_bar thì Python sẽ ngầm truyền foo thành tham số thứ nhất của phương thức đó. Và foo.instance_bar không còn là hàm nguyên gốc ban đầu mà là một phiên bản đã được "bind" cho foo.

```python
>>> foo.instance_bar
<bound method Foo.instance_bar of <__main__.Foo object at 0x7f994f8ad748>>
```

Vì vậy, mặc dù instance_bar cần hai tham số, nhưng foo.instance_bar chỉ cần một tham số thôi.

Tương tự với class method, Foo.class_bar thì class Foo được ngầm gán cho tham số thứ nhất của class_bar. Ngay cả khi gọi từ instance, foo.class_bar thì class Foo vẫn được gán cho class_bar.

```python
>>> Foo.class_bar
<bound method Foo.class_bar of <class '__main__.Foo'>>
```

<div class="merge-code"></div>

```python
>>> foo.class_bar
<bound method Foo.class_bar of <class '__main__.Foo'>>
```

Riêng static method là trường hợp đặc biệt, mặc dù nó là một phương thức nhưng dù gọi foo.static_bar hay Foo.static_bar thì kết quả trả về vẫn là hàm ban đầu không hề được "bind" bất cứ một đối tượng nào.

```python
>>> foo.static_bar
<function Foo.static_bar at 0x7f994f892b70>
```
<div class="merge-code"></div>

```python
>>> Foo.static_bar
<function Foo.static_bar at 0x7f994f892b70>
```

## Khi nào thì nên sử dụng static method
Static method, với sự đặc biệt của nó, được dùng rất hạn chế. Bởi vì nó không giống như instance method hay class method, nó không có bất cứ sự liên quan tới đối tượng gọi nó. Static method không phải là phương thức được sử dụng thường xuyên.

Tuy nhiên, nó vẫn tồn tại là có lý do của nó. Static method thường dùng để nhóm các hàm tiện ích lại với nhau (trong cùng một class). Nó không yêu cầu gì từ class đó, ngoại trừ việc tham chiếu khi được gọi.

Nhưng hàm như vậy không cho vào class nào cũng không vấn đề gì. Nhưng nhóm chúng trong class và gọi chúng thông quan instance hoặc class sẽ giúp chúng ta hiểu hơn về bối cảnh cũng như chức năng của chúng.

Nếu bạn cảm thấy những lợi ích trên từ việc sử dụng static method, hãy sử dụng nó. Còn không, hãy dùng hàm và module như thông thường.

## Kết luận
Instace method, class method, static method là những khái niệm rất cơ bản trong lập trình hướng đối tượng với Python. Nắm vững khái niệm cũng như bối cảnh sử dụng chúng sẽ giúp chúng ta code đẹp hơn rất nhiều

*Nguồn: [https://realpython.com/instance-class-and-static-methods-demystified/](https://realpython.com/instance-class-and-static-methods-demystified/)*
