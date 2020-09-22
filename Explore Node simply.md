# Chapter 02. 노드 간단하게 살펴보기

### 전역 객체(Global Object)

**종류**

- **console** : 콘솔 창에 결과를 보여주는 객체
- **process** : 프로세스의 실행에 대한 정보를 다루는 객체
- **exports** : 모듈을 다루는 객체

<br/>

### 콘솔에 로그 뿌리기

**console 객체**

  - **dir(object)** : 자바스크립트 객체의 속성들을 출력

    ```javascript
    var Person = {name:"Jaeyoung", age:21}
    console.dir(Person)
    
    // {name: 'Jaeyoung', age: 21} 로 출력
    ```

  - **time(id)** : 실행 시간을 측정하기 위한 시작 시간을 기록

  - **timeEnd(id)** : 실행 시간을 측정하기 위한 끝 시간을 기록

    ```javascript
    // 시간이 얼마나 지났는지 체크하는 작업에 하나의 이름을 붙여 구별함
    console.time('duration_sum'); // Parameter: String
    console.timeEnd('duration_sum');
    ```

**전역 변수(Global Variable)**

- **__filename** : 실행한 파일의 이름을 출력 (파일의 전체 Path가 출력)
- **__dirname** : 실행한 파일이 들어 있는 폴더를 출력 (폴더의 전체 Path가 출력)

<br/>

### 프로세스 객체 간단하게 살펴보기

**process 객체**

- **argv** : 프로세스를 실행할 때 전달되는 Parameter 정보 (배열 객체)

  ```
  첫 번째 Parameter : 자바스크립트 파일을 실행하기 위해 사용한 node.exe 파일의 이름
  두 번째 Parameter : 자바스크립트 파일의 Path
  ```

- **env** : 환경 변수 정보

  ```
  사용자 PC의 모든 환경 변수 값이 출력 가능
  ```

- **exit( )** : 프로세스를 끝내는 메소드

<br/>

### 노드에서 모듈 사용하기

**모듈(Module)의 개념**

- 한 시스템에서 분리된 여러 개의 기능적 구성 요소

- 메인 파일에서 분리된 파일을 노드에서는 모듈이라고 부름
- 별도의 파일로 분리된 독립 기능의 모음

**사용법**

- **exports 전역 객체** 사용

  - exports 객체의 속성으로 변수나 함수를 지정하면 그 속성을 main.js와 같은 메인 자바스크립트 파일에서 불러와 사용 가능
  - 모듈을 불러올 때는 require( ) 메소드를 사용 (Parameter: 파일의 이름)

- **module.exports** 사용

  - **exports**에는 속성을 추가할 수 있음 (여러 개의 변수나 함수를 각각의 속성으로 추가 가능)

    ```javascript
    exports.add = function(a,b) {
    	return a+b;
    }
    ```

  - **module.exports**는 하나의 변수나 함수 또는 객체를 직접 할당

    ```javascript
    var calc = {};
    
    calc.add = function(a,b) {
    	return a+b;
    }
    
    module.exports = calc;
    ```

- **둘의 차이점?? (아직 완벽히 이해하진 못함)**

  - https://programmingsummaries.tistory.com/340

**외장 모듈 사용하기**

1. **npm (Node Package Manager)**

   - 노드의 패키지를 사용할 수 있도록 설치 및 삭제 등을 지원하는 프로그램

2. **node_modules**

   - npm으로 설치한 외부 패키지들이 위치한 폴더
   - npm install ~ 을 사용하면 생기는 폴더
   - 모든 프로젝트에 적용하고 싶다면, 프로젝트의 상위 폴더로 옮겨서 설치하면 됨

3. **package.json**

   - 설치한 패키지들의 정보를 담을 수 있는 곳

   - 해당 프로젝트에서 사용한 모듈을 다른 PC에서 그대로 사용하고 싶다면 package.json 파일만 다른 PC로 옮긴 후

     ```
     npm install
     ```

     이라는 명령어를 입력하면 그 안에 들어있는 모든 패키지가 한꺼번에 설치됨

     (이는 package.json 내에 "dependencies" 속성의 값을 참조하여 패키지를 설치해줌)

   - npm 설치를 위한 --save 옵션은, 자동으로 dependencies 내부에 패키지를 포함하여 저장하도록 지시해주는 옵션

**내장 모듈 사용하기**

**개념**

- 자주 사용하는 기본 기능을 노드에 미리 포함시켜 제공하는 것 (바로 사용 가능)
- 개발자가 직접 만들어 올린 모듈은 **외장 모듈** (이는 npm으로 설치해야 함)
- os 모듈과 path 모듈이 존재

**1. os 모듈**

- 시스템에 대한 정보를 알려줌 (CPU나 메모리 또는 디스크 용량)
- 종류
  - **hostname( )** : 운영체제의 호스트 이름
  - **totalmem( )** : 시스템의 전체 메모리 용량
  - **freemem( )** : 시스템에서 사용 가능한 메모리 용량
  - **cpus( )** : CPU 정보
  - **networkInterfaces( )** : 네트워크 인터페이스 정보를 담은 배열 객체 반환

**2. path 모듈**

- 파일 Path를 다룸
- 종류
  - **join( )** : 여러 개의 이름들을 모두 합쳐 하나의 파일 Path로 만들어줌 (완성할 때 구분자 등을 알아서 조정)
  - **dirname( )** : 파일 Path에서 directory 이름을 반환
  - **basename( )** : 파일 Path에서 파일의 확장자를 제외한 이름을 반환
  - **extname( )** : 파일 Path에서 파일의 확장자를 반환