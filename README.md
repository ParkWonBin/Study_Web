## JS 문법 정리
```JS
// VB.NET
"Hellow World".contains("Hellow")
"1,2,3".split(","c).contains("1")
Arr = "1,2,3".split(","c)
join(Arr,",")

// JS
"Hellow World".includes("Hellow")
"1,2,3".split(",").includes("1")
Arr = "1,2,3".split(",")
Arr.join(",")

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
