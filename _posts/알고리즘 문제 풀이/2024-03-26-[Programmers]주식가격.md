---
title:  "주식가격"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

https://school.programmers.co.kr/learn/courses/30/lessons/42584

## 주식가격

문제 설명
초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.

제한사항
prices의 각 가격은 1 이상 10,000 이하인 자연수입니다.
prices의 길이는 2 이상 100,000 이하입니다.
입출력 예
prices	return
[1, 2, 3, 2, 3]	[4, 3, 1, 1, 0]
입출력 예 설명
1초 시점의 ₩1은 끝까지 가격이 떨어지지 않았습니다.
2초 시점의 ₩2은 끝까지 가격이 떨어지지 않았습니다.
3초 시점의 ₩3은 1초뒤에 가격이 떨어집니다. 따라서 1초간 가격이 떨어지지 않은 것으로 봅니다.
4초 시점의 ₩2은 1초간 가격이 떨어지지 않았습니다.
5초 시점의 ₩3은 0초간 가격이 떨어지지 않았습니다.
※ 공지 - 2019년 2월 28일 지문이 리뉴얼되었습니다.

## 문제 풀이
```java
import java.util.*;

class Solution {
    // Solution 클래스 선언

    // solution 메서드 선언
    // - int 배열 prices를 매개변수로 받음
    public int[] solution(int[] prices) {
        // int 배열 answer를 선언하여 prices 배열의 길이와 같은 크기로 초기화
        int[] answer = new int[prices.length];
        // Stack 객체 stack을 생성
        Stack<Integer> stack = new Stack<>();
        // prices 배열을 순회하는 반복문
        for (int i = 0; i < prices.length; i++) {
            // 스택이 비어있지 않고, 현재 가격이 스택의 맨 위 가격보다 작을 때까지 반복
            while (!stack.isEmpty() && prices[stack.peek()] > prices[i]) {
                // 스택에서 가장 위의 인덱스를 꺼냄
                int idx = stack.pop();
                // answer 배열에서 해당 인덱스의 값을 현재 인덱스와 차이를 계산하여 저장
                answer[idx] = i - idx;
            }
            // 현재 인덱스를 스택에 추가
            stack.push(i);
        }
        // 스택이 비어질 때까지 반복
        while (!stack.isEmpty()) {
            // 스택에서 가장 위의 인덱스를 꺼냄
            int idx = stack.pop();
            // answer 배열에서 해당 인덱스의 값을 prices 배열의 길이에서 현재 인덱스를 뺀 값으로 설정
            answer[idx] = prices.length - 1 - idx;
        }
        // 계산된 answer 배열을 반환
        return answer;
    }
}

```