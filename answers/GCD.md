# 문서명

| 질문출처 | 작성자 |
| :------- | :----: |
| JaeSungLee     |  Fomagran  |

## Question

- GCD란 무엇일까요?

## Simple Answer         


## MultiThreading

- 멀티쓰레딩은 여러개의 쓰레드가 동시에 진행되는 것
- GCD는 멀티쓰레딩 처리를 쉽고 편하게 제공하는 API

### MutiThread가 필요한 이유


보통의 작업들은 대표적으로 UI관련 작업들은 메인쓰레드에서 진행된다. 이러한 작업들은 대부분 순차적(sync)으로 이뤄져 있다. 하지만 순서없이 동시(async)에 이뤄져야 할 것들이 있다. 예를 들면 이미지 다운로드같은 경우 동시에 다운로딩을 시작해야 한다. 만약 순차적으로 진행한다면 아주 큰 용량의 이미지가 전에 있다면 뒤의 이미지가 진행조차 되지 않을 것이다. 또한 SNS에서 만약 어떤 유저가 포스트를 올렸는데 그게 화면에 배치될때까지 현재 사용하고 있는 유저가 기다려야 한다면 그 유저는 끊임없이 기다려야 할 것이다. 이것을 해결하기 위해 메인쓰레드와 다른 쓰레드에서 데이터를 불러오는 등의 작업을 실행하고 메인쓰레드에서는 유저가 앱을 사용할 수 있도록 해야 하기 때문에 여러 개의 쓰레드, 즉 멀티쓰레드가 필요하다.

## DispatchQueue

그렇다면 GCD가 이러한 멀티쓰레드를 어떤 식으로 지원해줄까? 바로 DispatchQueue이다. DispatchQueue는 공식 문서에 아래와 같이 정의되어 있다.

<img src="https://user-images.githubusercontent.com/47676921/144369210-adde5122-6bc8-4672-b05f-21e89b3d806e.png"  width="600" height="200">

해석하면 "앱의 메인스레드 또는 백그라운드 스레드에서 작업 실행을 순차적 또는 동시에 관리하는 개체입니다." 라고 되어있다. 즉 DispatchQueue에는 메인스레드와 백그라운드 스레드 2가지 큐가 있는데 순차적으로 작업을 실행하는 Serial Dispatch Queue 가 있고(순차적으로 작업을 한다는 의미는 Queue안에서 순차적으로 실행된다는 뜻이다.)  동시에 작업을 진행하는 Concurrent Dispatch Queue 가 있다. 이 두개의 큐는 다른 말로는 Main Queue와 Global Queue(Background)라고 한다.

## MainQueue   

메인큐의 특징은 아래와 같다.

- 순차적으로 작업이 진행된다.
- 시스템 작동시 자동으로 생성된다.
- UI관련 작업은 메인큐에서 반드시 동작되어야 한다.

## GlobalQueue

- 백그라운드에서 동작한다.
- 작업이 완료되는 시점을 정확히 알지 못한다.
- 메인큐에 동작하는 작업들에 영향을 끼치지 않아야 한다.
- Qos(Qulity Of Service)를 이용해 우선순위를 정할 수 있다.

### Qulity Of Service

Qos는 아래처럼 우선 순위에 따라 5가지로 사용할수 있다.

1.Userinteractive - 바로 수행되어야 할 것 (가장 중요한 것)

2.Userintiated - Userinteractive보단 덜 중요하지만 사용자가 기다리고 있는 것

3.Userdefault - 우선 순위를 신경쓰지 않는 것(중요한 정도가 상관없는 것)

4.Utility - 시간이 좀 걸려서 오래 걸리는 것

5.background - 사용자한테 당장 인식될 필요가 없는 것
