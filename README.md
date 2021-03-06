# Fokin Weather

Learning React Native by building a Fokin Weather App

### 0.3 Creating the Project

#### installation

- node >= 10.0
- npm >= 6.0
- npm install -g expo-cli

#### project 생성

- expo init fokin-weather

#### execute

- npm start
- localhost:19002 로 실행됨.
- run on iOS simulator를 하면 xCode의 simulator가 실행됨.
- 내 폰에서 실행시키려면?

1. 핸드폰과 컴퓨터가 같은 wifi
2. 핸드폰으로 expo 설치 후 로그인
3. 컴퓨터에서 expo login 으로 로그인
4. qrcode로 들어가기

### 0.4 Getting to know Expo

1. live reloading 변경사항을 저장하면 자동으로 expo와 연결되어있는 기기 앱들을
   refresh해서 변경사항을 바로 반영함

2. hot reloading 수동으로 refresh 하고 싶을 때

- 시뮬레이터 : ctrl+r or ctrl+d(development mode)
- 핸드폰 : 흔들어서 development mode -> restart

* debug remote js : Google developer tools를 사용해 애플리케이션 디버깅을 도와
  줌. 성능 저하됨

### 0.5 How does React Native Work?

- 모바일 자체 기능을 많이 사용하지 않을 때 (ex: 3d 게임, AR 등등)
- 인스타그램처럼 글쓰고 반응하는 작업에 좋음

- StyleSheet API를 사용해서 CSS를 지정할 수 있음
- 하지만 <View>에서 스타일을 지정했다고 View 내부에 있는 <Text>를 수정할 수는
  없음.
- Text도 따로 스타일 지정을 해주자
- 그런데 width를 px 단위로 설정하면 에러 발생함. %로 해줘야 함.

```
text: {
    color: "white"
    width: "100%"
  }
```

### 1.0 Layouts with Flexbox in React Native

- React Native에서 모든 flexbox는 flexDirection이 column이다. 모바일은 세로가
  기니까!
- View는 div 태그 같은 것.
- style={styles.yellowView} 이렇게 하는 대신 style={{flex: 1,
      backgroundColor: "yellow"}} 이렇게 해도 됨
- flex: 1 -> 모든 공간을 다 사용할 수 있음

```
동등한 위치에 있는 view1, view2 2개가 있다고 생각해보자
view1,2 모두 flex: 1이면 모든 공간을 차지해야 하기 때문에 공간을 1/2씩 나누어 가지게 된다. 비율에 따라서 크기가 변함.
```

### 1.1 Loading Screen

- 로딩 화면을 만들어보자(Loading.js)
- Loading.js를 export해서 App.js에서 사용할 수 있게 불러온다
- 변수 하나에 여러 component의 css를 지정해두면 component에서는 변수를 불러오면 되니 편함
- padding 가로 세로로 따로 주고 싶으면 paddingHorizontal, paddingVertical을 사
  용해보자

### 1.2 Getting the Location

- 사용자의 현재 위치를 알아보자
- react native는 geolocation.getCurrentPosition() 을 사용한다
  https://facebook.github.io/react-native/docs/geolocation
- web에서는 navigator.geolocation.getCurrentPosition()로 사용함
- expo에서는 expo-location을 사용함. 더 많은 기능을 갖고 있음
  https://docs.expo.io/versions/v35.0.0/sdk/location/
- 그 중에서도 *Geofencing*이 괜찮아보임
  https://docs.expo.io/versions/v35.0.0/sdk/location/#geofencing
- 어떤 곳에 들어가거나 나올 때 Geofencing API가 App에게 알려줌

1. 먼저 현재 위치를 받아보자

- Location.getCurrentPositionAsync(options); 로 받을 수 있고 Async니까 await로 기다려준다.
- options에는 accuracy, maximumAge가 들어갈 수 있음.
- 하지만 사용자에게 위치 접근 허가를 받아야 함

### 1.3 Asking for Permissions

- permission을 받으려면 Location.requestPermissionsAsync()로 사용자에게 물어보자
- return할 때 permission이 허가되었으면 promise를 리턴하고 거부되었으면 reject을 리턴함
- try - catch로 허가여부 알아보자

### 1.4 Getting the Weather

- weather 서버 API에서 날씨정보를 가져와보자
  https://openweathermap.org/current
- axios로 http request 보내기

```
npm add axios && npm install

import axios from "axios";
```

### 2.0 Displaying Temperature

- 섭씨 표기는 api를 보낼 때 units=metric, 화씨는 units=imperial
- 시뮬레이터의 위치를 바꾸려면 Debug > location > custom location
- 날씨정보를 화면에 보여주자

1. 온도
2. 날씨 아이콘
3. 글씨
4. 배경색

### 2.1 Getting the Condition Names

- 날씨 분류가 어떻게 되는지 문서에서 확인해보자
  https://openweathermap.org/weather-conditions

### 2.2 Icons and Styling

1. Icon

- expo/vector-icons 모듈을 이미 가지고 있음
- 유명한 아이콘들을 갖고 있음
  https://docs.expo.io/versions/latest/guides/icons/#expovector-icons
- icon 개수가 많은 디렉토리(?)를 불러온다(MaterialCommunityIcons)

### 2.3 Background Gradient

1. LinearGradient
   https://docs.expo.io/versions/latest/sdk/linear-gradient/

- 배경색을 그라데이션 주는 효과.
- 가장 바깥 View 대신에 LinearGradient 태그를 주면 됨.

```
$ expo install expo-linear-gradient
```

2. StatusBar

- react native가 지원하는 모듈.
- status bar를 바꾸고 싶을 때 가져오자
- 어느 위치에 넣든 다른 컴포넌트의 위치에 영향을 주지 않는다

```
!! 현재 버전에서는 다크모드를 지원하지 않는다..ㅜㅜ 업그레이드 하자
$ expo upgrade
```

### 2.4 Titles and Subtitles

- UI gradient
  https://uigradients.com/
- title과 subtitle을 왼쪽 정렬하고 싶으면?

```
alignItems: "flex-start"
```
