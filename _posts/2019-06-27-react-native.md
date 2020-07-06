---
title:  "React Native là gì ?"
categories: 
  - programming
tags: 
  - web 
  - software
header:
  image: /images/2019-06-27-react-native/react-native.png
---

## React Native là gì ?
React Native là một JavaScript framework để viết một ứng dụng *native* cho iOS và Android (cả Web được nữa). Nó dựa trên React (thư viện JavaScript do Facebook tạo ra), nhưng thay vì hướng đến nền tảng trình duyệt web thì nó hướng đến nền tảng di động. 

Xu hướng sử dụng React Native để phát triển ứng dụng di động đang ngày càng phát triển.

![React Native Trend][react-native-trend]
Source: https://recro.io/blog/wp-content/uploads/2017/07/Javascript-Native-Google-Trends.png

## Ứng dụng nào được viết bằng RN ?
Các ứng dụng nổi tiếng sử dụng React Native có thể kể đến là:
- Facebook
- Instagram
- SoundCloud Pulse
- Bloomberg
- Walmart
- Wix


## Nó hoạt động như thế nào ?
React Native "bridge" dùng native rendering APIs ở trong Objective-C (cho iOS) hay Java(cho Android). Thế nên chương trình của bạn sẽ được render với các mobile UI components, chứ ko phải webviews(như trong web app). 

Ngoài ra, nó cũng truy cập được các platform API như camera, định vị,... nhờ sử dụng JavaScript.

Nhìn một cách tổng quan, có 3 phần chính từ RN platform:
1. **Native Code/Modules**: Đôi khi một ứng dụng cần truy cập các platform API và RN không có các module tương ứng. Có thể sẽ cần phải tái sử dụng native code hoặc các đoạn code yêu cầu performance cao. Tìm hiểu thêm tại [đây](https://facebook.github.io/react-native/docs/native-modules-android.html)
2. **Javascript VM**: JS VM là nơi thực thi phần JS code. 
3. **React Native Bridge**: là cầu nối có trách nhiệm giao tiếp giữa các *native thread* và *JS thread*.



## Điểm mạnh
- Sử dụng platform's standard rendering APIs: đạt hiểu suất cao hơn so với các phương pháp khác(VD: Cordova, Ionic vốn sử dụng webviews).
- Sử dụng JavaScript: 
  + tiết kiệm thời gian, không phải build lại toàn bộ ứng dụng trong quá trình phát triển.
  + không cần IDE cồng kềnh như Android Studio, bất cứ text editor nào cũng được.
  + Tận dụng được Chrome's developer tools trong quá trình debug.
- Cross-platform: Share Knowledge, reuse code dễ dàng.


Giờ ta bắt tay vào phần technical một chút. Sẽ rất dễ dàng nếu bạn biến một chút về html, css, javascript.

## Một số thuật ngữ 
**JSX**: cú pháp dùng để nhúng XML vào trong JavaScript. (và ta cũng có thể nhúng các JavaScript expression vào trong JSX)

**Component's Lifetime**: vòng đời của một component. 


## Cấu trúc chương trình 

Một phần mềm React Native được tạo bởi các *(React) component*. Các component sẽ đại diện cho các Native View và component tương ứng. Ví dụ: 

![An example of a UI component][facebook_inputfield]

Ex: Một `TextInput` trong RN sẽ tương ứng với một native `EditText` trong Android.

Có hai loại dữ liệu để kiểm soát một component (giống cơ chế của React): 
- `props`: Thường thì các component sẽ được tạo ra cùng các thông số. Các thông số này được gọi là `props`, nó là thông số cố định suốt component's lifetime.  
- `state`: dữ liệu có thể thay đổi. Thường thì state sẽ được khởi tạo ở trong constructor, khi muốn thay đổi thì gọi hàm `setState`. 

Bất cứ khi nào một trong hai cái trên thay đổi thì chương trình sẽ tự động rerender lại UI.

Điểm qua một số các component đơn giản thì có:
- Text
- Image
- View
- TextInput

## Style
Kết hợp với nhau thì ta sẽ có được khung chương trình. Để làm chương trình có UI đẹp mắt thì ta dùng Style. Mỗi component đều chấp nhận prop có tên là `style`. Khi số lượng các component t
ăng lên, và trở nên phức tạp hơn thì ta cần tách biệt phần style và component. -> Sử dụng `StyleSheet.create`. Điểm này khá giống css và html. 

### Fixed Dimensions
Có một lưu ý nữa là style trong React Native đều là **unitless**, nên sẽ có kích cỡ giống nhau kể cả với màn hình như thế nào. -> [Device-independent pixel](https://en.wikipedia.org/wiki/Device-independent_pixel)

### Flex Dimensions
Dùng `flex` trong style để khiến component co dãn dựa trên khoảng trống cho phép. Thường ta sử dụng `flex: 1` để khiến component chiếm toàn bộ khoảng trống. Giá trị được đặt của `flex` càng lớn thì tỉ lệ chiếm càng lớn.

Kết hợp với các thuộc tính khác như: `flexDirection`, `alignItems`, `justifyContent`,... là có thể tạo được layout như ý muốn. Tìm hiểu thêm tại [đây](https://facebook.github.io/react-native/docs/flexbox)


## Ví dụ về BlinkApp
Source: https://facebook.github.io/react-native/docs/state#docsNav
```javascript
import React, { Component } from 'react';
import { AppRegistry, Text, View } from 'react-native';

class Blink extends Component {

    componentDidMount(){
    // Toggle the state every second
        setInterval(() => (
          this.setState(previousState => (
            { isShowingText: !previousState.isShowingText }
          ))
        ), 1000);
     }

    //state object
    state = { isShowingText: true };

  render() {
    if (!this.state.isShowingText) {
      return null;
    }

    return (
      <Text>{this.props.text}</Text>
    );
  }
}

export default class BlinkApp extends Component {
  render() {
    return (
      <View>
        <Blink text='I love to blink' />
        <Blink text='Yes blinking is so great' />
        <Blink text='Why did they ever take this out of HTML' />
        <Blink text='Look at me look at me look at me' />
      </View>
    );
  }
}

// skip this line if using Create React Native App
AppRegistry.registerComponent('AwesomeProject', () => BlinkApp);

```

Để tạo một text có hiệu ứng blink thì có một cách là khởi tạo một component mới là `Blink` như trên.

- `componentDidMount()`: hàm này sẽ chạy khi component này load xong.
- `setInterval(functionA, interval)`: hàm này để `functionA` chạy theo chu kỳ là `interval`.



## Tham khảo
- [https://www.oreilly.com/library/view/learning-react-native/9781491929049/ch01.html](https://www.oreilly.com/library/view/learning-react-native/9781491929049/ch01.html)

[facebook_inputfield]: /images/2019-06-27-react-native/facebook_inputfield.png
[react-native-trend]: /images/2019-06-27-react-native/react-native-trend.png