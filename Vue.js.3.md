# Vue.js 3.0
## 페이지 소개
- 주소 : [https://to2.kr/cfS](https://to2.kr/cfS)
- 내용 : Web Development with Vue.js
- 공부 Vlog
- [참고동영상](https://www.youtube.com/watch?v=qZXt1Aom3Cs)

---
## 2021-03-31
### Vue.js란?
  - [Vue.js 공식 홈페이지](https://vuejs.org/)
  - [공식가이드(한국어))](https://kr.vuejs.org/v2/guide/)
  - React, Agular 대비 간결한 프레임워크이자 실행속도가 더 빠름
  - Angular를 이용해 개발을 하던 개발자가 Angular의 불편함을 개선하면서 만들게 된 프레임워크로 학습량이 매우 적고 적용이 쉬움
  
  
## 강의자료를 통한 학습

### Vue.js 세팅
- HTML 파일에 아래의 스크립트 코드로 추가
```js
<script src="https://unpkg.com/vue@next"></script>
```


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

```
    // computed를 활용하여 참조하는 값의 변화가 자동으로 결과값에 반영이 되도록 할 수 있음
    const isAdult = Vue.computed(() => age.value >= 20);
```
     
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

```vue
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
 
 
   ---
### 8. [v-show, v-if](https://www.youtube.com/watch?v=u1DtRdKyCRI)

- v-show : 클릭 이벤트에 보여주고, 숨기는 기능은 매우 비번하게 구현되기에 아예 간단하게 구현가능한 방법으로 제공
- 이벤트 대상 객체에 v-show = "imgVisible"(변경 가능) 을 태그에 입력
- @click="imgVisible = true;" /  @click="imgVisible = true;" 를 버튼 기능을 하는 태그에 입력하여 간단하게 구현
- 이 둘의 가장 큰 차이점은 우선 v-if는 조건에 따라 컴포넌트가 실제로 제거되고 생성됨
- 반면에 v-show 는 단순히 css 의 display 속성만 변경됨
- v-if : v-show는 디스플레이 속성을 none으로 숨기지만, v-if는 대상 컴포넌트를 삭제하여 숨겨진 상태에서는 해당 요소를 찾기 힘듬
- v-else : v-if와 함께 if 문 처럼 활용할 수 있음
- 아래의 예시와 같이 이미지가 숨겨졌을 때 텍스트가 보여지게 구현이 가능
- 여러 가지로 응용이 가능하며 제이쿼리 대비 메뉴 클릭 이벤트에서 작동하는 기능 구현이 수월할 듯함

  - 구현된 예시)

```vue
<div id="vue-app">
  <h1>v-show</h1>
  <button @click="imgVisible = true;">보여주기</button>
  <button @click="imgVisible = false;">숨기기</button>
  <hr>
  <img v-show="imgVisible" :src="imgUrl" alt="">
  
  <h1>v-if</h1>
  <button @click="imgVisible = true;">보여주기</button>
  <button @click="imgVisible = false;">숨기기</button>
  <hr>
  <img v-if="imgVisible" :src="imgUrl" alt="">
  <span v-else>{{imgUrl}}은(는) 숨겨짐</span>
</div>
```

- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/WNRRerK)
 
 
---
### 9. [v-for](https://www.youtube.com/watch?v=7UcHGmy2RhU)

- HTML 내에서 for문을 구현 가능 : v-for = "i in number" 사용
  - HTML 코드

```html
<div id="vue-app">
  <input :value="dan" ref="inputNumElRef" type="number" placeholder="구구단">
  <button @click="changeDan" type="button">출력</button>
  
  <div v-for="i in 9">
    {{dan}} * {{i}} = {{dan * i}}
  </div>
</div>
```

  - Vue 코드

```vue
const VueApp = {
  setup() {
    const inputNumElRef = Vue.ref();
    const dan = Vue.ref(5);
    
    const changeDan = () => {
      const inputNum = inputNumElRef.value;
      inputNum.value = inputNum.value.trim();
      
      if ( inputNum.value.length == 0 ) {
        alert('숫자를 입력해주세요.');
        inputNum.focus();
        return;
      }
      
      dan.value = inputNum.value;
    }
    
    return {
      inputNumElRef,
      changeDan,
      dan
    }
  }
};

const vueApp1 = Vue.createApp(VueApp).mount('#vue-app');
```

- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/bGggeZE)

 
---
### 10. [@input](https://www.youtube.com/watch?v=cE_vJb0TNbU)

- 입력값을 입력과 동시에 반영하는 @input 사용
- 입력값을 받는 변수는 $event.target.value 활용
- v-if 와 v-for 를 함께 사용이 가능
- v-for="i in 9" 에서 i는 1부터 9까지 사용되고, index를 지정할 경우는 0부터 8까지 사용됨

```html
<div id="vue-app">
  <!-- 입력값을 입력과 동시에 반영하는 @input 사용 -->
  <!-- 입력값을 받는 변수는 $event.target.value 활용 -->
  <input @input="dan = $event.target.value" :value="dan" type="number" placeholder="구구단">
  
  <div v-if="!isNaN(dan) && dan > 0" v-for="i in 9">
    {{dan}} * {{i}} = {{dan * i}}
  </div>
</div>
```


- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/wvggEXJ?editors=1010)

  
---
### 11. [@v-model](https://www.youtube.com/watch?v=l186Miv6o4c)

- v-model : 10강의 v-input을 더욱 간편하게 구현하는 방법
- Vue는 양방향 데이터 바인딩이 가능함
- 콘솔에서의 데어터 변화값이 뷰에 반영이 됨
- 뷰의 데이터를 콘솔에서 확인이 가능
- option과 label 등에서도 동일하게 구현 가능
- 범위를 지정할 때는 최대, 최솟값을 지정하기

```
    <label style="display:block;" v-for="(i, index) in inputMaxDan" :key="index">
      <span>{{i}} 단</span>
      <input v-model="dan" type="radio" name="dan" :value="i">
    </label>
  </div>
  <select v-model="dan">
    <option :value="i" v-for="(i, index) in inputMaxDan" :key="index">{{i}} 단</option>
  </select>
  <input v-model="dan" type="number" min="1" pattern="\d*" placeholder="구구단">
```

- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/KKaaxjR)


---
### 12. [컴포넌트 정의](https://www.youtube.com/watch?v=Ue9cLEgoW6o)

- 반복되어 사용되는 코드를 재활용하는 방법
- 클래스에 적용하여 css코드를 묶어서 사용하는 방법 대비 구성 요소의 변화도 쉽게 반영할 수 있는 이점이 있음
- 아래의 코드를 통해 3가지 버전의 차이점을 확인 가능

- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/BappqpJ)


---
### 13. [컴포넌트, props](https://www.youtube.com/watch?v=nxTaG-oVgEg)

- 컴포넌트로 생성한 태그에 추가적으로 클래스를 입력하면 기존에 사용하던 방식 그대로 추가 css 속성을 적용할 수 있음
- 개발자 도구로 확인해보면 추가 입력한 클래스가 기존의 클래스와 함께 자연스럽게 입력되어있는 것을 확인할 수 있음
- props : 생성자 매서드
- props에 태그로 사용할 변수를 스트링으로 설정하면 template에서 태그로 활용할 수 있음

```
  <square-box-1 class="bg-red" text-bg-class="bg-gold">내용4</square-box-1>
```

```
const VueApp = {
  setup() {
  }
};

const vueApp1 = Vue.createApp(VueApp)

vueApp1.component('square-box-1', {
  props: {
    'textBgClass': {
      type:String
    }
  },
  template: `
    <div class="square-box-1">
      <span :class="textBgClass"><slot /></span>
    </div>
  `
});

vueApp1.mount('#vue-app');
```


- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/ZELLmeW)


---
### 14. [컴포넌트, template 태그를 활용한 외부 템플릿](https://www.youtube.com/watch?v=uNmgPugp6Yo)

- Vue 템플릿 안에 코드를 작성하는 것이 번거로운 경우 html에서 작성이 가능하게 할 수 있음
- template에 아이디를 정의하여 참조하는 방법
- html에는 아래와 같이 태그명을 template로 하여 작성

  - 코드 예시

```
<template id="vue-component__square-box-1">
  <div class="square-box-1">
    <span :class="textBgClass"><slot /></span>
  </div>
</template>
```

- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/OJWWaEe)


---
### 15. [컴포넌트, 로직 넣기](https://www.youtube.com/watch?v=MUDJr2Ef3Nw)

- Vue로 마운트가 된 이후에 태그가 활성화가 되어 적용이 됨
- 프로그램은 항상 위에서 아래로 실행함을 고려
- js 일반 function과 arrow function에서 this가 가리키는 대상이 다름(차이점이 존재)
- js가 함께 html, css 묶여서 모듈화가 가능함

- Vue 구조 : setup, props, template

```
<template id="vue-component__square-box-1">
  <div @click="toggleBoxShadow" class="square-box-1 vue-component" :style="divStyle">
    <span :class="textBgClass"><slot /></span>
  </div>
</template>
```

```
const VueApp = {
  setup() {
    const maxCount = Vue.ref(10);

    return {
      maxCount
    }
  },
  mounted() {
    $('.square-box-1:not(.vue-component)').click(function() {
      $(this).css('box-shadow', '10px 10px 10px red');
    });
  }
};

const vueAppBuilder = Vue.createApp(VueApp)

vueAppBuilder.component('square-box-1', {
  setup() {
    const boxShadowStatus = Vue.ref(false);

    const toggleBoxShadow = () => {
      boxShadowStatus.value = !boxShadowStatus.value;
    };

    const divStyle = Vue.computed(() => {
      return {
        boxShadow:boxShadowStatus.value ? '10px 10px 10px red' : ''
      };
    });

    return {
      divStyle,
      toggleBoxShadow
    }
  },
  props: {
    'textBgClass': {
      type:String
    }
  },
  template: '#vue-component__square-box-1'
});

const vueApp1 = vueAppBuilder.mount('#vue-app');
```


- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/poRRQGE)


---
### 16. [할일리스트, 추가](https://www.youtube.com/watch?v=dYL64vCFoT8)

- setup() 
  - 변수 선언 : let, const
  - return : 변수를 사용하려면 반드시 해야함

- 기능 구현시 간단한 기본 기능부터 차례대로 구현하면서 점검 및 수정 / 보완을 함

- 바닐라 자바스크립트 프로그래밍 능력도 겸비하면 프론트 단의 작업에 있어 효율성을 얻을 수 있음

- Vue 2.0과 문법적으로 차이는 있지만 학습하면 도움이 될 것으로 예상

- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/wvggZLe)



---
### 17. [할일리스트, 삭제](https://www.youtube.com/watch?v=lVJc9U7iTIE)

- v-for 를 사용할 때는 항상 key를 사용하는 것이 좋음
- key가 검색이나 렌더링에 있어 Vue가 참조하여 처리할 수 있게 해줌
- 필요한 기능 검색 후 적용해보는 습관이 중요!!!


- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/PoWWvQE)


---
### 18. [할일리스트, 삭제](https://www.youtube.com/watch?v=h5bGH9n6TcY)

- v-for 를 사용할 때는 항상 key를 사용하는 것이 좋음
- key가 검색이나 렌더링에 있어 Vue가 참조하여 처리할 수 있게 해줌
- 필요한 기능 검색 후 적용해보는 습관이 중요!!!
- CRUD 기능 구현이 항상 모든 서비스의 기본으로 구현 과정을 이해하고 숙지해야함
- java 뿐만 아니라 다른 언어로 프로그래밍을 할 때도 기본적인 CRUD 구현 알고리즘은 숙지, 숙련해야함

- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/Bappezw)



---
### 19. [할일리스트, 삭제](https://www.youtube.com/watch?v=icRLU8QTpq0)

- v-for 를 사용할 때는 항상 key를 사용하는 것이 좋음
- key가 검색이나 렌더링에 있어 Vue가 참조하여 처리할 수 있게 해줌
- 필요한 기능 검색 후 적용해보는 습관이 중요!!!
- CRUD 기능 구현이 항상 모든 서비스의 기본으로 구현 과정을 이해하고 숙지해야함
- java 뿐만 아니라 다른 언어로 프로그래밍을 할 때도 기본적인 CRUD 구현 알고리즘은 숙지, 숙련해야함

- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/eYggwgZ?editors=0010)


---
### 20. [할일 리스트, 리스트 부분을 todo-list 컴포넌트로 분리](https://www.youtube.com/watch?v=CmVI4gDDnx0&feature=youtu.be)

- 복잡한 html 코드 부분을 컴포넌트로 분리하여 작성하여 재사용에 있어 유리함
- props 설정값 입력 필수

- Vue에는 self-closing 이 지원되지 않음

- 최근 대부분의 프레임워크에서 컴포넌트 단위로 작업하는 이유를 확인 가능
- 컴포넌트로 구성한 부분은 바로 재사용이 가능하고 필요한 부분만 수정해서 프로젝트별로 커스터마이징이 가능


- [활용된 사례 코드 링크](https://codepen.io/NTL-design/pen/KKaWovP)


---
## Vue.js 3.0
- 뷰 강의 독학(Vu3.js 입문, 이지스퍼블리싱)
  - 강의 자료 [참고](https://codepen.io/jangka44/live/NWdqRER)
  - 뷰 활용 프로젝트 강의 수강 후 연습
  - 상장례 어플 유지, 보수 및 이후 프로젝트 진행에 활용
  
- Vue3.0
  - 컴포넌트 별로 스크립트 및 css 속성을 줄 수 있으며, 독립적으로 적용
  - 재활용성이 우수함
  
  
### 3. 화면을 개발하기 위한 필수 단위 - 인스턴스 & 컴포넌트
- 뷰 인스턴스 생성
  - new Vue()와 같이 생성
  - 인스턴스 안에 el, data, template, methods, created와 같은 속성 활용
  - Vue 생성자 : 개발에 필요한 기능들을 생성자이 미리 정의해 사용자가 그 기능르 재정의하여 편리하게 사용하로독 하기 위함
    - el : 뷰 인스턴스가 그려질 시작점
    - data : 화면의 변수에 데이터 연동
    - template : 화면에 표시할 HTML, CSS 등의 마크업 요소를 정의하는 속성, 뷰의 데이터 및 기타 속성들도 함께 화면에 그릴 수 있음
    - methods : 화면 로직 제어와 관계된 메서드를 정의하는 속성, 마우스 클릭 이벤트 처리와 같이 화면의 전반적인 이벤트와 화면 동작과 관련된 로직을 추가
    - created : 뷰 인스턴스가 생성되자마자 실행할 로직을 정의할 수 있는 속성
  
- 컴포넌트
  - 전역 컴포넌트
    ```vue.js
    Vue.component('컴포넌트 이름', {
      // 컴포넌틑 내용
    });
    ```
    
  - 지역 컴포넌트
  ```vue.js
  new Vue({
    components: {
      '컴포넌트 이름' : 컴포넌트 내용
    }
  })
  ```
  
  - 컴포넌트 단위로 유효범위를 갖기 때문에 다른 컴포넌트의 값을 직접적으로 참조할 수 없음
  - 상위 컴포넌트에서 하위 컴포넌트로 props 전달
  - 하위 컴포넌트에서 상위 컴포넌트로는 기본적으로 이벤트만 전달 가능
  - props : 상위에서 하위 컴포넌트로 데이터를 전달할 때 사용하는 속성
  - 뷰 인스턴스에 컴포넌트를 등록하면 자동적으로 부모 자식관계 생성
  - 부모는 뷰 인스턴스, 자식은 컴포넌트
  - 같은 레벨의 컴포넌트 간 통신
    - 이벤트 버스 활용
    

- 이벤트 발생
  - $emit()과 v-on: 속성을 사용하여 구현
  
