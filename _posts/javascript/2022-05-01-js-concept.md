---
layout: post
title: js concept 
description: >

sitemap: true 
categories: 
    - zero-base-javascript 
---

  
# 1. JavaScript 
## 1. 개요 
 : 웹 브라우저 위에서 구동시킬 수 있게 개발된 언어 
 - 자바-  문법
 - 오크- 함수
 - 셀프- 프로토타입 확장 
 - 펄, 파이썬- 문자열, 배열, 정규표현식 
 - 스키마- 일급객체 & 클로저 
 - 하이퍼토크- 브라우저 이벤트 처리 

* EcmaScript: JS(프로그래밍 언어)의 버전 

* Node.js: Chrome V8 JavaScript 엔진으로 빌드된 JavaScript Runtime
    - React Native, Electron으로 활용 
    - Web App, Cross Desktop App, Mobile App 을 만들 수 있음 
    - 서버 개발 가능 
    - => JavaScript EveryWhere   

* 참고: Figma, WebAssembly 

* 공부 방법 
    - 문법
        - 문서: MDN 
        - 구글링
        - 코드 작성 
    - 프로젝트
        - 해설 
        - 구현 

* 참고자료 
    - modern javascript tutorial 
    - java script deep dive (poiemaweb)

 
## 2. 개발환경
- IDE
    - JetBrain + Live Server 
    - VScode + Live Server 
- Node.js + NVM + Brew 
- Browser
    - Chrome 
    - FireFox
    - Safari 
    - Whale 

- Terminal
    - postman 
    - hyper.js 
    - iterms + zsh 

- codesandbox.io 
    : github 연동, ios ipados 등에서도 접근 가능


## 3. DOM (document object model)
- HTML, XML 문서의 프로그래밍 인터페이스  
- DOM 과 JS 
    - 문서의 요소(element; 문서 전체, headm table,..) 에 접근하기 위해 사용 
- DOM 접근 방법 

## 3.  문법 
### 1. 기본 문법 & 키워드 
- Scope: 변수 유효 범위 ; 외부에서 내부로 접근 불가 
    - var: Function Scope
    - let, const: Block Scope 

-  주석 
    - // 
    - /* */ 
    - JS DOC 
    ```js 
    /**
     * Represents book 
     * @constructor 
     *
     * @param {string} title - The title of the book. 
     * @param {string} author - The author of the book. 
     */ 
    function Book(title, author) {

    }
    ```
- 값, 식, 문 
    - value 
    - expression: 값으로 귀결 
    - statement: Interpreter 에게 지시문으로 명령 
    
- 식별자(id; 예약어) 
    - 코드 내 변수, 함수, 속성을 식별하는 문자열 
    - keyword를 식별자로 사용할 수 없음

- 리터럴 
    - 데이터 값 
- use strict 
    : JS 의 느슨한 기본 값을 엄격하게 바꿔준다. 예를 들어, 
        - 무시되던 에러들을 throw 
        - 최적화하여 더 빨리 작동하도록 함 
        - ECMAScript 나중 버전 시맨틱을 적용하지 않게 함

    ```js 

    // use strict 
    function func() {
        'use strict';
        globalVal = 10; 
        console.log(this); 
        return 'hello'; 
    }

    func(); 
    
    ``` 

### 2. value 
- type
    - js: loosely typed language 
    - 타입은 프로그램이 처리되는 과정(런타임)에 자동으로 파악 
    - 같은 변수에 여러 타입 값을 넣을 수 있다. 
    - 구분 
        - Primitive type: 불변, 재할당을 해야 값이 변한다.  
             - undefined 
             - boolean
             - string 
             - number
             - bigint 
             - symbol
             
        - Reference type: 
            - Object 
            - Array 
            - Function 
    
    - undefined vs null 
        - undefined: 선언만 해놓고 값을 대입하지 않은 상태 
        - null: 아무것도 가리키지 않음을 명시적으로 대입해 놓은 상태
        - 명시적 형변환 
            - Number(undefined) // NaN
            - Number(null) // 0 

    - 원시값의 wrapper 객체 ) 
        ```js 
        const bool = false; 
        const num = 123; 
        const str = 'string'; 

        const bool2 = New Boolean(false); 
        const num2 = New Number(123); 
        const str2 = New String('string');

        console.log(typeof bool); // boolean 
        console.log(typeof bool2); // object  

        console.log('string' instanceof String); // false 
        console.log(str instancof String); // true 
        ```
    
    - 형변환 
        -> 명시적 변환을 하자

### 3. Boolean

