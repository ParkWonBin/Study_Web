## JS 특이한 문법
#### [slice(start[, end])](https://im-developer.tistory.com/103)
```JS
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var arr1 = arr.slice(3, 5); // [4, 5]
var arr2 = arr.slice(undefined, 5); // [1, 2, 3, 4, 5]
var arr3 = arr.slice(-3); // [8, 9, 10]
var arr4 = arr.slice(-3, 9); // [8, 9]
```

#### [splice(start[, deleteCount[, item1[, item2[, ...]]]])](https://im-developer.tistory.com/103)
```JS
// 
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12];
var arr1 = arr.splice(10, 2, 'a', 'b', 'c');
console.log(arr); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, "a", "b", "c"]
console.log(arr1); // [11, 12]
```

## JS 문법 정리
```JS
// VB.NET
"Hellow World".contains("Hellow")
"1,2,3".split(","c).contains("1")
Arr = "1,2,3".split(","c)
join(Arr,",")
Arr.Count

// JS
"Hellow World".includes("Hellow")
"1,2,3".split(",").includes("1")
Arr = "1,2,3".split(",")
Arr.join(",")
Arr.length
```


## [Mac 에서 VScode로 Web_Dev 세팅](https://www.youtube.com/watch?v=J8JPPcxr8Q8)

## 반응형 웹에 따른 서식 변경 예시
```html
<html>
    <header>
    
        <!-- CSS 파일분리 문법 -->
        <!-- <link rel="stylesheet" href="css/main.css" /> -->
        
        <style>
            @charset "utf-8";

            /* Default */
            h1{background-color: yellow; color: black}

            /* small desktop */
            @media screen and (max-width: 1200px){
                h1{background-color: greenyellow; color: gray}
            }

            /* tablet */
            @media screen and (max-width: 1024px){
                h1{background-color: blue; color: yellow;}
            }

            /* mobile phone */
            @media screen and (max-width: 940px){
                h1{background-color: red; color: white}
            }
        </style>
    </header>

    <h1>
        반응형 서식 예시 - 박원빈
    </h1>

</html>
```
