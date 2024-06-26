---
title:  "N으로 표현"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42895

## 문제 제목 : N으로 표현

문제 설명
아래와 같이 5와 사칙연산만으로 12를 표현할 수 있습니다.

12 = 5 + 5 + (5 / 5) + (5 / 5)
12 = 55 / 5 + 5 / 5
12 = (55 + 5) / 5

5를 사용한 횟수는 각각 6,5,4 입니다. 그리고 이중 가장 작은 경우는 4입니다.
이처럼 숫자 N과 number가 주어질 때, N과 사칙연산만 사용해서 표현 할 수 있는 방법 중 N 사용횟수의 최솟값을 return 하도록 solution 함수를 작성하세요.

제한사항
N은 1 이상 9 이하입니다.
number는 1 이상 32,000 이하입니다.
수식에는 괄호와 사칙연산만 가능하며 나누기 연산에서 나머지는 무시합니다.
최솟값이 8보다 크면 -1을 return 합니다.
입출력 예
N	number	return
5	12	4
2	11	3
입출력 예 설명
예제 #1
문제에 나온 예와 같습니다.

예제 #2
11 = 22 / 2와 같이 2를 3번만 사용하여 표현할 수 있습니다.

※ 공지 - 2020년 9월 3일 테스트케이스가 추가되었습니다.

## 문제 풀이
```java
import java.util.*;

class Solution {
    // 주어진 N과 사칙연산을 이용하여 number를 만들기 위한 최소 횟수를 반환하는 함수
    public int solution(int N, int number) {
        int answer = -1; // 만약 number를 만들 수 없다면 -1을 반환할 변수
        ArrayList<Integer>[] setArr = new ArrayList[9]; // 사칙연산 결과를 저장할 배열
        int t = N; // N부터 시작하여 5, 55, 555, ...와 같은 숫자를 생성할 변수

        // 1부터 8까지 반복하여 setArr의 각 요소를 ArrayList로 초기화
        for(int i = 1; i < 9; i++) {
            setArr[i] = new ArrayList<>();
            setArr[i].add(t); // 현재 숫자를 해당하는 setArr의 ArrayList에 추가
            t = t * 10 + N; // 다음 숫자 생성 (5, 55, 555, ...)
        }

        // DP(Dynamic Programming)를 사용하여 사칙연산 결과를 계산하여 setArr에 저장
        for(int i = 1; i < 9; i++) {
            for(int j = 1; j < i; j++) {
                for(int k = 0; k < setArr[j].size(); k++) {
                    for(int l = 0; l < setArr[i - j].size(); l++) {
                        int a = setArr[j].get(k); // 첫 번째 숫자
                        int b = setArr[i - j].get(l); // 두 번째 숫자
                        // 사칙연산 결과를 setArr에 추가
                        setArr[i].add(a + b);
                        setArr[i].add(a - b);
                        setArr[i].add(b - a);
                        setArr[i].add(a * b);
                        if(b != 0) { // 0으로 나누는 경우 예외 처리
                            setArr[i].add(a / b);
                        }
                        if(a != 0) { // 0으로 나누는 경우 예외 처리
                            setArr[i].add(b / a);
                        }
                    }
                }
            }
        }

        // number를 만들 수 있는 최소 횟수를 찾아 반환
        for(int i = 1; i < 9; i++) {
            if(setArr[i].contains(number)) { // 해당하는 숫자가 있는지 확인
                answer = i; // 최소 횟수를 저장
                break; // 최소 횟수를 찾았으므로 반복 중단
            }
        }
        return answer; // 최소 횟수 반환
    }
}
```