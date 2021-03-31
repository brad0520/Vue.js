# Vue.js
## 페이지 소개
- 주소 : [https://to2.kr/cfS](https://to2.kr/cfS)
- 내용 : Web Development with Vue.js
- 공부 Vlog
 
---
## 2021-03-31
### Vue.js란?
  - [Vue.js 공식 홈페이지](https://vuejs.org/)
  - [공식가이드(한국어))](https://kr.vuejs.org/v2/guide/)
  - React, Agular 대비 간결한 프레임워크이자 실행속도가 더 빠름
  - Angular를 이용해 개발을 하던 개발자가 Angular의 불편함을 개선하면서 만들게 된 프레임워크로 학습량이 매우 적고 적용이 쉬움
  
  
---
### Vue.js 세팅
- HTML 파일에 아래의 스크립트 코드로 추가
```js
<script src="https://unpkg.com/vue@next"></script>
```
- 

---
### 1. [Vue 변수 선언](https://codepen.io/NTL-design/pen/KKaNJRj?editors=1010)

- 아래와 같이 html, js 작성

```html
<!-- vue 3.0 불러오기 -->
<script src="https://unpkg.com/vue@next"></script>

<div id="vue-app">
  <!-- 변수는 {{변수명}}의 형식으로 선언 -->
  <!--   변수로 선언된 부분은 정적이 아닌 동적인 부분으로 Vue를 통해 활용 가능 -->
  이름 : {{name}}
  <br>
  나이 : {{age}}
</div>
```

```js
const test = {
  setup() {
    // 변수 선언  
    const name = "Brad";
    const age = 22;
    // 저장한 변수 반환
    return {
      name,
      age
    }
  },
};

// Vue를 통해 HTML의 DOM 요소에 연결됨(mount)
Vue.createApp(test).mount('#vue-app');
```
---
### 2. [Vue 참조 변수 선언](https://www.youtube.com/watch?v=KdV6bI9WGZk)
- Vue.ref(변수) 와 같이 value 값을 입력하면 const로 선언된 변수에도 실시간으로 변동된 값을 반영할 수 있음

- 아래와 같은 코드로 구현 가능 예시
```js
const VueApp = {
  setup() {
    const name = "Brad";
    // Vue.ref를 통해 참조변수로 사용 가능
    const age = Vue.ref(22);
    
    // 인터벌 혹은 지연 시간 설정한 함수 실행 가능
    // Vue.ref로 인해 실시간으로 반영된 다이나믹한 화면 구현 가능
    setInterval(() => {
      age.value = age.value + 1;
    }, 1000);  
    
    return {
      name,
      age
    }
  },
};

Vue.createApp(VueApp).mount('#vue-app');
```

