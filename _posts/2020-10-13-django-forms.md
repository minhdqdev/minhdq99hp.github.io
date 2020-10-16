---
title: Làm việc với Django Forms
categories:
    - Technology
tags: 
    - django
---

Với Django, cách tốt nhất để accept input from user đó là sử dụng form. Việc hiểu cách hoạt động của form và sử dụng chúng là cực kì cần thiết khi học Django.

## HTML Forms
GET và POST là 2 method duy nhất khi làm việc với forms

Với POST thì sẽ gửi lên form data. Phía server đọc trong request.POST.
Ngược lại, với GET thì sẽ format data dưới dạng string rồi append vào trong url -> query parameters.

Thế nên những form quan trọng, như bao gồm password không được sử dụng GET. Chỉ sử dụng GET để search, vì lệnh GET lưu params ngay trong url thế nên có thể dễ dàng share cho người khác.

Django forms xử lý 3 vấn đề chính:
- preparing and restructuring data to make it ready for rendering
- creating HTML forms for the data
- receiving and processing submitted forms and data from the client.


Ví dụ form đơn giản:
```python
from django import forms

class NameForm(forms.Form):
    your_name = forms.CharField(label='Your name', max_length=100)
```

Options:
- max_length: thêm vào luôn html -> validate ngay ở template và trong backend.

Nếu form `is_valid()` thì có thể access `form.cleaned_data`

## Initial populating on Django forms
```python
data={'username': user.username}
form = UserForm(initial=data)
```


## References
- [https://docs.djangoproject.com/en/3.1/topics/forms/](https://docs.djangoproject.com/en/3.1/topics/forms/)