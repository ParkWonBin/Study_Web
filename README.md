##### JS 요일 구하기
```JS
function GetWeekDaty(Year,Month, Day) {
return "SUN,MON,TUE,WED,THU,FRI,SAT".split(",")[new Date( [Year,Month,Day].join("-") ).getDay()]
}
```
##### JS Distinct 중복제거
```JS
Arr = Arr.filter((v,i)=> Arr.indexOf(v)==i) // 중복값 제거
Arr = [...new Set(Arr)] // 중복값 제거
```
##### JS 이진수 변환
```JS
3 | 15 // 15 두 수를 이진수로 변환한 후 OR 연산, 결과를 다시 숫자로 변환
3 & 15 // 3 두 수를 이진수로 변환한 후 AND연산, 결과를 다시 숫자로 변환
(15).toSting(2) // 1111 해당 숫자를 이진수로 변환 후 문자열로 표시

// & : 비트연산자 AND
// | : 비트연산자 OR
// && : 조건문 AND
// || : 조건문 OR
```

#### 누적계산
##### [JS - Reduce](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)  
```JS
Arr.Reduce((acc, cur, idx, src)=> somthing , seed)
Arr.Reduce(function(acc, cur, idx, src){return something } , seed)
// 누산기 (acc), 현재 값 (cur), 현재 인덱스 (idx), 원본 배열 (src)
"123456789".split("").reduce((acc,crt)=>{return Number(acc)+Number(crt)})
"123456789".split("").reduce((acc,crt)=>{return acc+Number(crt)},0) // 초기값 seed 명시

Math.max.apply(null,[1,2,3,2,1])
Math.max(...[1,2,3,2,1])
Math.max(1,2,3,2,1)
```
##### [Linq - Aggrigete](https://linqsamples.com/linq-to-objects/aggregation/Aggregate-seed-lambda-vb)
```VB
"123456789".split(""c).Aggregate(Function(acc, crt) acc + crt)
"123456789".split(""c).Aggregate(0, Function(acc, crt) acc + crt) '초기값 seed 명시
```

## JS 특이한 문법
#### [정렬 관련](https://hianna.tistory.com/409)
```JS
arr = "1,2,10,4".split(",")
arr.sort() // [1,10,2,4]
arr.sort((a,b)=> a-b ) // [1,2,4,10]
arr.sort((a,b)=> b-a ) // [10,4,2,1]
```

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
//Linq
ArrArr = "1,2,3|4,5,6|7,8,9".split("|"c).select(function(x) x.split(",")).ToArray
join(ArrArr.select(function(x) x.join(",")).ToArray , "|")

// JS
"Hellow World".includes("Hellow")
"1,2,3".split(",").includes("1")
Arr = "1,2,3".split(",")
Arr.join(",")
Arr.length
// Array Method
ArrArr = "1,2,3|4,5,6|7,8,9".split("|").map(function(x){ return x.split(",")})
ArrArr = "1,2,3|4,5,6|7,8,9".split("|").map((x)=> x.split(",") )
ArrArr.map(function(x){return x.join(",")}).join("|")
ArrArr.map((x)=> x.join(",") ).join("|")
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
