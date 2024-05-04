---
title:  "같은 숫자는 싫어"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

https://school.programmers.co.kr/learn/courses/30/lessons/12906

## 같은 숫자는 싫어

문제 설명
배열 arr가 주어집니다. 배열 arr의 각 원소는 숫자 0부터 9까지로 이루어져 있습니다. 이때, 배열 arr에서 연속적으로 나타나는 숫자는 하나만 남기고 전부 제거하려고 합니다. 단, 제거된 후 남은 수들을 반환할 때는 배열 arr의 원소들의 순서를 유지해야 합니다. 예를 들면,

arr = [1, 1, 3, 3, 0, 1, 1] 이면 [1, 3, 0, 1] 을 return 합니다.
arr = [4, 4, 4, 3, 3] 이면 [4, 3] 을 return 합니다.
배열 arr에서 연속적으로 나타나는 숫자는 제거하고 남은 수들을 return 하는 solution 함수를 완성해 주세요.

제한사항
배열 arr의 크기 : 1,000,000 이하의 자연수
배열 arr의 원소의 크기 : 0보다 크거나 같고 9보다 작거나 같은 정수
입출력 예
arr	answer
[1,1,3,3,0,1,1]	[1,3,0,1]
[4,4,4,3,3]	[4,3]
입출력 예 설명
입출력 예 #1,2
문제의 예시와 같습니다.

## 문제 풀이
```java
import java.util.*;

public class Solution {
    // 반환 = 중복값이 제거된 배열
    // 저장용 answer ArrayList 사용
    public List<Integer> solution(int []arr) {
        // 중복값이 제거된 배열을 저장할 리스트 생성
        List<Integer> answer = new ArrayList<>();
        // 배열의 첫 번째 요소를 answer 리스트에 추가
        answer.add(arr[0]);
        // 배열을 순회하며 중복값을 제거하여 answer 리스트에 추가
        for(int i = 1; i < arr.length; i++){
            // 현재 요소가 바로 이전 요소와 다를 경우에만 추가
            if(arr[i] != arr[i - 1]){
                answer.add(arr[i]);
            }
        }
        // 중복값이 제거된 배열 리스트 반환
        return answer;
    }
}
```