# Chapter 01. 노드에 대해 알아보기

### **노드를 개발한 이유와 문제점**

- 2009년 Ryan Dahl이 개발한 개발 도구
- 당시에 웹 서버에 파일을 업로드할 때면, **업로드가 완료되기 전까지 웹 서버에서 데이터를 조회한다거나 하는 등의 다른 작업을 할 수 없었음**
- 이를 해결하기 위해 새로운 방식의 서버 개발 도구를 만들기 시작하였는데, 그것도 바로 **노드**
- **노드의 대표적 특징** 3가지
  - **비동기 입출력 방식**
  - **이벤트 기반 입출력 방식**
  - **노드의 모듈**

<br></br>

### 비동기 입출력 방식

**비동기 입출력(Non-Blocking IO)의 개념**

- 하나의 요청 처리가 **끝날 때까지 기다리지 않고**, **다른 요청을 동시에 처리**할 수 있는 방식

**동기 입출력(Blocking IO) 방식과의 차이점 비교**

|          비동기 입출력           |                       파일을 읽는 과정                       |           동기 입출력            |
| :------------------------------: | :----------------------------------------------------------: | :------------------------------: |
|            읽기 요청             |                   **파일 시스템에 파일을**                   |            읽기 요청             |
| 대기하지 않고 **다른 작업 진행** | **파일 시스템에서 파일 확인 및 준비 후 처리하는 시간 동안**  | 다른 작업 진행하지 않고 **대기** |
|  자동으로 **콜백 함수**를 호출   | **프로그램이 파일 내용 읽어와 화면에 보여준 후 (파일 처리가 끝났을 때)** | 그제서야 **다른 작업 진행 가능** |

- **콜백 함수(Callback Function)** 
  - **다른 함수의 내부**에서 **어떤 특정한 시점에 호출**되는 함수
  - 보통 콜백 함수는 **함수의 매개변수로 전달**하여 **특정 시점에서 콜백 함수를 호출**

<br></br>

### 이벤트 기반 입출력 방식

**이벤트 기반 입출력(Event driven IO) 모델의 개념**

- 파일 시스템에서 **콜백 함수를 호출**할 때, 파일 시스템이 **이벤트와 함께 호출**하는 방식
- 파일 시스템에서 **파일 읽기가 완료되었다는 이벤트만 전달**하면, 프로그램에서는 **그 이벤트를 받아 콜백 함수를 실행**할 수 있음

**간단한 구현 예시**

```js
http.request(options, function(res) {
    res.on('data', function(chunk) {	// 이벤트를 콜백 함수와 바인딩(Binding)
        console.log('Body :' + chunk);
    });
});
```

- **바인딩(Binding)**
  - **서로 묶어서 연결**해 준다는 의미
  - **이벤트**와 **함수 객체**를 **바인딩**하면, **이벤트가 발생했을 때 등록한 함수 객체가 실행**
  - 위 코드에서, **data라는 이름의 이벤트를 받았을 때 등록한 콜백 함수가 실행**

<br></br>

### 노드를 더 쉽게 사용할 수 있게 하는 모듈

**모듈(Module)의 개념**

- 메인이 되는 **파일의 일부 코드를 떼어 만들어진 별도의 파일**
- **require( ) 함수**로 **모듈을 호출**할 수 있음
- **자바스크립트 객체로 인식**되며, 그 객체를 **참조**하여 **파일에 넣어 둔 기능을 사용**할 수 있음

**모듈을 사용하는 이유**

- 소스 파일 하나에 실행하려는 기능이 **모두** 들어있다면 **코드의 양이 많을 뿐만 아니라 복잡해짐**

- 웹 브라우저에서 사용하는 자바스크립트는 **확장자가 js인 별도의 파일로 만들면, 코드를 분리해서 관리**할 수 있고 **필요할 때 불러서 사용**할 수 있음

- 여러 프로그램에서 **공통으로 사용하는 기능**은 **모듈로 분리하여 구성**하는 것이 일반적

- **npm(Node Package Manager)**

  - **여러 개의 모듈을 합쳐서 하나의 패키지**로 만들어 둔 것을 **npm 프로그램**을 사용하여 **손쉽게 패키지 설치 가능**

  - **다른 프로그래머가 미리 개발하여 올려 둔 패키지**를 찾아 **설치하는 방법을 제공**