---
title:  "K번째수"
categories: "coding_test"
tag: [coding_test]
toc: true
---

https://school.programmers.co.kr/learn/courses/30/lessons/42748

## K번째수

문제 설명
배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
2에서 나온 배열의 3번째 숫자는 5입니다.
배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

제한사항
array의 길이는 1 이상 100 이하입니다.
array의 각 원소는 1 이상 100 이하입니다.
commands의 길이는 1 이상 50 이하입니다.
commands의 각 원소는 길이가 3입니다.
입출력 예
array	commands	return
[1, 5, 2, 6, 3, 7, 4]	[[2, 5, 3], [4, 4, 1], [1, 7, 3]]	[5, 6, 3]
입출력 예 설명
[1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다. [2, 3, 5, 6]의 세 번째 숫자는 5입니다.
[1, 5, 2, 6, 3, 7, 4]를 4번째부터 4번째까지 자른 후 정렬합니다. [6]의 첫 번째 숫자는 6입니다.
[1, 5, 2, 6, 3, 7, 4]를 1번째부터 7번째까지 자릅니다. [1, 2, 3, 4, 5, 6, 7]의 세 번째 숫자는 3입니다.

## 문제 해결
```java
import java.util.Arrays;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        // 결과 배열의 크기를 commands 배열의 길이로 설정합니다.
        int[] answer = new int[commands.length];
        
        // commands 배열의 각 행에 대해 반복합니다.
        for(int n = 0; n < commands.length; n++){
            // i, j, k 값을 추출합니다.
            int i = commands[n][0]; // 부분 배열의 시작 인덱스
            int j = commands[n][1]; // 부분 배열의 끝 인덱스
            int k = commands[n][2]; // k번째 작은 수
            
            // 부분 배열의 길이만큼의 크기를 가진 임시 배열을 생성합니다.
            int[] idxArray = new int[j - i + 1];
            int idx = 0; // 임시 배열에 값을 채우기 위한 인덱스 변수
            
            // 원본 배열에서 부분 배열을 추출하여 임시 배열에 저장합니다.
            for(int l = i - 1; l < j; l++){
                idxArray[idx] = array[l];
                idx++;
            }
            
            // 부분 배열을 오름차순으로 정렬합니다.
            Arrays.sort(idxArray);
            
            // k번째 원소를 결과 배열에 저장합니다.
            answer[n] = idxArray[k - 1];
        }
        // 결과 배열을 반환합니다.
        return answer;
    }
}

```