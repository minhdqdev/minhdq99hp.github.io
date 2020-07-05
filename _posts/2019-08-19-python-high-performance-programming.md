---
layout: post
title:  "Python High Performance Programming"
date:   2019-08-19 15:00:00 +0700
description: "Ghi chú những kiến thức học được từ cuốn sách"
categories: programming 
mathjax: false
header_image: /images/2019-08-19-python-high-performance-programming/header.jpg
---

## 1. Benchmarking and Profiling
Phát hiện phần bị chạy chậm trong phần mềm (bottleneck) là một công việc quan trọng khi muốn tối ưu code.

**Profiling** là một kỹ thuật giúp xác định được bottlenecks. Profiler là một chương trình chạy code và quan sát xem mỗi function chạy mất bao lâu, giúp xác định ra vị trí chạy chậm. 

Khi thiết kế chương trình hiệu suất cao (performance-intensive), bước đầu tiên là viết code chưa cần quan tâm đến tối ưu vội.

> "Premature optimization is the root of all evil" - Donald Knuth

Một số nguyên tắc cần phải nhớ khi tối ưu code:
- Make it run: đảm bảo code chạy ra kết quả đúng trước khi tối ưu.
- Make it right: đảm bảo thiết kế chương trình chắc chắn, có hệ thống.
- Make it fast: sau đó, tối ưu những phần chạy chậm trước.

### Writing tests and benchmarks
- **Test**: Trong quá trình tối ưu, chún ta sẽ phải viết lại code, vì thế phải tạo ra các hàm test để tránh mất thời gian vào broken code.
- **Benchmark**: Tạo hàm benchmark để đánh giá performance của code.

### Timing your benchmarks
Cách 1: dùng lệnh `time` của Unix.
```
time python simul.py
```
sẽ trả về  thông tin:
```
real    0m7.998s
user    0m8.094s
sys     0m0.221s
```
Với:
- **real**: Thời gian thực tế để chạy chương trình.
- **user**: Thời gian của các CPUs để tính toán
- **sys**: Thời gian của các CPUs để thực hiện các system-related tasks. VD: memory allocation.

Chú ý: 
- user+sys có thể nhiều hơn real do đa nhân chạy song song.
- Để đo chính xác hơn thì benchmark nên chạy đủ lâu, để quá trình setup ngắn hơn execution.

Cách 2: Module `timeit`

Module timeit chạy đoạn code trong vòng lặp n lần, rồi thực hiện quá trình này r lần (thường r là 3) rồi trả về giá trị tốt nhất. Vì vậy, timeit phù hợp để tính toán thời gian chính xác một phần nhỏ của chương trình.

Chú ý:
- `timeit` có thể dùng dưới dạng module hoặc magic command trong Jupyter Notebook.

### Finding bottlenecks with `cProfile`
```
python -m cProfile simul.py
```
se in ra danh sách thời gian chạy của từng phần trong code.

`cProfile` output có 5 cột: ncalls, tottime, cumtime, percall, filename:lineno:

Metric quan trọng nhất là tottime, thời gian chạy thực tế trong function body, không bao gồm sub-calls.

**KCachegrind** là một công cụ GUI hỗ trợ profiling. Dùng `pyprof2calltree` để convert output của `cProfile` sáng `KCachegrind`... (đọc thêm)

### Profile line by line with `line_profiler`
Sau khi xác định được function cần tối ưu thì sử dụng `line_profiler` để check xem thời gian chạy của các dòng. (đọc thêm)

### Optimizing Code 
Có một số cách để tối ưu, cách tốt nhất là thay đổi thuật toán. 

Module `dis` (disassemble): liệt kê các instructions. 

### Profiling memory usage with `memory_profiler`
Tương tự, `memory_profiler` thống kê lượng bộ nhớ bị chiếm qua từng dòng. (đọc thêm)

Cách để tối ưu memory: sử dụng `__slot__`

### Performance tuning tips for pure Python code
Khi tối ưu code Python, tốt nhất nên nhìn vào standard library, nơi chứa nhiều modules đã được tối ưu, viết bằng C.

Module `collections` cung cấp nhiều data containers phù hợp để giải quyết một số trường hợp.



## 2. Fast Array Operations with Numpy

## Reference
- Book: Python High Performance Programming