---
title:  "뒤에 있는 큰 수 찾기"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/154539

## 문제 제목 : 뒤에 있는 큰 수 찾기

문제 설명
정수로 이루어진 배열 numbers가 있습니다. 배열 의 각 원소들에 대해 자신보다 뒤에 있는 숫자 중에서 자신보다 크면서 가장 가까이 있는 수를 뒷 큰수라고 합니다.
정수 배열 numbers가 매개변수로 주어질 때, 모든 원소에 대한 뒷 큰수들을 차례로 담은 배열을 return 하도록 solution 함수를 완성해주세요. 단, 뒷 큰수가 존재하지 않는 원소는 -1을 담습니다.

제한사항
4 ≤ numbers의 길이 ≤ 1,000,000
1 ≤ numbers[i] ≤ 1,000,000
입출력 예
numbers	result
[2, 3, 3, 5]	[3, 5, 5, -1]
[9, 1, 5, 3, 6, 2]	[-1, 5, 6, 6, -1, -1]
입출력 예 설명
입출력 예 #1
2의 뒷 큰수는 3입니다. 첫 번째 3의 뒷 큰수는 5입니다. 두 번째 3 또한 마찬가지입니다. 5는 뒷 큰수가 없으므로 -1입니다. 위 수들을 차례대로 배열에 담으면 [3, 5, 5, -1]이 됩니다.

입출력 예 #2
9는 뒷 큰수가 없으므로 -1입니다. 1의 뒷 큰수는 5이며, 5와 3의 뒷 큰수는 6입니다. 6과 2는 뒷 큰수가 없으므로 -1입니다. 위 수들을 차례대로 배열에 담으면 [-1, 5, 6, 6, -1, -1]이 됩니다.

## 문제 풀이
```java
import java.util.*;

class Solution {
    // 반환 = 각 원소 자신보다 크고, 뒤에 위치한 것 중 가장 가까이 있는 수들을 차례로 담은 배열
    public int[] solution(int[] numbers) {
        // 결과를 담을 배열
        int[] answer = new int[numbers.length];
        // 인덱스를 담을 스택
        Stack<Integer> stack = new Stack<>();
        // 모든 원소에 대해 반복
        for (int i = 0; i < numbers.length; i++) {
            // 스택이 비어있지 않고, 스택의 가장 위에 있는 원소의 값이 현재 원소보다 작은 경우
            while (!stack.isEmpty() && numbers[stack.peek()] < numbers[i]) {
                // 스택에서 값을 꺼내서 해당 인덱스의 원소에 현재 원소 값을 저장
                answer[stack.pop()] = numbers[i];
            }
            // 현재 원소의 인덱스를 스택에 넣음
            stack.push(i);
        }
        // 스택에 남아있는 인덱스가 있다면 해당 원소들은 뒤에 큰 수가 없는 것이므로 -1로 채움
        while (!stack.isEmpty()) {
            answer[stack.pop()] = -1;
        }
        // 결과 반환
        return answer;
    }
}
```