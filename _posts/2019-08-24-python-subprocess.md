---
title: "Python `subprocess` module"
categories: programming
header:
    image: /images/2019-08-23-python-cli/header.png
---

## Định nghĩa
The `subprocess` mudle allows you to spawn new processes, connect to their input/output/error pipes, and obtain their return codes.

Có các hàm:
- call
- check_call
- check_output

Về bản chất, `subprocess` sử dụng class `Popen` để tạo và quản lý process. Khi có nhu cầu sử dụng phức tạp hơn thì phải sử dụng `Popen`. VD: kill process.

Code tham khảo mình để trong repo [minhdq99hp/sample-code](https://github.com/minhdq99hp/sample-code/tree/master/subprocess).

## References
- https://docs.python.org/2/library/subprocess.html