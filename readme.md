# VUE3 SYNTAX

## 보간법
Vue {{}} 이중 중괄호를 통해 데이터를 바인딩 할수 있음
```html
  <span>메시지:{{msg}}</span>
```
## 원시 HTML
이중 중괄호는 데이터를 HTML이 아닌 일반 텍스트로 해석  
실제 HTML로 출력할려면 v-html 디렉티브 사용

## 속성
{{}}는 HTML 속성에 사용할 수 없음.  
v-bind를 사용하여 HTML 속성에 바인딩

## Computed
### 계산된 데이터 
데이터 옵션에 정의된 특정한 데이터를 추가적으로 연산을 통해 반환된 값을 새로운 데이터로 활용
### 캐싱
한 번 연산된 데이터가 있으면 반복적으로 사용해도 다시 연산 하지 않음
### Getter,Setter
computed로 계산된 데이터는 읽기 전용이기 때문에 연산을 통해
값을 얻어내는 용도로만 사용됨
```js
computed :{
  revesedMessage :{ //객체 데이터 형식
    get() {
      return 연산로직
    }
    set(value){
      value
    }
  }
}
```

### v-if & v-show

v-if는 조건부 렌더링  
초기 렌더링시 조건이 false면 아무 작업도 하지 않음(렌더링 안됨)  
조건부 블록은 조건이 true가 될 때가지 렌더링 되지 않음

v-show는 초기 조건과 관계없이 항상 렌더링 됨

v-if는 전환비용이 놓고 v-show는 초기 렌더링 비용이 높다
자주 변환해야 한다면 v-show 사용

### 고유한 아이디 생성 패키지

```
$ npm i -D shortid
```
```js
  newFruits(){
        return this.fruits.map(fruit => ({
          id:shortid.generate(),
          name:fruit
        }))
```

### 이벤트 수식어
```
@event.prevent.once 체이닝 가능
.stop 이벤트 전파 중단
.prevent html 기본 이벤트 중단
.capture
.self
.once
.passive 
```
- 이벤트 버블링
어떤 요소를 선택했을때 그 요소를 포함하는 부모 요소에도
이벤트가 전파 되는 것
- 이벤트 캡쳐링
부모요소에서 자식요소로 이벤트가 내려오는 것

### v-model 
양방향 데이터 바인딩
```html
<input type="text" v-model="msg" />
```
v-model은 한글 작성시 글자가 한박자 느리게 반응  
따라서 이벤트객체 타겟에 바로 할당 하게 코드 작성

```html
<input type="text" :value="msg" @input="msg = $event.target.value>
```
v-model.lazy 인풋박스에 포커스가 해제되면 반응함
v-model.number 숫자데이터를 받아야할때
v-model.trim 데이터 앞뒤쪽 공백문자 제거

### \<slot>\</slot>
속성 상속
최상위 요소가 2개일 경우 적용이 안됨  
컴포넌트 안에
```js
  export default {
    inheritAttrs:false, //상속받지 않겠다
  }
```
속성 직접적 연결
```html
  <h1 :class="$attrs.class">원하는 요소에 연결</h1> //속성 하나하나 연결
  <h1 v-bind="$attrs"></h1> // 속성 전부 연결 * :가 아닌 v-bind 사용
```
### 이름을 갖는 slot
순서를 보장해줄 수 있음
```html
상위 컴포넌트에서 v-slot:이름으로 지정
<template v-slot:icon>(B)</template> 
<template v-slot:text>Banana</template>

v-slot 약어 #
<template #icon>(B)</template> 
<template #text>Banana</template>

하위 컴포넌트에서 name="지정한 이름"으로 받음
<slot name="text"></slot>
<slot name="icon"></slot>

출력 결과 
<slot>의 순서에 의해 Banana(B)가 출력
```
### emits
컴포넌트에 이벤트 전달
최상위 요소가 2개일 경우 적용이 안됨 
컴포넌트 안에
```js
  <Mybtn @이벤트이름 ='log'></Mybtn>
  <h1 @click ="$emit('이벤트이름', $event)"></h1>

  export default {
    emits:[
      '이벤트이름'
    ]
  }
```

### Provide / Inject

App > Parent > Child 로 데이터를 넘겨주기위해  
Parent 컴포넌트에 props를 정의 해야함  
매개체 없이 App > Child로 전달하기 위해 provide / inject 사용  
반응성을 가지지 않기 때문에 반응성을 가지려면 computed를 사용해야함

```js
  App.vue에 작성
  provide (){
    return {
      msg: computed(() => {
          return this.message
        })
    }
  }

  parent에 props를 전달해줄 필요가 없음

  Child.vue에 작성
  inject :[
    'msg'
  ]
```
computed
```js
App.vue
import { computed } from 'vue'
  provide() {
    return {
      msg: computed(()=>{
        return this.message
      })
    }
  }

Child.vue 
msg에서 내보낸 데이터는 계산된 객체 데이터기때문에 value 속성으로 값을 출력
<h1>{{msg.value}}</h1>
```

### ref

```
  <h1 ref="hello> Hello World </h1>
```
```js
  export default {
    created(){ //컴포넌트가 생성된 직후기 때문에 undefined
      console.log(this.$refs.hello)
    },
    mounted(){ // 컴포넌트가 HTML에 연결된 후기 때문에 참조 가능
      console.log(this.$refs.hello)
    }
  }
```
컴포넌트를 참조할때는 $el 속성을 적어줘야함
```js
  export default {
    mounted(){ // 컴포넌트가 HTML에 연결된 후기 때문에 참조 가능
      console.log(this.$refs.hello.$el) //컴포넌트의 최상위 요소 참조
    }
    mounted(){ // 컴포넌트가 HTML에 연결된 후기 때문에 참조 가능
      console.log(this.$refs.hello.$el) //컴포넌트의 최상위 요소 참조
    }
  }   

Hello.vue
  <template>
    <div>
      <h1>Hello</h1>
      <h1 ref="good">Hello</h1>
    </div>
  </template>

  export default {
    mounted(){ // 컴포넌트가 HTML에 연결된 후기 때문에 참조 가능
      console.log(this.$refs.hello.$refs.good) //지정한 요소 참조
    }
  }
```
