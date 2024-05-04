---
title:  "행렬의 곱셈"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/12949

## 문제 제목 : 행렬의 곱셈

문제 설명
2차원 행렬 arr1과 arr2를 입력받아, arr1에 arr2를 곱한 결과를 반환하는 함수, solution을 완성해주세요.

제한 조건
행렬 arr1, arr2의 행과 열의 길이는 2 이상 100 이하입니다.
행렬 arr1, arr2의 원소는 -10 이상 20 이하인 자연수입니다.
곱할 수 있는 배열만 주어집니다.
입출력 예
arr1	arr2	return
[[1, 4], [3, 2], [4, 1]]	[[3, 3], [3, 3]]	[[15, 15], [15, 15], [15, 15]]
[[2, 3, 2], [4, 2, 4], [3, 1, 4]]	[[5, 4, 3], [2, 4, 1], [3, 1, 1]]	[[22, 22, 11], [36, 28, 18], [29, 20, 14]]

## 문제 풀이
```java
class Solution {
    // 반환 = 행렬의 곱
    // 1 * 3 + 4 * 3 = 15
    // ...

    // 두 개의 2차원 배열을 받아서 행렬의 곱을 계산하는 함수
    public int[][] solution(int[][] arr1, int[][] arr2) {
        // 행렬 곱 결과를 저장할 배열 생성
        int[][] answer = new int[arr1.length][arr2[0].length];
        // arr1의 행 길이만큼 반복
        for(int i = 0 ; i < arr1.length ; ++i){
            // arr2의 열 길이만큼 반복
            for(int j = 0 ; j < arr2[0].length ; ++j){
                // arr1의 열 길이만큼 반복하며 행렬의 곱 계산
                for(int k = 0 ; k < arr1[0].length ; ++k) {
                    // answer[i][j]에 arr1의 i행과 arr2의 j열 각 원소들의 곱을 더함
                    answer[i][j] += arr1[i][k] * arr2[k][j];
                }
            }
        }
        // 행렬 곱 결과 반환
        return answer;
    }
}
```