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