---
title:  "멀리 뛰기"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/12914

## 문제 제목 : 멀리 뛰기

문제 설명
효진이는 멀리 뛰기를 연습하고 있습니다. 효진이는 한번에 1칸, 또는 2칸을 뛸 수 있습니다. 칸이 총 4개 있을 때, 효진이는
(1칸, 1칸, 1칸, 1칸)
(1칸, 2칸, 1칸)
(1칸, 1칸, 2칸)
(2칸, 1칸, 1칸)
(2칸, 2칸)
의 5가지 방법으로 맨 끝 칸에 도달할 수 있습니다. 멀리뛰기에 사용될 칸의 수 n이 주어질 때, 효진이가 끝에 도달하는 방법이 몇 가지인지 알아내, 여기에 1234567를 나눈 나머지를 리턴하는 함수, solution을 완성하세요. 예를 들어 4가 입력된다면, 5를 return하면 됩니다.

제한 사항
n은 1 이상, 2000 이하인 정수입니다.
입출력 예
n	result
4	5
3	3
입출력 예 설명
입출력 예 #1
위에서 설명한 내용과 같습니다.

입출력 예 #2
(2칸, 1칸)
(1칸, 2칸)
(1칸, 1칸, 1칸)
총 3가지 방법으로 멀리 뛸 수 있습니다.

## 문제 풀이
```java
class Solution {
    // 피보나치 수열 문제 1234567를 나눈
    public long solution(int n) {
        // 결과값을 저장할 변수 선언
        long answer = 0;
        // 피보나치 수열을 저장할 배열 선언
        long[] fb = new long[n + 2];
        // 초기값 설정
        fb[0] = 0;
        fb[1] = 1;
        fb[2] = 2;
        
        // 피보나치 수열 계산
        for(int i = 3; i <= n; i++){
            fb[i] = (fb[i - 1] + fb[i - 2]) % 1234567;
        }
        // 결과값 설정
        answer = fb[n];
        // 결과 반환
        return answer;
    }
}

```