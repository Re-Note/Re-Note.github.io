---
title:  "K진수에서 소수 개수 구하기"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/92335

## 문제 제목 : k진수에서 소수 개수 구하기

문제 설명
문제 설명
양의 정수 n이 주어집니다. 이 숫자를 k진수로 바꿨을 때, 변환된 수 안에 아래 조건에 맞는 소수(Prime number)가 몇 개인지 알아보려 합니다.

0P0처럼 소수 양쪽에 0이 있는 경우
P0처럼 소수 오른쪽에만 0이 있고 왼쪽에는 아무것도 없는 경우
0P처럼 소수 왼쪽에만 0이 있고 오른쪽에는 아무것도 없는 경우
P처럼 소수 양쪽에 아무것도 없는 경우
단, P는 각 자릿수에 0을 포함하지 않는 소수입니다.
예를 들어, 101은 P가 될 수 없습니다.
예를 들어, 437674을 3진수로 바꾸면 211020101011입니다. 여기서 찾을 수 있는 조건에 맞는 소수는 왼쪽부터 순서대로 211, 2, 11이 있으며, 총 3개입니다. (211, 2, 11을 k진법으로 보았을 때가 아닌, 10진법으로 보았을 때 소수여야 한다는 점에 주의합니다.) 211은 P0 형태에서 찾을 수 있으며, 2는 0P0에서, 11은 0P에서 찾을 수 있습니다.

정수 n과 k가 매개변수로 주어집니다. n을 k진수로 바꿨을 때, 변환된 수 안에서 찾을 수 있는 위 조건에 맞는 소수의 개수를 return 하도록 solution 함수를 완성해 주세요.

제한사항
1 ≤ n ≤ 1,000,000
3 ≤ k ≤ 10
입출력 예
n	k	result
437674	3	3
110011	10	2
입출력 예 설명
입출력 예 #1

문제 예시와 같습니다.

입출력 예 #2

110011을 10진수로 바꾸면 110011입니다. 여기서 찾을 수 있는 조건에 맞는 소수는 11, 11 2개입니다. 이와 같이, 중복되는 소수를 발견하더라도 모두 따로 세어야 합니다.

문제가 잘 안풀린다면😢
힌트가 필요한가요? [코딩테스트 연습 힌트 모음집]으로 오세요! → 클릭

## 문제 풀이
```java
class Solution {
    
    // 소수 판별 함수: 주어진 정수 num이 소수인지 판별합니다.
    public boolean isPrime(long num){
        if(num == 1){ // 1은 소수가 아니므로 false를 반환합니다.
            return false;
        }
        // 2부터 num의 제곱근까지의 숫자로 num이 나누어지는지 확인합니다.
        for(int i = 2; i <= Math.sqrt(num); i++){
            if(num % i == 0){ // 나누어 떨어지면 소수가 아니므로 false를 반환합니다.
                return false;
            }
        }
        return true; // 위 조건을 모두 통과하면 소수이므로 true를 반환합니다.
    }
    
    // 주어진 정수 n을 k진수로 변환하고, 변환된 문자열에서 소수를 찾는 함수
    public int solution(int n, int k) {
        int answer = 0; // 소수의 개수를 저장할 변수
        
        // 정수 n을 k진수로 변환한 문자열을 얻습니다.
        String str = Integer.toString(n, k);
        // 변환된 문자열을 '0'을 기준으로 분리하여 배열에 저장합니다.
        String[] arr = str.split("0");
        
        // 배열의 각 요소를 확인합니다.
        for(int i = 0; i < arr.length; i++){
            if(arr[i].equals("")){ // 빈 문자열은 건너뜁니다.
                continue;
            }
            // 문자열을 정수로 변환합니다.
            long num = Long.parseLong(arr[i]); // int로 하면 제한, long을 사용.
            // 변환된 정수가 소수인지 확인하고, 소수이면 answer를 증가시킵니다.
            if(isPrime(num)){
                answer++;
            }
        }
        System.out.println(str); // 변환된 k진수 문자열을 출력합니다.
        return answer; // 소수의 개수를 반환합니다.
    }
}
```