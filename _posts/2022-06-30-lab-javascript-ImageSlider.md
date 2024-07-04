---
title: "[JS/자바스크립트] 이미지 슬라이더 예제 (ImageSlider)"
date: 2022-06-09 17:14:34 +0900
categories: [Lab, JavaScript]
tags: [javascript]
---

> 3초마다 자동으로 넘어가는 이미지 슬라이더 웹 페이지에서 구현하기

<br>

### **구현**

우선 웹 페이지를 구성하였다.

```html
<!DOCTYPE html>
<html>
    <head>
        <title>이미지 슬라이더</title>
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
        <script src="ImageSlider.js"></script> // 플러그인의 JS 파일을 추가함
        <script>
            // 문서 객체 조작 이전에 화면 구성 필요
            // jQuery에서는 document 객체의 ready 이벤트를 활용함
            $(document).ready(function () {
                $('.slider').imageSlider({
                    width: 460,
                    height: 300
                });
            });
        </script>
    </head>
    <body>
        <div class="slider">
            <div class="images">
                <img class="image" src="img.png" />
                <img class="image" src="img2.png" />
                <img class="image" src="img.png" />
                <img class="image" src="img2.png" />
                <div class="image">
                    <h1>이미지가 아닌 것</h1>
                    <p>Lorem ipsum dolor sit amet.</p>
                </div>
            </div>
        </div>
    </body>
</html>
```

jQuery로 만든 코드는 *플러그인*으로 만들면 재사용이 용이하다. 플러그인이란 추가적인 기능이나 특징을 제공하는 것이라고 할 수 있는데, jQuery 플러그인은 기존의 jQuery 라이브러리에 없는 기능을 추가하거나 사용성을 개선하는 역할을 한다. 플러그인은 일반적으로 외부에서 작성된 자바스크립트 코드로 구현되며, jQuery의 기능과 메서드를 사용하여 작동한다.

플러그인을 사용하기 위해서는 해당 플러그인의 JavaScript 파일을 웹 페이지에 추가해야 한다. 이후 jQuery를 사용하여 원하는 요소를 선택하고, 플러그인의 메서드를 호출하여 플러그인을 적용합니다.

이미지 슬라이더를 조작하는 부분을 플러그인 형태로 구성하고자 \$.fn 속성에 메소드를 만들어 분리하였다.

\$.fn 속성에 메소드를 설정하면 () 함수로 생성되는 jQuery 객체에 메소드를 사용할 수 있게 하였다.

```js
// $.fn 속성의 메소드 imageSlider 설정
// 변수 imageSlider에 익명 함수를 생성 및 할
// $는 jQuery 객체
$.fn.imageSlider = function (object) {
    // 변수를 선언함
    // '||' 연산자는 변수의 디폴트 값을 정해주는 데 사용됨
    // 할당한 값이 undefined일 때 '||' 연산자 이후의 값으로 초기화 (짧은 초기화 조건문)
    const width = object.width || 460;
    const height = object.height || 300;
    // 변수 선언은 .html에서는 var, .js에서는 let을 사용함
    let current = 0;
    // 함수를 선언함
    const moveTo = function () {
        console.log("moveTo 함수를 실행합니다.");
        // console.log(this); 
        // $(this).find('.images').animate({    
        // animate 메서드 실행 안됨. 해결 요망-
        /* 'function () {}' 형태의 익명 함수 내부에서 this는 자바스크립트 최상위 객체 또는 외부에서 강제로 연결한 객체를 나타냄.
        위 코드를 사용하려면 메소드 내부의 this는 외부에서 강제로 연결된 객체, 즉 width: 460, height: 300의 div 태그를 나타내야 함.
        'console.log(this);' 코드를 위에 삽입하여 콘솔 창을 확인한 결과 Window { ... }가 뜨는 것을 확인함.
        즉, 여기서 this는 자바스크립트 최상위 객체인 window 객체를 나타냄. */
        $('.images').animate({
            left: -current * width
        }, 1000, function () {
            console.log("이미지를 이동시켰습니다.");
            // alert("animate() 메서드가 실행되면 이 메시지를 콘솔 로그에 출력합니다.");
        });
        console.log("moveTo 함수를 종료합니다.");
    };
    // 슬라이더 내부의 이미지 개수를 확인함
    // 이때 this는 외부에서 강제로 연결된 객체, 즉 width: 460, height: 300의 div 태그를 나타냄
    const imageLength = $(this).find('.image').length;
    // 슬라이더 버튼을 추가함
    for (let i = 0; i < imageLength; i++) {
        $('<button></button>')
            .attr('data-position', i)
            .text(i)
            .click(function () {
                current = $(this).attr('data-position');
                console.log("버튼을 눌렀습니다.");
                moveTo();
            })
            .insertBefore(this); // 다른 노드 앞에 새로운 노드를 삽입
    }
    // 슬라이더 스타일을 설정함
    $(this).css({
        position: 'relative',
        width: width,
        height: height,
        overflow: 'hidden'
    });
    $(this).find('.images').css({
        position: 'relative',
        width: width * imageLength
    });
    $(this).find('.image').css({
        margin: 0,
        padding: 0,
        width: width,
        height: height,
        display: 'block',
        float: 'left'
    });
    // 3초마다 슬라이더를 이동시킴
    setInterval(function () {
        current = current + 1;
        current = current % imageLength;
        console.log("3초가 지났습니다.");
        moveTo();
    }, 3000);
};
```

<br>

### **오류**

..

콘솔 로그를 찍어본 결과, `$(this).find('.images').animate({ ... });` 부분이 실행되지 않는 것을 확인하였다.

`function () {}` 형태의 익명 함수 내부에서 this는 자바스크립트 최상위 객체 또는 외부에서 강제로 연결한 객체를 나타낸다. 위 코드를 사용하려면 메소드 내부의 this는 외부에서 강제로 연결된 객체, 즉 width: 460, height: 300의 div 태그를 나타내야 한다.
 `console.log(this);` 코드를 상위에 삽입하여 콘솔 창을 확인한 결과 Window { ... }가 뜨는 것을 확인하였다.
 즉, 여기서 this는 자바스크립트 최상위 객체인 window 객체를 나타내고 있는 것이다.

<br>
