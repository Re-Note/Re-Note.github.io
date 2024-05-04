---
title:  "JadenCase 문자열"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/12951

## 문제 제목 : JadenCase 문자열

문제 설명
JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)
문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

제한 조건
s는 길이 1 이상 200 이하인 문자열입니다.
s는 알파벳과 숫자, 공백문자(" ")로 이루어져 있습니다.
숫자는 단어의 첫 문자로만 나옵니다.
숫자로만 이루어진 단어는 없습니다.
공백문자가 연속해서 나올 수 있습니다.
입출력 예
s	return
"3people unFollowed me"	"3people Unfollowed Me"
"for the last week"	"For The Last Week"
※ 공지 - 2022년 1월 14일 제한 조건과 테스트 케이스가 추가되었습니다.

## 문제 풀이
```java
class Solution {
    // 주어진 문자열의 단어들의 첫 글자를 대문자로 변환하는 메소드
    public String solution(String s) {
        // 결과를 저장할 StringBuilder 선언
        StringBuilder answer = new StringBuilder();
        
        // 주어진 문자열을 모두 소문자로 변환
        String str = s.toLowerCase();
        
        // 공백을 기준으로 문자열을 나누어 배열에 저장
        String[] arr = str.split(" ");
        
        // 배열의 각 요소에 대해 처리
        for(int i = 0; i < arr.length; i++){
            // 단어의 길이가 0이면 공백 문자열이므로 공백 추가
            if(arr[i].length() == 0) {
                answer.append(" ");
            }
            else{
                // 단어의 첫 글자를 대문자로 변환하여 추가
                answer.append(arr[i].substring(0, 1).toUpperCase());
                // 나머지 부분은 그대로 추가
                answer.append(arr[i].substring(1, arr[i].length()));
                // 단어 사이에 공백 추가
                answer.append(" ");
            }
        }
        
        // 입력 받은 문자열의 맨 마지막이 공백 문자라면 변환된 문자열 반환
        if(s.substring(s.length() - 1, s.length()).equals(" ")){
            return answer.toString();
        }
        // 맨 마지막 공백 제거 후 변환된 문자열 반환
        return answer.substring(0, answer.length() - 1);
    }
}
```