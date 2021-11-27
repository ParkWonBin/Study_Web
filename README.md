# Web-Study

# Web-Study



### 반응혀 웹에 따른 서식 변경 예시
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
