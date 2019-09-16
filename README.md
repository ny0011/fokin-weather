# Fokin Weather

Learning React Native by building a Fokin Weather App

### 0.3 Creating the Project

#### installation

- node >= 10.0
- npm >= 6.0
- npm install -g expo-cli

#### project 생성

- expo init fokin-weather

```
blank, yes
```

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

1. live reloading
   변경사항을 저장하면 자동으로 expo와 연결되어있는 기기 앱들을 refresh해서 변경사항을 바로 반영함

2. hot reloading
   수동으로 refresh 하고 싶을 때

- 시뮬레이터 : ctrl+r or ctrl+d(development mode)
- 핸드폰 : 흔들어서 development mode -> restart

* debug remote js :
