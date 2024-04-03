---
title:  "소수찾기"
categories: "coding_test"
tag: [coding_test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42839

## 문제 제목 : 소수찾기

문제 설명
한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

제한사항
numbers는 길이 1 이상 7 이하인 문자열입니다.
numbers는 0~9까지 숫자만으로 이루어져 있습니다.
"013"은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.
입출력 예
numbers	return
"17"	3
"011"	2
입출력 예 설명
예제 #1
[1, 7]으로는 소수 [7, 17, 71]를 만들 수 있습니다.

예제 #2
[0, 1, 1]으로는 소수 [11, 101]를 만들 수 있습니다.

11과 011은 같은 숫자로 취급합니다.

## 문제 풀이
```java
import java.util.*;

class Solution {
    public int solution(String numbers) {
        Set<Integer> primeSet = new HashSet<>();
        char[] numArr = numbers.toCharArray();
        boolean[] visited = new boolean[numbers.length()];
        makePermutation(numArr, visited, "", primeSet);
        int answer = 0;
        // primeSet에 있는 각 숫자에 대해 반복하여 소수인지 확인
        for (int num : primeSet) {
            // 소수 판별
            if (isPrime(num)) {
                answer++; // 소수인 경우 카운트 증가
            }
        }
        return answer;
    }
    
    private void makePermutation(char[] numArr, boolean[] visited, String permutation, Set<Integer> primeSet){
        if(!permutation.equals("")){
            primeSet.add(Integer.parseInt(permutation));
        }
        for(int i = 0; i < numArr.length; i++){
            if(!visited[i]){
                visited[i] = true;
                makePermutation(numArr, visited, permutation + numArr[i], primeSet);
                visited[i] = false;
            }
        }
    }
    
    private boolean isPrime(int num){
        if(num <= 1){
            return false;
        }
        for(int i = 2; i * i <= num; i++){
            if(num % i == 0){
                return false;
            }
        }
        return true;
    }
}
```