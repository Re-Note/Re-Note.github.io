---
title:  "나머지 한 점"
categories: "coding_test"
tag: [coding_test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/18/lessons/1878

## 문제 제목 : 나머지 한 점

문제 설명
직사각형을 만드는 데 필요한 4개의 점 중 3개의 좌표가 주어질 때, 나머지 한 점의 좌표를 구하려고 합니다. 점 3개의 좌표가 들어있는 배열 v가 매개변수로 주어질 때, 직사각형을 만드는 데 필요한 나머지 한 점의 좌표를 return 하도록 solution 함수를 완성해주세요. 단, 직사각형의 각 변은 x축, y축에 평행하며, 반드시 직사각형을 만들 수 있는 경우만 입력으로 주어집니다.

제한사항
v는 세 점의 좌표가 들어있는 2차원 배열입니다.
v의 각 원소는 점의 좌표를 나타내며, 좌표는 [x축 좌표, y축 좌표] 순으로 주어집니다.
좌표값은 1 이상 10억 이하의 자연수입니다.
직사각형을 만드는 데 필요한 나머지 한 점의 좌표를 [x축 좌표, y축 좌표] 순으로 담아 return 해주세요.
입출력 예
v	result
[[1, 4], [3, 4], [3, 10]]	[1, 10]
[[1, 1], [2, 2], [1, 2]]	[2, 1]
입출력 예 설명
입출력 예 #1
세 점이 [1, 4], [3, 4], [3, 10] 위치에 있을 때, [1, 10]에 점이 위치하면 직사각형이 됩니다.

입출력 예 #2
세 점이 [1, 1], [2, 2], [1, 2] 위치에 있을 때, [2, 1]에 점이 위치하면 직사각형이 됩니다.

## 문제 풀이
```java
import java.util.*;

class Solution {
    // 반환 = 나머지 한 점의 좌표
    public int[] solution(int[][] v) {
        // 답을 저장할 배열 선언
        int[] answer = new int[2];
        
        // X좌표의 출현 빈도를 저장할 맵
        Map<Integer, Integer> XfreMap = new HashMap<>();
        // Y좌표의 출현 빈도를 저장할 맵
        Map<Integer, Integer> YfreMap = new HashMap<>();
        
        // 모든 좌표에 대해 출현 빈도를 계산하고 맵에 저장
        for(int i = 0; i < v.length; i++){
            int x = v[i][0];
            int y = v[i][1];
            
            // X좌표의 출현 빈도를 계산하고 맵에 저장
            XfreMap.put(x, XfreMap.getOrDefault(x, 0) + 1);
            // Y좌표의 출현 빈도를 계산하고 맵에 저장
            YfreMap.put(y, YfreMap.getOrDefault(y, 0) + 1);
        }
        
        // 출현 빈도가 1인 좌표 찾기
        for(int i = 0; i < v.length; i++){
            int x = v[i][0];
            int y = v[i][1];
            
            // X좌표의 출현 빈도가 1인 경우 해당 좌표를 답 배열에 저장
            if(XfreMap.get(x) == 1) {
                answer[0] = x;
            }
            // Y좌표의 출현 빈도가 1인 경우 해당 좌표를 답 배열에 저장
            if(YfreMap.get(y) == 1) {
                answer[1] = y;
            }
        }
        // 답 배열 반환
        return answer;
    }
}

```