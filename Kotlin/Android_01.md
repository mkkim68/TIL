# 안드로이드란?
## 정의
- 스마트폰과 태블릿 컴퓨터에서 사용되는 *오픈소스 운영체제*
- 휴머노이드 로봇
- 플랫폼
- 태블릿, 휴대폰, 웨어러블 시계... 기타 등등에서 사용되는 소프트웨어
## Android vs iOS
- 기능적인 공통점은 존재하지만, 호환되지 않은 별개의 운영체제
	- 전화, 인터넷, 카메라 등 동일 기능은 존재하지만 서로 호환 X
- 동일한 기능의 앱이 있으나, Design System이 다르다.
	- Material Design System (Android)
	- Human Interface Guidelines (iOS)
## 특정
- 기본적으로 자바 기반으로 동작, 자바와 완벽 호환되는 kotlin이 이를 대체해 나가고 있음
- 안드로이드 운영체제의 핵심 커널은 리눅스 기반
- 안드로이드 스튜디오를 통해서 개발한다.
- 안드로이드 플랫폼을 탑재한 다양한 제조사의 단말이 출시되고 있음
- Open Handset Alliance
# 안드로이드 플랫폼 구조
## 안드로이드 플랫폼
- Android Developer
	- [https://developer.android.com/?hl=ko](https://developer.android.com/?hl=ko)
- 사용하는 언어들
	- Java: 많이 사용 중
	- Kotlin: 현재 안드로이드에서 주력으로 사용하는 언어
	- React: React Native 프레임워크를 통해 하이브리드(안드로이드, iOS 동시 개발)앱을 만들 수 있음
	- Dart: Flutter 프레임워크를 통해 하이브리드(안드로이드, iOS 동시 개발)앱을 만들 수 있음
## 안드로이드 플랫폼 아키텍처
### Linux Kernel
- 보안, 메모리관리, 프로세스 관리, 파일시스템 관리, 파워 관리, 네트워크 스택, 하드웨어 드라이버 등 하드웨어를 지원
### HAL
- Hardware Abstraction Layer(하드웨어 추상화 계층)
	- 상위 수준의 Java API 프레임워크에 기기 하드웨어 기능을 노출하는 표준 인터페이스를 제공
	- HAL은 여러 라이브러리 모듈로 구성되어 있으며, 카메라 또는 블루투스 모듈과 같은 특정 유형의 하드웨어 구성 요소를 위한 인터페이스를 구현
	- 프레임워크 API가 기기 하드웨어에 액세스하기 위해 호출을 수행하면 Android 시스템이 해당 하드웨어 구성 요소에 대한 라이브러리 모듈을 로드
### Native C/C++ Libraries
- 안드로이드 프레임워크에서 필요한 C와 C++ 라이브러리를 제공
### Android Runtime
- 코어 라이브러리 지원, Dalvik | ART Virtual Machine으로 안드로이드 애플리케이션 실행환경을 제공
### Java API Framework
- 안드로이드 어플리케이션 개발 시 필요한 API를 제공
### System Apps
- Email 클라이언트, SMS 프로그램, 달력, 지도, 브라우저 등의 코어 어플리케이션을 제공
## App Components
### 컴포넌트란?
1. 앱의 구성단위, 컴포넌트 여러 개 조합하여 하나의 앱을 만듦
2. 컴포넌트는 앱 내에서 독립적인 실행 단위
	1. 일반 클래스와 달리 생명주기를 안드로이드 시스템이 관리
	2. 독립적인 실행 단위라는 말은 직접 코드로 결합해서 실행하는 것이 아니라 컴포넌트 간에 Intent라는 특정 클래스를 매개로 하여 결합하지 않은 상태로 실행하는 구조
3. Main 함수 같은 애플리케이션의 진입 지점이 따로 없다
	- 런처의 아이콘을 클릭해서 실행하면, 최초 시작인 경우 메인화면이 보이게 된다.
	- 알림을 눌러서 진입하면, 이때는 해당 알림이 원하는 화면이 보이게 된다.
		- ex. 메신저의 대화창으로 바로
#### 1. Activity
- UI를 구성하기 위한 컴포넌트
#### 2. Service
- UI 없이 백그라운드에서 수행하는 컴포넌트
#### 3. Broadcast Receiver
- 이벤트로 수행되는 컴포넌트(방송을 수신하는 컴포넌트)
- ex. 시스템에 배터리가 부족하거나 시스템 부팅이 완료되는 등의 이벤트가 발생하였을 때 해야 할 작업이 있다면, 이벤트를 수신하는 컴포넌트
#### 4. Content Provider
- 어플리케이션 간 데이터를 공유하기 위한 컴포넌트
## JVM, DVM, ART
### JVM
1. Java Virtual Machine
2. WORA: Write Once and Run Anywhere
![](../241015_1.png)
### DVM
1. Dalvik Virtual Machine
![](../241015_2.png)
2. 초기 Android Run Time, Android 2.2 이후 JIT 컴파일러로 처음 적용되었다.
3. JIT란?
	- Just in time
	- 자주 사용하는 부분에 대해 미리 컴파일하여 기계어로 해석해놓기 때문에 실행 성능을 향상시킬 수 있다
	- 실행시에 인터프리팅 시작
### ART
1. Android Run Time
2. AOT 컴파일러 사용 (Ahead Of Time)
   - 설치 시점에 이미 컴파일을 완료하여 기계어로 해석을 끝냄
   - 실행시에는 해석 과정이 없이 곧바로 기계어로 실행
3. Android 4.4 (API 19)에서 처음으로 등장, 도입 (DVM과 선택적 사용)
4. Android 5.0 (API 21) 이후, 기본 런타임으로 지정
5. Android 7.0 이후로는 AOT + JIT
### DVM vs ART
- DVM: JIT (Just In Time)
	- 앱 실행 시 컴파일
	- 설치 시 컴파일을 하지 않기 때문에 AOT보다 설치 속도 빠름
	- 실행 시 컴파일을 하기 때문에 AOT에 비해 실행 속도 느림
	- 용량 작음
- ART: AOT (Ahead Of Time)
	- 앱 설치 시 컴파일
	- 설치 시 컴파일을 완료하기 때문에 JIT에 비해 설치 속도 느림
	- 실행 시 컴파일을 하지 않기 때문에 JIT에 비해 실행 속도 빠름
	- 용량 큼(미리 컴파일하여 가지고 있기 때문)
## 앱의 폴더와 파일 구조
### 프로젝트 생성
- Name
	- 프로젝트 이름
- Package name
	- 도메인 네임을 거꾸로 뒤집은 네이밍
	- 식별자라 유니크 해야함
- Language
	- Java와 Kotlin 중 하나를 선택
- Minimum SDK
	- 애플리케이션의 동작을 보장하는 최소 SDK
- Build Configuration Language
	- Kotlin DSL이 기본으로 선택됨. 기존은 Groovy로 작성이 기본, 현재는 Kotlin이 추천되고 있음
### 디렉토리 파일 구조
- AndroidManifest.xml
	- 앱의 메인 환경 파일
- MainActivity.java
	- 화면 구성을 위한 액티비티 컴포넌트로 실제 이 파일이 수행되어 화면에 UI가 출력됨
- res
	- 앱의 모든 리소스 파일은 res폴더 하위에 위치
	- res/drawable: 이미지 파일 저장
	- res/layout: UI 구성을 위한 레이아웃 XML 파일
	- res/mipmap: 앱 아이콘 이미지
	- res/values: 문자열 값을 위한 폴더
## Manifest
### Manifext
- AndroidManifest.xml 분석
- \<manifest> 태그 부분
	- manifest 태그를 통해 이 문서가 manifest에 관련된 문서라는 것을 지정
	- 'xmlns:android' 네임스페이스를 선언
	- package 선언: android 33, gradle 8부터는 xml 파일에서 설정이 제거되고, build.gradle 파일에 namespace 항목으로 선언됨
- \<application> 태그 부분
	- 어플리케이션 정보 정의
	- android: allowBackup
		- 백업 및 복구 기능을 사용할 것인가 여부
		- 기본값 true
	- android: icon
		- 어플리케이션 전체를 위한 아이콘과 각각의 컴포넌트를 위한 아이콘
	- android: label
		- 어플리케이션을 나타내는 사용자가 읽을 수 있는 라벨
		- 간단히 말해 어플 이름
	- android: roundIcon
		- 적응형 아이콘 적용
# 안드로이드 Hello World!
# Activity와 Intent