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
### 1. [변수 선언](https://codepen.io/NTL-design/pen/KKaNJRj?editors=1010)

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
### 2. [참조 변수 선언](https://www.youtube.com/watch?v=KdV6bI9WGZk)
- Vue.ref(변수) 와 같이 value 값을 입력하면 const로 선언된 변수에도 실시간으로 변동된 값을 반영할 수 있음
- 참조변수로 선언된 변수의 값을 사용하기 위해서는 변수.value와 같이 사용해야함
 
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

---
### 3. [Computed](https://www.youtube.com/watch?v=sxFpRUARP2s)

- 다른 변수값에 따라 값이 달라지는 변수의 경우 computed를 활용해서 자동으로 반영된 값을 산출하고 웹에 전달 가능

- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/GRrNLmZ?editors=1010)


---
### 4. [속성 바인딩](https://www.youtube.com/watch?v=nYWwO1evj_U)

- HTML 태그 안의 속성에 바인딩 할 경우 {{}}가 아닌 : 을 사용하여 바인딩하며, 바인딩된 부분의 코드는 자바스크립트로 인식하기에 자바스크립트 코드로 작성해야함.


```html
<!-- vue 3.0 불러오기 -->
<script src="https://unpkg.com/vue@next"></script>

<div id="vue-app">
  이름 : {{name}}
  <br>
  <!-- 태그 내의 속성과 직접 바인딩을 할 경우에는 : 을 사용하여 입력 -->
  나이 : <span :title="introduceMsg">{{age}}</span>
  <br>
  <!-- : 로 바인딩된 상태에서 ""안의 내용은 JavaScript 코드로 인식하기에 그에 맞게 작성 필요 -->
  나이 : <span :title="name + '의 나이는 ' + age + '살 입니다.'">{{age}}</span>
  <br>
  성년 : {{isAdult}}
  <br>
  소개 : {{introduceMsg}}
</div>
```

- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/MWJbREX?editors=1010)




---
### 5. [속성 바인딩 응용](https://www.youtube.com/watch?v=a6IcdC2HQHU)

- 이미지 링크 등에도 바인딩하여 다이다믹한 효과 구현 가능
- jQuery에 비해 간결한 코딩이 가능

- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/QWdGPJm?editors=1010)


---
### 6. [스타일 바인딩](https://www.youtube.com/watch?v=bA_oPnHW1yY)

- CSS 스타일 적용을 태그에 바로 적용함에 있어 불편함을 바인딩을 통해 css소스코드를 편집하 듯이 할 수 있음
- 웹 구성 요소들을 제어하는데에 있어 제이쿼리보다 편리함

```js
    // imgStyle 변수의 값으로 css 스타일 속성을 제어
    const imgStyle = Vue.ref({});
    
    imgStyle.value = {
      display:'block',
      boxShadow:"10px 10px 10px black",
      border:"10px solid green"
    };
    
    setInterval(() => {
      const msg = imgUrlCount % 2 == 1 ? 'Hello' : 'World';
            
      imgUrl.value = 'https://via.placeholder.com/150?text=' + msg;
      
      imgStyle.value.borderColor = imgUrlCount % 2 == 1 ? 'gold' : '';
 ```     

 - [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/vYgywGm)
 
 
 ---
### 7. [클래스 바인딩](https://www.youtube.com/watch?v=oHsNAtog778)

- HTML class를 Vue를 통해 바인딩 하여 제어 가능
- 이벤트 핸들링에서 제이쿼리 대비 직관적이고 가독성이 높은 코딩 가능

- HTML 코드

```html
<div id="vue-app">
  <!--  add, reomve class를 사용하지 않아도 Vue로 클래스 추가, 삭제 구현 가능 : 클래스 바인딩  -->
  <img :src="imgUrl" :class="imgClass" alt="">
  <hr>
  
  <!--  @click으로 onclick구현 / 이벤트 실행 코드가 제이쿼리보다 간결하고 보다 직관적임  -->
  <button @click="activeRed">red</button>
  <button @click="activeBlue">blue</button>
  <button @click="inactiveAll">inactiveAll</button>
</div>
```
- JS 코드(Vue.js)

```js
    const imgClass = Vue.ref();
    
    // 아래의 코드는 red, blue 클래스의 초기화로 사용
    // 주석처리하면 이후 코드가 실행이 되지 않음
    // 초기화가 아래와 같이 필요함
    imgClass.value = {
      red:false,
      blue:false
    };
    
    const activeRed = () => {
      imgClass.value.red = true;
      imgClass.value.blue = false;
    };
    
    const activeBlue = () => {
      imgClass.value.red = false;
      imgClass.value.blue = true;
    };
    
    // 제어하는 클래스가 다수인 경우 for문을 사용하는 것이 효율적임(필수 체크!!!)
    const inactiveAll = () => {
      for ( let key in imgClass.value ) {
        imgClass.value[key] = false;
      }
      // 위 코드와 아래 코드는 같은 의미
      // imgClass.value.red = false;
      // imgClass.value.blue = false;
    };
```

 - [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/qBRqGoR)
