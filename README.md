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
