DOIT Vue.js 책을 기반으로 공부한 내용입니다.


# Vue.js란?
> 웹 페이지 화면을 개발하기 위한 프런트엔드 프레임워크

- Angular의 데이터 바인딩 특성과 React의 Virtual DOM 기반 렌더링 특징을 모두 가지고 있다.

## MVVM 패턴
> 마크업 언어나 GUI 코드를 비즈니스 로직 또는 백엔드 로직과 분리하여 개발하는 소프트웨어 디자인 패턴

- 화면을 'Model-View-ViewModel'로 구조화하여 개발
  - Model: 데이터를 담는 용기. 보텅은 서버에서 가져온 데이터를 자바스크립트 객체 형태로 저장 (Javascript Object)
  - View: 사용자에게 보이는 화면 (DOM)
  - ViewModel: 뷰와 모델의 중간 영역. 데이터 바인딩(View에 표시되는 내용과 Model의 데이터를 동기화)을 제공하는 영역 (Vue.js)
- 프론트엔드의 화면 동작과 관련된 로직과 백엔드의 데이터베이스 데이터 처리 로직을 분리하여 깔끔하게 코드 구성을 가능하게 해 줌



# Component
> 조합하여 화면을 구성할 수 있는 블록

- 코드를 재사용하기 쉽다
- HTML 코드에서 화면의 구조를 직관적으로 파악할 수 있다.
- 컴포넌트는 각각 고유한 유효 범위를 가지고 있기 때문에 직접 다른 컴포넌트의 값을 참조할 수 없다. 때문에 뷰 프레임워크 자체에서 정의한 컴포넌트 데이터 전달 방법을 따라야 한다.
  - 상위 컴포넌트 -> 하위 컴포넌트: props(속성) 전달
  - 하위 컴포넌트 -> 상위 컴포넌트: 이벤트 발생(이벤트만 전달 가능)

## props 속성
하위 컴포넌트의 props 속성 정의
```javascript
Vue.component('child-component', {
  props: ['props 속성 이름']
})
```
상위 컴포넌트의 HTML코드에 등록된 child-component 태그에 v-bind 속성 추가
```javascript
<child-component v-bind:props 속성 이름="하위 컴포넌트에 전달할 상위 컴포넌트의 data 속성"></child-component>
```

## 이벤트 발생과 수신
```javascript
this.$emit('이벤트명')  // 이벤트 발생
<child-component v-on:이벤트명="상위 컴포넌트의 메서드명"></child-component>  //  이벤트 수신

```



# Vue Instance
> Vue로 화면을 개발하기 위해 필수적으로 생성해야 하는 기본 단위

## 뷰 인스턴스 생성
```javascript
new Vue({  // Vue 인스턴스
  el: '#app'  // el 속성
  data: {
    message: 'Hello Vue.js!'  // data 속성
  }
})
```

## 뷰 인스턴스 옵션 속성
- el: 뷰로 만든 화면이 그려지는 시작점
- template: 화면에 표시할 HTML, CSS 등의 마크업 요소를 정의
- methods: 화면 로직 제어와 관계된 메서드 정의
- created: 뷰 인스턴스가 생성되자 마자 실행할 로직 정의
- computed: 데이터 속성 값의 변화에 따라 자동으로 다시 연산, 캐싱

### methods와 computed의 차이
#### methods
- 호출할 때만 해당 로직이 수행
- 수행할 때마다 연산을 하기 때문에 캐싱 X
#### computed
- 대상 데이터 값이 변경되면 자동으로 수행
- 데이터가 변하지 않는 한 이전 계산 값을 가지고 있다가(캐싱) 필요할 때 바로 반환

## 뷰 인스턴스 라이프 사이클
> 인스턴스의 상태에 따라 호출할 수 있는 속성들


인스턴스의 생성 -(created)-(mounted)- 생성된 인스턴스를 화면에 부착 -(updated)- 부착된 인스턴스 내용의 갱신 -(destroyed)- 인스턴스 제거(소멸)

### 라이프 사이클 훅
> 각 라이프 사이클 속성에서 실행되는 커스텀 로직(개발자가 임의로 작성한 추가 로직)



# 뷰 라우터
> 뷰에서 라우팅 기능을 구현할 수 있도록 지원하는 라이브러리

## 라우팅
> 웹 페이지 간의 이동 방법

- SPA(Single Page Application)에서 주로 사용
- 깜빡거림 없이 화면을 매끄럽게 전환 가능 (사용자 경험 향상)

