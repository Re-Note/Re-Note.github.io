---
title:  "귤 고르기"
categories: "coding_test"
tag: [coding_test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/138476

## 문제 제목 : 귤 고르기

문제 설명
경화는 과수원에서 귤을 수확했습니다. 경화는 수확한 귤 중 'k'개를 골라 상자 하나에 담아 판매하려고 합니다. 그런데 수확한 귤의 크기가 일정하지 않아 보기에 좋지 않다고 생각한 경화는 귤을 크기별로 분류했을 때 서로 다른 종류의 수를 최소화하고 싶습니다.

예를 들어, 경화가 수확한 귤 8개의 크기가 [1, 3, 2, 5, 4, 5, 2, 3] 이라고 합시다. 경화가 귤 6개를 판매하고 싶다면, 크기가 1, 4인 귤을 제외한 여섯 개의 귤을 상자에 담으면, 귤의 크기의 종류가 2, 3, 5로 총 3가지가 되며 이때가 서로 다른 종류가 최소일 때입니다.

경화가 한 상자에 담으려는 귤의 개수 k와 귤의 크기를 담은 배열 tangerine이 매개변수로 주어집니다. 경화가 귤 k개를 고를 때 크기가 서로 다른 종류의 수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

제한사항
1 ≤ k ≤ tangerine의 길이 ≤ 100,000
1 ≤ tangerine의 원소 ≤ 10,000,000
입출력 예
k	tangerine	result
6	[1, 3, 2, 5, 4, 5, 2, 3]	3
4	[1, 3, 2, 5, 4, 5, 2, 3]	2
2	[1, 1, 1, 1, 2, 2, 2, 3]	1
입출력 예 설명
입출력 예 #1

본문에서 설명한 예시입니다.
입출력 예 #2

경화는 크기가 2인 귤 2개와 3인 귤 2개 또는 2인 귤 2개와 5인 귤 2개 또는 3인 귤 2개와 5인 귤 2개로 귤을 판매할 수 있습니다. 이때의 크기 종류는 2가지로 이 값이 최소가 됩니다.
입출력 예 #3

경화는 크기가 1인 귤 2개를 판매하거나 2인 귤 2개를 판매할 수 있습니다. 이때의 크기 종류는 1가지로, 이 값이 최소가 됩니다.

## 문제 풀이
```java
import java.util.*;

class Solution {
    public int solution(int k, int[] tangerine) {
        int sum = 0; // 귤의 개수를 누적할 변수
        int cnt = 0; // 최종 결과값(선택한 귤의 그룹 수)을 저장할 변수
        Arrays.sort(tangerine); // 귤을 오름차순으로 정렬

        // 각 귤의 개수를 저장할 해시맵 생성
        Map<Integer, Integer> hash = new HashMap<>();
        for(int i = 0; i < tangerine.length; i++) {
            // 해당 귤이 이미 해시맵에 있으면 개수를 1 증가시킴
            if(hash.containsKey(tangerine[i])) {
                hash.put(tangerine[i], hash.get(tangerine[i]) + 1);
            } else { // 없으면 개수를 1로 설정하여 새로 추가함
                hash.put(tangerine[i], 1);
            }
        }
        
        // 각 귤의 개수를 리스트에 담아 내림차순으로 정렬
        ArrayList<Integer> valueList = new ArrayList<>(hash.values()); // hash.values() = 각 귤의 개수
        Collections.sort(valueList, Collections.reverseOrder());
        
        // System.out.println("valueList: " + valueList); // 출력
             
        // 귤의 개수를 내림차순으로 정렬된 리스트를 순회하며 선택할 귤의 그룹 수 계산
        for (int i = 0; i < valueList.size(); i++) {
            // 현재까지 선택한 귤의 개수가 목표 귤의 개수를 넘으면 반복문 종료
            if (sum >= k) {
                break;
            } else { // 아니면 현재 귤의 개수를 선택하여 누적하고 그룹 수를 증가시킴
                sum += valueList.get(i);
                cnt++;
            }
        }
        return cnt; // 선택한 귤의 그룹 수 반환
    }
}

```