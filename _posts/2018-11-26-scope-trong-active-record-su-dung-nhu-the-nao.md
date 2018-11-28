---
layout: post
title:  "Scope trong Active Record sử dụng như thế nào cho đúng"
date:   2018-11-25 19:30:18 +0700
categories: RubyOnRails
tags: Rails, Scope, ActiveRecord
author: Minh Tang Q.
permalink: /scope-trong-active-record-su-dung-nhu-the-nao-cho-dung.html
---

* content
{:toc}


Đối với developer Rails thì việc sử dụng scope và class method khá quen thuộc, nhưng sử dụng nó như thế nào cho đúng thì ta cùng xem xét ví dụ bên dưới:
```ruby
# model/company_contract.rb
class CompanyContract < ApplicationRecord
    # Ví dụ 1:
    scope :latest_contract, lambda { |company_id|
        where(company_id: company_id).order(:start_date).last
    }

    # Ví dụ 2:
    scope :latest_contract, lambda { |company_id|
        find_by(company_id: company_id).order(:start_date)
    }
end
```



Trong đoạn code trên ta sử dụng `scope` để chỉ lấy ra **duy nhất một kết quả** dựa vào đối số truyền vào. **Nếu như tìm thấy dữ liệu** thì kết quả đều cho ra như nhau. Nhưng điều đáng lưu ý là giả sử như nếu không có dữ liệu trả về thì điều gì xảy ra?

Bởi vì `scope` là một `Relation` cho nên nếu như tìm không ra dữ liệu thì kết quả sẽ trả ra tất cả các Record có trong bảng CompanyContract.

Cho nên từ giờ ta đúc kết ra một kinh nghiệm nếu như ta muốn **tìm một kết quả** thì ta nên sử dụng `class method`, còn ngược lại nếu đầu ra là 1 tập hợp các kết quả thì vẫn sử dụng scope như bình thường.
Trong ví dụ trên ta có thể viết class method như sau:
```ruby
def self.lastest_contract(company_id)
    find_by(company_id: company_id).order(:start_date)
end
```
Lưu ý: Nếu ta sử dụng class method cho việc truy vấn lấy ra nhiều kết quả thì ta sẽ không `chain` (nối) các method khác. Đây là điểm khác biệt cần lưu ý khi sử dụng class method và scope.
