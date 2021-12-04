### 정규식과 반복문
[관련 문제](https://programmers.co.kr/learn/courses/30/lessons/81301)
```JS
function solution(s) {
    const List = "zero,one,two,three,four,five,six,seven,eight,nine".split(",")
    for (var i in List){ s = s.replace(new RegExp(List[i],"gi"),i) }
    return Number(s);
}
```
```JS
const digit2word = ['zero','one','two','three','four','five','six','seven', 'eight','nine']
function solution(s) {
    return Number(digit2word.reduce((ans, word, digit) => ans.replace(new RegExp(word, 'g'), digit), s));
}
```
### 정규식 관련 문제
[관련 문제](https://programmers.co.kr/learn/courses/30/lessons/72410)
```JS
const solution = new_id =>
    new_id.toLowerCase()
          .replace(/[^\w-_.]/g, "")
          .replace(/\.+/g, ".")
          .replace(/^\.|\.$/g, "")
          .replace(/^$/, "a")
          .match(/^.{0,14}[^.]/)[0]
          .replace(/^(.)$/, "$1$1$1")
          .replace(/^(.)(.)$/, "$1$2$2");
```

```JS
function solution(new_id) {
    const answer = new_id
        .toLowerCase() // 1
        .replace(/[^\w-_.]/g, '') // 2
        .replace(/\.+/g, '.') // 3
        .replace(/^\.|\.$/g, '') // 4
        .replace(/^$/, 'a') // 5
        .slice(0, 15).replace(/\.$/, ''); // 6
    const len = answer.length;
    return len > 2 ? answer : answer + answer.charAt(len - 1).repeat(3 - len);
}
```
