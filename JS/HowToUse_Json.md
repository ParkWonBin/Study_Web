##### JSON Array 초기화
```JS
Arr1 = new Array(3).fill({"totoal":0, "stay":0} }) // 각 위치에 같은 reference 들어감
Arr2 = new Array(3).fill(null).map(x=>{return{"totoal":0, "stay":0} }) // 각 위치에 각각의 value 초기화됨

Arr1[0].total++ // Arr1은 0,1,2 위치에서 모두 같은 ref를 사용하기 때문에, 모든 원소의 total이 증가함
Arr2[0].total++ // Arr2는 0,1,2 위치에서 각각 다른 ref를 사용(다른 값으로 입력)되었기 때문에 해당 위치의 total만 증가함
```

##### JSON 사용하여 문제 해결
[관련문제](https://programmers.co.kr/learn/courses/30/lessons/42889)
```JS
function solution(N, stages) {
    var Arr = new Array(N+2).fill(null).map((x,i)=>{ return{"stage":i,"clear":0, "stay":0, "fail":0} })
    
    // 해당 스테이지에 막혀있는 인원
    for(var i=0; i<stages.length; i++){ Arr[stages[i]]["stay"]++ }
    
    // 해당 스테이지 누적 clear 횟수
    for(var i=N; i>0; i--){ Arr[i].clear = Arr[i+1].clear + Arr[i+1].stay }
    
    // 실패율 누적
    for(var i=0; i<N+1; i++){ Arr[i].fail = Arr[i].stay /  (Arr[i].stay + Arr[i].clear)}
    
    // 불필요한 데이터 제거
    Arr.shift(); Arr.pop()
    
    // 정렬
    Arr.sort((a,b)=>b["fail"]-a["fail"])
    
    // console.table(Arr)
    return Arr.map(x=> x['stage']) ;
}

// Json 없이 풀기
function solution(N, stages) {
    let result = [];
    for(let i=1; i<=N; i++){
        let reach = stages.filter((x) => x >= i).length;
        let curr = stages.filter((x) => x === i).length;
        result.push([i, curr/reach]);
    }
    result.sort((a,b) => b[1] - a[1]);
    return result.map((x) => x[0]);
}
```

### JSON for문 사용 
[문자열 대체](https://programmers.co.kr/learn/courses/30/lessons/81301)
```js
function solution(s) {
    let charSet = {
        "zero" : 0,
        "one" : 1,
        "two" : 2,
        "three" : 3,
        "four" : 4,
        "five" : 5,
        "six" : 6,
        "seven" : 7,
        "eight" : 8,
        "nine" : 9,
    }

    for(let [key, value] of Object.entries(charSet)) {
        let re = new RegExp(`${key}`,"g");
        s = s.replace(re, value);
    }
    return parseInt(s);
}
```
