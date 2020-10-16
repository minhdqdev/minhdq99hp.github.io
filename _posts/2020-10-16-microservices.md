---
title: [Draft] Kinh nghiệm làm việc với Microservices
toc: true
categories:
    - Technology
tags:
    - architecture
    - experience
---

Terms:
- A microservice is a single purpose software application


Với một hệ thống microservice thì việc kết nối giữa các service rất quan trọng. Nó cần ổn định, tin cậy, failure tolerable. Phải đảm bảo tối thiểu rằng không một kết nối lỗi nào có thể break cả service.

Các framework đã giải quyết cho mình vấn đề đấy rồi, tuy nhiên nếu như task bị lỗi thì phải có cách thông báo lại, hoặc cách handle nó. Mình lấy ví dụ cụ thể ở đây là TTS service và backend AutoVid.

Backend service sẽ gửi thông tin đến TTS service bao gồm: text, voice, callback_url.
TTS sẽ xử lý và sẽ gửi metadata của kết quả về callback_url (metadata ở đây bao gồm: link lấy file mp3, subtitle). Phía backend sẽ dựa vào đó để lấy dữ liệu về. Cơ chế callback_url ở đây mình học được từ Vbee API. Nó cũng hoạt động theo cơ chế này. Các service trong mô hình microservice sẽ không thằng nào phải đợi thằng nào cả.

Nếu quá trình diễn ra suôn sẻ thì không sao, trường hợp xấu có thể xảy ra là:
	* 
Backend không gửi thông tin task cho TTS service: trường hợp này thì đơn giản rồi, mình try catch lỗi ở backend luôn và nếu TTS service trả về status_code >= 300 (hiện tại là thế, sau sẽ phải specific hơn) là lỗi.
	* 
Backend gửi thành công nhưng TTS service bị lỗi: trong trường hợp này thì bên phía TTS service sẽ phải try/catch toàn bộ lỗi có thể xảy ra và gửi thông báo rằng TTS xử lý lỗi về phía Backend.
	* 
TTS lỗi nhưng không gửi về Backend được: cái này một là do TTS không connect được đến backend, hai là backend cung cấp callback_url sai. Ở trường hợp này thì bên phía Backend buộc phải có cơ thế timeout.Vấn đề bây giờ là đặt timeout như nào khi mà backend sẽ không có process nào đợi ? -> Sử dụng scheduler để tính timeout. Khi Backend gửi task thành công thì sẽ cập nhật 2 field: created_datetime và status. Khi scheduler đến thời điểm kích hoạt (created_datetime + max_timeout), nó sẽ kiểm tra field status.




Vậy kinh nghiệm rút ra ở đây là:

Ở cả 2 phía sender và receiver:
	* 
Phải đảm bảo code chạy không xảy ra lỗi, phải có try/catch toàn bộ trường hợp. Nếu không thì sẽ rất khó để debug.



Ở phía sender:
	* 
Khi gửi task về receiver thì bản thân cũng phải set timeout đề phòng trường hợp task bị drop không rõ nguyên nhân.
	* 
Phải cung cấp callback_url chuẩn xác, đảm bảo đường link đấy hoạt động ổn định.



Ở phía receiver:
	* 
Trạng thái của task như thế nào, thành công hay thất bại phải gửi thông tin đấy về sender bằng mọi cách.
	* 
Nên check callback_url mà sender gửi xem có mở không, Để tránh trường hợp phải xử lý task nặng xong gửi lại thì không được, rất tốn resource.

