---
title: React Native tổng quan
categories:
    - programming
tags:
    - library
---

Nhân tiện đợt này tham gia khóa học React Native nên mình sẽ viết note này để tổng hợp lại kiến thức. 

React Native là một công nghệ, mà đã là công nghệ thì sẽ có lúc nó lỗi thời. Công nghệ nó có tồn tại được hay không là do bản chất đứng đằng sau nó.

## React Native là framework hay library ?
RN là một framework, khác với ReactJS, vốn là một UI library cho web. Cả hai đều được backed bởi Facebook, có community khá lớn. Tuy hướng đến những nền tảng khác nhau, nhưng chúng có chung một nguyên lý thiết kế.


## Tại sao người ta dùng React Native ?
RN sinh ra để những JS dev có thể tham gia vào viết native app, chủ yếu là cho 2 hệ điều Android và iOS.

Trên thị trường cũng có nhiều giải pháp công nghệ khác hỗ trợ cross-platform development. Tuy nhiên RN được sử dụng khá nhiều là do nó nhanh, các component trong RN sẽ được map sang native component trong các nền tảng di động.

Còn tại sao map được, thì là do có một thằng "bridge" ở trung gian thực hiện việc mapping này. Cái này không quá quan trọng, bạn biết là có thằng này nó thực hiện là được.



## Nhược điểm của React Native ?

Nhược điểm của nó có thể thấy rõ rằng là nó vẫn khá mới, chỉ mới xuất hiện từ 2015. 

Theo kinh nghiệm của mình cũng như chính lời của anh lecturer thì việc cài đặt RN thôi cũng có thể sinh ra rất nhiều lỗi, chủ yếu là về xung đột dependencies. Cái này thì cũng có thể khắc phục được bằng cách sử dụng Expo (một công cụ giúp quản lý, deploy, cài đặt RN project và hơn thế nữa...). Dùng lệnh `expo install` thì sẽ giảm thiểu nguy cơ xung hơn là sử dụng `npm install`.

Nếu ai đã làm quen với Python thì có thể thấy rằng việc install bằng Expo cũng giống như dùng Anaconda để cài.

Nhược điểm thứ 2 đó là khó để debug, có nhiều lỗi nó báo không rõ ràng (hoặc có thể là do mình không hiểu). Nhưng đại loại là tìm kiếm cách debug trên mạng khá khoai vì sẽ có nhiều kiểu có thể dẫn đến lỗi đấy. (You know what I'm talking about right)

Tương lai của RN cũng không quá chắc chắn, cũng không biết lúc nào thì FB cho dừng dự án này chẳng hạn. Có thể chưa phải lúc này, khi mà nó vẫn được rất nhiều người sử dụng.

Có một số công nghệ cũng mới nổi lên, ví dụ như Flutter do Google đứng sau. Mà Google thì đứng sau Android, thế nên bạn biết rồi đấy :). 

Anw, RN có đáng học tại thời điểm này không ? Thì thực ra là có, RN vẫn được nhiều công ty startup tuyển. Vì nó giúp người ta giảm chi phí xây dựng UI, vì nó vẫn được việc, vẫn tạo được những app hiển thị đơn giản (chủ yếu xử lý trên cloud).


## Bắt đầu với React Native
Để bắt đầu với React Native, thì đầu tiên nên biết căn bản về html, javascript, css, nhất là javascript. Ở phần này thì mình sẽ bám theo nội dung chương trình mà mình đang tham gia vì mình thấy nó khá là ổn.

Sau khi biết cơ bản rồi thì có thể bắt tay vào cài đặt React Native. Phần này chính ra khá là lằng nhằng đấy. Có thể bám theo hướng dẫn cài đặt trong trang chủ của RN. Thì về cơ bản là nên sử dụng expo để cài đặt môi trường. 

Nếu không có máy thật thì có thể sử dụng emulator. Với Android thì cài Android Studio rồi tạo emulator. (Với Mac thì chịu, mình chưa có Mac + iphone để mà test...). Anw, cài app Expo vào máy là nó có thể kết nối được.

Nhược điểm của thằng Expo này đó là nó chỉ hỗ trợ project React Native thuần JS. Với trường hợp muốn inject một số native component vào project thì sẽ phải "eject from Expo". Nói chung thì tốt nhất là cố gắng tìm mọi cách để không phải rời Expo. Tránh xa các cái job sử dụng RN để làm mấy cái quét ảnh, dùng camera nhận diện các thứ vì những app như thế sẽ phải sử dụng các cảm biến của thiết bị. 

Cài đặt xong thì bắt tay vào học tiếp thôi. Nguồn tham khảo tốt nhất chính là docs, vì RN còn mới, thay đổi rất nhanh. Các nguồn tham khảo có thể nhanh chóng bị outdated. 

Các vấn đề của RN thì phải bắt tay vào code thì mới rõ được. Trong chương trình mình học thì có một số assignment hỗ trợ việc học:
- Clone Instagram profile screen: học về cách layout trong RN, chủ yếu là sử dụng flex. Học cách sử dụng các components cơ bản. 
- Oẳn tù tì: học về props và states. Học về cách tạo  custom components.
- Todolist: học về react-navigation.

Ở assignment todolist thì mình gặp phải vấn đề state và prop, về cách chia sẻ data giữa các screen. Thì trong hướng dẫn trong docs, người ta cũng có hẳn một mục về Lift up states, đại loại là đẩy state của child components thành state của parent components, biến nó thành ground-truth data. 

Tuy nhiên là với một dự án phức tạp thì việc nâng state lên như kia sẽ rất phức tạp, khó kiểm soát. Thế nên người ta sẽ phải dùng Redux. 

Phần Redux mình chưa học chi tiết, thế nên không chém tiếp được :v. Mấy tuần nữa học xong thì mình viết tiếp.

To be continued...

## Tham khảo
- [React Native: What is it and why is it used](https://medium.com/@thinkwik/react-native-what-is-it-and-why-is-it-used-b132c3581df#:~:text=React%20Native%20is%20a%20framework,library%20to%20create%20user%20interfaces.)
- [React Native docs](https://reactnative.dev/docs/getting-started)
