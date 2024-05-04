---
title:  "타겟 넘버"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/43165

## 문제 제목 : 타겟 넘버

문제 설명
n개의 음이 아닌 정수들이 있습니다. 이 정수들을 순서를 바꾸지 않고 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

제한사항
주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
각 숫자는 1 이상 50 이하인 자연수입니다.
타겟 넘버는 1 이상 1000 이하인 자연수입니다.
입출력 예
numbers	target	return
[1, 1, 1, 1, 1]	3	5
[4, 1, 2, 1]	4	2
입출력 예 설명
입출력 예 #1

문제 예시와 같습니다.

입출력 예 #2

+4+1-2+1 = 4
+4-1+2-1 = 4
총 2가지 방법이 있으므로, 2를 return 합니다.

## 문제 풀이
```java
class Solution {
    // 반환 = target에 +1 또는 -1을 해서 타겟 넘버를 만드는 방법의 수
    // 함수 dfs로 깊이 우선 탐색을 사용
    int answer = 0; // 결과값을 저장할 변수
    
    public int solution(int[] numbers, int target) { // 주어진 숫자 배열과 타겟 넘버를 이용하여 타겟 넘버를 만드는 방법의 수를 반환하는 메소드
        dfs(numbers, target, 0, 0); // 깊이 우선 탐색 메소드 호출
        return answer; // 결과값 반환
    }
    
    public void dfs(int[] numbers, int target, int idx, int sum){ // 깊이 우선 탐색 메소드
        if(idx == numbers.length){ // 배열의 끝에 도달했을 때
            if(target == sum){ // 타겟 넘버를 만들었을 때
                answer++; // 결과값 증가
            }
            return; // 종료
        }
        dfs(numbers, target, idx+1, sum+numbers[idx]); // 현재 숫자를 더해서 다음 인덱스로 이동하는 경우
        dfs(numbers, target, idx+1, sum-numbers[idx]); // 현재 숫자를 빼서 다음 인덱스로 이동하는 경우
    }
}
```