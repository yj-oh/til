# Lifecycle

![](.%5B20200823%5D_lifecycle_images/b8463395.png)
* *Reference : https://kr.vuejs.org/v2/guide/instance.html*

## beforeCreate
- **Init Events & LifeCycle 직후** 가장 처음으로 실행되는 단계.
- 인스턴스는 생성되었으나 아직 속성이 정의되지 않았다.
- 돔에 접근할 수 없다.

## created
- **data 속성값과 methods 속성값에 접근 가능**한 가장 첫번째 단계.
- 인스턴스가 돔에 부착되기 전.
- template 속성에 접근할 수 없음.

## beforeMount
- **template 속성의 마크업 속성을 render function으로 변환.**
- 인스턴스가 돔에 부착되기 전.

## mounted
- el 속성에 지정한 **돔에 인스턴스를 부착하자마자** 호출되는 단계.
- 돔을 제어할 수 있으나 부착하자마자 호출되므로 하위 컴포넌트나 외부 라이브러리에 의해 추가된 화면요소가 최종 HTML 코드로 변환되는 시점과 다를 수 있음.

## beforeUpdate
- 인스턴스의 속성들이 화면에 치환되고나면 '데이터 관찰'을 통해 데이터가 변경되는지를 감시하는데,
- **데이터가 변경되고 화면을 다시 그리기 직전**에 호출되는 단계.
- 변경 예정인 새 데이터에 접근할 수 있으므로 데이터 값을 갱신하기 위해서는 이 단계에 로직을 추가한다.

## updated
- 가상 돔으로 **다시 화면 그리고나서** 실행되는 단계.
- 데이터 변경 후의 돔과 관련된 로직을 추가할 수 있다.
- 이 단계에서 값을 갱신하면 무한루프에 빠질 수 있음.

## beforeDestroy
- **인스턴스 파괴 직전**에 호출되는 단계.
- 아직 인스턴스에 접근할 수 있음.

## destroyed
- **인스턴스 파괴 후** 호출되는 단계.
- 인스턴스의 모든 속성, 하위에 선언한 인스턴스들까지 모두 파괴됨.

## 👉 코드로 확인
```html
<!DOCTYPE html>
<html lang="kr">
<head>
    <meta charset="UTF-8">
    <title>Vue 공부 중</title>
</head>
<body>
    <div id="app">
        {{ message }}
    </div>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.6.10/vue.min.js" type="text/javascript"></script>
    <script>
        let vue = new Vue({
            el: '#app',
            data: {
                message: 'Hello, World!',
            },
            beforeCreate: function() {
            	console.log("beforeCreate");
            },
            created: function() {
            	console.log("created");
            },
            beforeMount: function() {
            	console.log("beforeMount");
            },
            mounted: function() {
            	console.log("mounted");
            	//this.message = "재밌네";
            	//console.log("값 변경");
            },
            beforeUpdate: function() {
            	console.log("beforeUpdate");
            },
            updated: function() {
            	console.log("update");
            },
            beforeDestroy: function() {
            	console.log("beforeDestroy");
            },
            destroyed: function() {
            	console.log("destroyed");
            }
        });

        let sec = 0;
        let delay = setInterval(function(){
            console.log(++sec);
            if(sec === 2) {
                vue.$destroy();
                clearInterval(delay);
            }
        }, 1000);
    </script>
</body>
</html>
```
- 라이프 사이클 단계마다 console.log() 찍었고, 2초 뒤에 뷰 인스턴스 소멸시키려고
```javascript
let sec = 0;
let delay = setInterval(function(){
  console.log(++sec);
  if(sec === 2) {
    vue.$destroy();
    clearInterval(delay);
  }
}, 1000);
```
- 위의 코드를 넣었다.
- 타이머처럼 초 단위로 console.log() 찍으려고 setTimeout() 말고 setInterval() 이용했다. 
- 그냥 깔끔하게 아래와 같이 넣어도 된다.
```javascript
setTimeout(function () { vue.$destroy(); }, 2000);
```

#### 브라우저 켜보면 결과는?
![](.%5B20200823%5D_lifecycle_images/51acb3c7.png)

- 각 사이클 순서대로 거치고 소멸됨.
- 빠진 단계가 있다.
   - **beforeUpdate랑 updated**
   - 왜냐?
   - 둘은 $watch 속성이 데이터 관찰 하다가 데이터가 변경되면 호출되는 단계들이라서.
   - 위 코드에서는 데이터가 변경되지 않기 때문에 호출되지 않는다.
- 두 단계를 호출하기 위해 데이터를 변경시키자.
- mounted 단계
- 아래 코드의 주석을 해제하고 다시 돌려보자.
```javascript
this.message = "재밌네";
console.log("값 변경");
```
![](.%5B20200823%5D_lifecycle_images/c6387d26.png)
- 값이 변경되고 beforeUpdate랑 updated 단계가 호출됨.
