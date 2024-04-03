---
title:  "올바른 괄호"
categories: "coding_test"
tag: [coding_test]
toc: true
---

https://school.programmers.co.kr/learn/courses/30/lessons/12909

## 올바른 괄호

문제 설명
괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어

"()()" 또는 "(())()" 는 올바른 괄호입니다.
")()(" 또는 "(()(" 는 올바르지 않은 괄호입니다.
'(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면 false를 return 하는 solution 함수를 완성해 주세요.

제한사항
문자열 s의 길이 : 100,000 이하의 자연수
문자열 s는 '(' 또는 ')' 로만 이루어져 있습니다.
입출력 예
s	answer
"()()"	true
"(())()"	true
")()("	false
"(()("	false
입출력 예 설명
입출력 예 #1,2,3,4
문제의 예시와 같습니다.

## 문제 풀이
```java
import java.util.*;

class Solution {
    // 주어진 문자열이 올바른 괄호 짝을 가지고 있는지 확인하는 메소드
    boolean solution(String s) {
        // 괄호를 저장할 스택 생성
        Stack<Character> testStack = new Stack<>();
        // 결과를 저장할 변수 초기화
        boolean answer = true;
        
        // 문자열을 순회하며 괄호 짝을 확인
        for(int i=0; i < s.length(); i++){
            char currentChar = s.charAt(i); // 현재 문자
            if(currentChar == '('){ // (를 만나면 
                testStack.push(currentChar); // (값을 스택에 넣음
            }
            else if(currentChar == ')'){ // )를 만나면
                if(testStack.isEmpty()) { // 스택이 비어 있다면
                    answer = false; // 잘못된 문장
                    break; // 종료
                } 
                else { // 스택이 안비었으면 = 스택에 (값이 있으면
                    testStack.pop(); // 꺼내고 계속 진행
                }
            }
        }
        
        // 문자열을 모두 순회한 후에도 스택에 괄호가 남아 있다면 올바르지 않은 괄호
        if(!testStack.isEmpty()){ 
            answer = false; // 잘못된 문장
        }
        
        return answer; // 결과 반환
    }
}

```