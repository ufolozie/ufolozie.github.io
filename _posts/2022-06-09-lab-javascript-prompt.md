---
title: "[JS/자바스크립트] prompt() 함수 활용 예제"
date: 2022-06-09 17:40:05 +0900
categories: [Lab, JavaScript]
tags: [javascript]
---

> 사용자가 태어난 연도를 입력 받아 띠를 출력하는 프로그램  
> (예: '1991'을 입력하면 '양띠'를 출력)

<br>

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Prompt Example</title>
        <script>
            const input = prompt('출생년도를 입력하세요.', '(예: 2001)');
            const ddi = input % 12;
            let output = '';

            switch (ddi) {
                case 0:
                    output = '원숭이';
                    break;
                case 1:
                    output = '닭';
                    break;
                case 2:
                    output = '개';
                    break;
                case 3:
                    output = '돼지';
                    break;
                case 4:
                    output = '쥐';
                    break;
                case 5:
                    output = '소';
                    break;
                case 6:
                    output = '호랑이';
                    break;
                case 7:
                    output = '토끼';
                    break;
                case 8:
                    output = '용';
                    break;
                case 9:
                    output = '뱀';
                    break;
                case 10:
                    output = '말';
                    break;
                case 11:
                    output = '양';
                    break;
            }

            alert(output + '띠');
        </script>
    </head>
    <body>

    </body>
</html>
```

<br>

<br>

<br>

> 사용자에게서 숫자를 2개 입력 받아 두 숫자 사이의 범위 값을 모두 더하는 프로그램  
> (예: '1, 3'을 입력하면 1 + 2 + 3을 해서 6을 출력. 단, '3, 1'을 입력해도 6을 출력할 수 있게 함.)

<br>

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Prompt Example</title>
        <script>
            // 사용자의 입력을 받음
            const input = prompt('서로 다른 숫자를 두 개 입력하세요.', '(예: 1, 3)');

            // 입력을 파싱하여 배열에 넣음
            const array = input.split(',');
            // 숫자로 변환할 수 없는 문자열은 버림
            let num1 = parseInt(array[0]);
            let num2 = parseInt(array[1]);
            let output;

            // num1가 num2보다 항상 작은 수가 되도록 정렬
            if (num1 > num2) {
                let temp;
                temp = num1;
                num1 = num2;
                num2 = temp;
            }
            // 두 수의 합 계산
            for (output = 0; num1 <= num2; num1++) {
                output += num1;
            }

            // 결과 출력
            alert('두 숫자의 합은 ' + output + '입니다.');
        </script>
    </head>
    <body>

    </body>
</html>
```

<br>
