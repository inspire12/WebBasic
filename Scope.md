# 스코프(Scope)
스코프는 현재 접근할 수 있는 변수들의 범위를 말한다. 유효범위라고도 하며 변수와 매개변수의 접근성과 생존기간을 뜻한다.<br>
따라서 스코프의 개념을 잘 알고 있어야 변수와 매개변수의 접근성과 생존기간을 제어할 수 있다. <br>
스코프의 종류는 크게 두 가지가 있다.

- Global Sope : 스크립트 전체에서 참조되는 것
- Local Scope : 정의된 함수 안에서만 참조되는 것

## 스코프의 생성
자바스크립트는 일반적인 블록 스코프를 따르지 않는다. 자바스크립트에서 스코프를 생성하는 구문은 다음과 같다.
- `function`
- `catch`
- `with`
> 자바스크립트에 있지만 없는 듯이 살아야 하는 두 가지 구문이 있다. 바로 with 와 eval 

이런 구문들이 사용될 때만 스코프가 생성되고, 다른 프로그래밍 언어처럼 `{ }` 를 이용해 블록을 생성한다고 해서 스코프가 생성되는 것이 아니다. 
> 자바스크립트는 전통적으로 함수 레벨 스코프를 지원해왔지만, ES6 부터 블록레벨 스코프를 지원하기 시작했다 !

### function 구문의 스코프 생성
````javascript
function foo() {
   if (true) {
      var color = "red";
   }
   console.log(color); // red
}
foo();
````
위 코드는 아무 문제 없이 red 를 출력한다.

### ES6 의 블록 레벨 스코프
ES6 의 `let`, `const` 키워드는 블록 레벨 스코프 변수를 생성한다.
````javascript
function foo() {
   if (true) {
      let color = "yellow";
      console.log(color); // yellow
   }
   console.log(color); // ReferenceError: color is not defined
}
foo();
````
`let color` 를 `if` 블록 내에 선언하였기 때문에 `if` 블록 내부에서만 참조할 수 있으며 그 밖의 영역에서는 참조할 수 없다.


## 스코프의 지속성
지금 함수가 선언된 곳이 아닌 전혀 다른 곳에서 함수가 호출될 수 있어서 해당 함수가 현재 참조하는 스코프를 
지속할 필요가 있다. 이는 자바스크립트의 큰 특징 중 하나이다. 


## 렉시컬 스코프
렉시컬 스코프는 보통 동적 스코프와 많이 비교된다.
<br> 
동적 스코프는 프로그램의 런타임 도중의 실행 컨택스트나 호출 컨택스트에 의해 결정되고, 렉시컬 스코프에서는 소스코드가 작성된 그 문맥에서 
결정된다. 대부분의 언어들은 렉시컬 스코프 규칙을 따르고 있다. 

#### var 키워드 없이 변수를 선언할 경우
`var` 키워드를 쓰지 않으면 '현재보다 상위의 스코프를 탐색하면서 변수가 있는지 검사' 하는 단계를 반복해서 거치게 된다. 이러한 
검사가 글로벌 영역까지 다다라서 그 곳에도 변수가 정의되어 있지 않다면, 그때야 비로소 글로벌 영역에 변수를 정의한다. <br>
따라서 var 키워드 없이 변수를 사용하면 글로벌 변수 라는 말은 정확하게 말하자면 틀린 말이다. 