```javascript
<router-link to="URL 값">  // 페이지 이동 태그
```
- 화면 상에서 `<a>` 버튼 태그로 변환되어 표시
- 버튼을 클릭하면 to=""에 정의된 텍스트 값이 브라우저 URL 끝에 추가

```javascript
<router-view>  // 페이지 표시 태그
```
- 갱신된 URL에 해당하는 화면을 보여주는 영역
- 나타낼 화면은 `<script>`에서 정의



# 뷰 HTTP 통신

## 웹 앱의 HTTP 통신 방법
### ajax
> 서버에서 받아온 데이터를 표시할 때 화면 전체를 갱신하지 않고도 화면 일부분만 변경할 수 있게 하는 자바스크립트 기법

## 뷰 앱의 HTTP 통신 방법
### axios
> ajax를 지원하기 위한 라이브러리

- Promise(비동기 로직 처리에 유용한 JS 객체) 기반의 API 형식이 다양하게 제공됨
  - 데이터를 요청하고 받아올 때까지 기다렸다가 화면에 나타내는 로직을 실행해야 할 때 주로 사용

```javascript
axios({
  method: 'get',
  url: 'URL 주소',
  ...
})
```



# 뷰 템플릿
> HTML, CSS 등의 마크업 속성과 뷰 인스턴스에서 정의한 데이터 및 로직을 연결하여 사용자가 브라우저에서 볼 수 있는 형태의 HTML로 변환해 주는 속성

## 템플릿에서 사용하는 뷰의 속성과 문법
### 데이터 바인딩
> HTML 화면 요소를 뷰 인스턴스의 데이터와 연결

- {{}}: 뷰 인스턴스의 데이터를 HTML 태그에 연결하는 기본적인 텍스트 삽입 방식
- v-bind: id, class, style 등 HTML 속성(attribute)값에 뷰 데이터 값을 연결할 때 사용되는 데이터 연결 방식 
  - `v-bind:`를 `:`로 간소화 가능

### 디렉티브
> HTML 태그 안에 v- 접두사를 가지는 모든 속성

- 화면의 요소를 더 쉽게 조작하기 위해 사용하는 기능
- `v-if` : 지정한 뷰 데이터 값의 참/거짓 여부에 따라 해당 HTML 태그를 화면에 표시
- `v-for` : 지정한 뷰 데이터의 개수만큼 HTML 태그 반복
- `v-show` : 데이터의 진위 여부에 따라 화면에 표시 (false인 경우 태그를 완전 삭제하는 `v-if`와는 `v-show`는 CSS 효과만 `display:none`으로 바뀜 )
- `v-bind` : HTML 태그의 기본 속성과 뷰 데이터 속성을 연결
- `v-on` : 화면 요소의 이벤트를 감지하여 처리할 때 사용
- `v-model` : form에서 주로 사용 / 폼에 입력한 값을 뷰 인스턴스의 데이터와 즉시 동기화


---
# 용어 정리

### 프레임워크
> 개발자들의 개발 생산성을 높이기 위해 일정한 틀과 규칙에 따라 개발하도록 미리 구조를 정의해 둔 도구

### 라이브러리
> 자주 사용되는 기능들을 모아 재활용할 수 있도록 정리한 기술 모음집

### DOM
> HTML 문서에 들어가는 요소(태그, 클래스, 속성 등)의 정보를 담고 있는 데이터 트리

### SPA (Single Page Application)
> 페이지를 이동할 때마다 서버에 웹 페이지를 요청해 새로 갱신하는 것이 아니라 미리 해당 페이지들을 받아 놓고 페이지 이동 시에 클라이언트의 라우팅을 이용해 화면을 갱신하는 패턴을 적용한 어플리케이션

### HTTP (HyperText Transfer Protocol)
> 브라우저와 서버 간에 데이터를 주고받는 통신 프로토콜

- 브라우저에서 특정 데이터를 보내달라고 요청(request)하면 서버에서 응답(response)으로 해당 데이터를 보내주는 방식

### 프로토콜
> 컴퓨터나 단말기 간에 통신하기 위해 상호간에 정의한 규칙

### 캐싱
> 데이터나 값을 임시 장소에 미리 복사해 놓는 동작

- 데이터에 접근하는 시간이나 값을 다시 계산하는 시간이 오래 걸릴 때 미리 임시 저장소에 저장하고 필요할 때 바로 불러올 수 있어 수행 시간이 빠름

### SFC (Single File Components)
> .vue 파일로 프로젝트 구조를 구성하는 방식

### CLI (Command Line Interface)
> 커멘드 창에서 명령어로 특정 동작을 수행할 수 있는 도구