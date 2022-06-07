# 자바 개요

## 목차

1. [자바란?](#자바란)
2. [자바의 사용](#자바의-사용)
3. [자바의 특징](#자바의-특징)

## 자바란?

자바 오크(Oak)라는 언어로부터 탄생된 언어다. 오크는 가전제품에 탑재되어 네트워크를 통해 신규 프로그램을 다운받아 기능을 향상시키는 개념에서 시작된 언어이다. 그러나 등장 직후 별다른 관심을 끝지 못하고 있었으나, 1990년대 중반 WWW가 등장하면서 변환점을 맞는다. 클라이언트-서버 형태로 작동하는 WWW가 오크 언어의 기본 개념과 같은 다운로드 기능을 제공하는 서비스였기 때문에, 썬 마이크로시스템즈는 오크 언어를 WWW에 적용하기 위한 작업을 시작했고, 오크 언어를 커피의 속어인 자바(Java) 언어로 이름을 바꾼다.

자바 언어는 **C/C++에서 어렵게 사용되는 포인터나 메모리 조작 등의 개념을 과감하게 제거하거나 개선**했다. 또한 **신뢰성을 증대시키기 위해 예외 처리 기능을 효율적으로 제공하여 예상치 못한 오류 등을 처리하는 방법을 제공**한다.

## 자바의 사용

1996년 자바의 공식 버전이 패보된 이후, 자바 언어의 사용이 급속하게 확대되었는데, 이에 썬 마이크로시스템즈에서는 자바를 3가지 종류의 플랫폼으로 제공하기 시작했다.

- Java ME(Mobile Edition) : 스마트폰 등 소형 기기를 위한 개발 환경.
- Java SE(Standard Edition) : 클라이언트 중심의 일반적인 자바 응용 프로그램 개발 환경.
- Java EE(Enterprise Edition) : 서버 중심의 기업용 소프트웨어 개발 환경.

## 자바의 특징

자바 백서에 기술된 '**11가지 자바의 특징**(혹은 언어 설계 목표)'에 따르면 자바는 다음과 같은 특징들을 가진다.

1. 단순함(Simple)

   - 자바는 C++에서 유래했지만 포인터, 다중 상속, 연산자 중복과 같이 까다롭고 **혼란을 일으킬 수 있는 요소들은 제거**하고 꼭 필요한 기능만 포함시켰다.

2. 객체 지향적(Objected-Oriented)

   - 자바는 처음부터 객체지향적 언어로 설계되었다. 그에따라 객체지향적 언어라면 제공해야 하는 **추상화(Abstraction)**, **상속(Inheritance)**, **다형성(Polymorphism)** 등과 같은 특성들을 모두 완벽하게 지원한다.

3. 분산 환경에 적합(Distributed)

   - 자바는 인터넷/네트워크를 통해 효율적으로 수행될 수 있도록 설계되었다. **HTTP**, **FTP**, **TCP/IP 프로토콜** 등 네트워크와 관련된 라이브러리를 기본으로 제공하며, 타 컴퓨터에 있는 원격 객체들을 호출할 수 있는 **RMI(Remote Method Invocation)** 기능을 제공한다.

4. 견고(Robust)

   - 자바는 한 번 작성된 코드가 다양한 컴퓨터에서 실행되어야 하기에 **높은 신뢰성**이 요구된다. 높은 신뢰성을 유지하기 위해서 다음과 같은 특성들을 가지게 된다.
     - No Pointer  
       포인터는 메모리 접근이 자유롭게 하지만 오류 발생 빈도를 높이기도 하므로 이를 제거했다.
     - Automatic Garbage Collection  
       자동으로 메모리 해지를 수행한다.
     - Strict Type Checking  
       컴파일/런타임 시 클래스 타입의 체크가 가능하여 클래스 단위로 동작하는 자바에서 오류 파악이 수월하다.
     - Runtime Error Processing  
       예외처리 기능을 의미한다.

5. 컴퓨터 구조에 중립

   - 자바는 서로 다른 네트워크 환경에서 분산 실행될 수 있도록 설계되었기 때문에 여러 플랫폼에서 실행될 수 있도록 **구조 중립적인 중간 코드**를 생성한다.
   - 자바는 컴파일 시 소스 코드를 자바 바이트코드로 변환하는데, 이는 **자바 가상 머신**(JVM)에서 실행되기 위한 이진 파일로, 플랫폼에 구애받지 않고 독립적이다.
   - 따라서 **JVM을 설치할 수 있는 환경이라면, 어디에서나 자바 프로그램을 실행할 수 있다.**

6. 안전(Secure)

   - 자바는 네트워크 환경에서 작업하도록 만들어진 언어이기 때문에 그만큼 보안성에 중점을 두고 있다.
   - **메모리에서 데이터 접근 제한이 가능**하여, 허가 없이 앱의 데이터에 접근하는 것을 방지할 수 있다.

7. 이식성(Protable)

   - C, C++과는 달리 구현 환경에 따라 달라지는 자료의 크기가 없다.  
     예시) int 자료형의 크기 - C/C++ : 상황에 따라 16bit or 32bit, Java : 항상 32bit
   - 이는 자바 실행 환경이 JVM으로 동일하기 때문이다. 덕분에 다른 CPU, 다른 환경에서 같은 코드를 사용할 수 있다.

8. 인터프리트 언어(Interpreter)

   - 자바로 작성된 프로그램은 중간 언어 형태인 자바 바이트코드로 컴파일된 후, 이를 자바 인터프리터가 한 줄씩 해석함으로써 프로그램이 실행된다.
   - 이러한 방식 덕분에 자바 인터프리터와 런타임 시스템이 이식된 모든 플랫폼에서 자바 바이트 코드를 직접 실행할 수 있다.
   - 자바는 인터프리터 기능이 있는 **컴파일러 언어**이다.

9. 높은 수행성능(High Performance)

   - 자바는 인터프리터가 런타임 환경을 검사할 필요 없이 실행될 수 있도록 구성되었기 때문에 뛰어난 성능을 제공한다.
   - 먼저 언급한 **가비지 컬렉터**(GC)가 자동으로 낮은 우선순위의 백그라운드 스레드로 실행되어 메모리가 필요할 때에만 작동하도록 관리해 줌으로써 자바 가상 머신(JVM)에 무리를 주지 않도록 하며, 보다 나은 수행 성능을 제공한다.
   - JVM에 무리를 줄만한 방대한 양의 계산을 수행하는 프로그램이 실행되는 경우, **고부하 작업을 담당하는 부분을 본래의 플랫폼(Windows, Linux 등)에 해당하는 기계어 코드로 재작성하여 실행**한 후, 자바 프로그램과 상호작용 할 수 있도록 했다.

10. 다중 스레드 지원(Multithreaded)

    - 자바는 프로그래밍 언어 안에서 여러 작업을 동시에 실행하는 '다중 스레딩'을 지원한다.
    - 자바가 제공하는 API에는 스레드를 지원하기 위한 Thread 클래스가 존재하며, 자바 런타임 시스템(자바 실행 환경)에서는 모니터와 조건 잠금 함수를 제공한다.

11. 동적(Dynamic)

    - 자바는 인터넷과 같이 동적으로 변화하는 환경에 적응하도록 설계됐다.
    - 기존의 C/C++ 기반 프로그램은 라이브러리가 변경되면 소스 파일들을 다시 컴파일, 링크하여 신규 실행 파일을 생성해야 했으나 자바는 **실행되기 직전에 필요한 라이브러리를 필요할 때 불러와서 적재**할 수 있다. 이것을 **동적 로딩**이라 한다.

# 참고 서적/문서

- 알기 쉽게 해설한 Java 8th edition - 김충석 저
- [0 \_2. 자바의 특징](https://j4bez.tistory.com/5)