---
title:  "Python CLI"
categories: 
    - programming
header:
    image: /images/2019-08-23-python-cli/header.png
---

Để hiểu cách sử dụng `argparse` thì bạn hãy đọc 2 bài đầu tiên dưới phần Reference, nhất là bài của RealPython.

Mình có viết ví dụ về cách sử dụng tại repo [minhdq99hp/sample-code](www.github.io/minhdq99hp/sample-code)


Có một số thư viện hỗ trợ việc viết CLI cho python (VD: click), trong đó `argparse` là một cách standard nhất để viết.

- An **argument** is a single part of a command line, delimited by blanks.
- An **option** is a particular type of argument (or a part of an argument) that can modify the behavior of the command line.
- A **parameter** is a particular type of argument that provides additional information to a single option or command.



### `argparse`
Đọc bài viết [này](https://towardsdatascience.com/learn-enough-python-to-be-useful-argparse-e482e1764e05).

Ngoài ra, mình cũng viết file `argparse_example.py` tại repo [minhdq99hp/sample-code](https://github.com/minhdq99hp/sample-code)


## References
- https://realpython.com/command-line-interfaces-python-argparse/#what-is-a-command-line-interface
