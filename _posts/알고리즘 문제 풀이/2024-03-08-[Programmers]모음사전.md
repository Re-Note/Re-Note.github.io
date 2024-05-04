---
title:  "모음사전"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

https://school.programmers.co.kr/learn/courses/30/lessons/84512

## 모음사전
문제 설명
사전에 알파벳 모음 'A', 'E', 'I', 'O', 'U'만을 사용하여 만들 수 있는, 길이 5 이하의 모든 단어가 수록되어 있습니다. 사전에서 첫 번째 단어는 "A"이고, 그다음은 "AA"이며, 마지막 단어는 "UUUUU"입니다.

단어 하나 word가 매개변수로 주어질 때, 이 단어가 사전에서 몇 번째 단어인지 return 하도록 solution 함수를 완성해주세요.

제한사항
word의 길이는 1 이상 5 이하입니다.
word는 알파벳 대문자 'A', 'E', 'I', 'O', 'U'로만 이루어져 있습니다.
입출력 예
word	result
"AAAAE"	6
"AAAE"	10
"I"	1563
"EIO"	1189
입출력 예 설명
입출력 예 #1

사전에서 첫 번째 단어는 "A"이고, 그다음은 "AA", "AAA", "AAAA", "AAAAA", "AAAAE", ... 와 같습니다. "AAAAE"는 사전에서 6번째 단어입니다.

입출력 예 #2

"AAAE"는 "A", "AA", "AAA", "AAAA", "AAAAA", "AAAAE", "AAAAI", "AAAAO", "AAAAU"의 다음인 10번째 단어입니다.

입출력 예 #3

"I"는 1563번째 단어입니다.

입출력 예 #4

"EIO"는 1189번째 단어입니다.

## 문제 해결
```java
import java.util.*;

class Solution {
    // 단어의 모든 조합을 탐색해서 저장한뒤 word 문자열과 비교해서 같은 경우 해당 인덱스 반환
    // 백트래킹으로 단어를 하나씩 추가해가며 확인
    ArrayList<String> list = new ArrayList<>(); // 단어들을 저장할 ArrayList 선언
    char[] ch = {'A', 'E', 'I', 'O', 'U'}; // 주어진 문자 배열 선언

    // solution 메서드는 주어진 단어(word)의 순서를 찾는 메서드입니다.
    public int solution(String word) {
        // 백트래킹, 완전 탐색을 이용하여 가능한 모든 단어를 생성합니다.
        backtracking(0, "");

        // 생성된 단어들을 정렬합니다.
        Collections.sort(list);

        int answer = 0;
        // 주어진 단어와 생성된 단어들을 비교하여 주어진 단어의 순서를 찾습니다.
        for (int i = 0; i < list.size(); i++) {
            if (list.get(i).equals(word)) { // 리스트에 있는 단어와 주어진 단어를 비교합니다. => 같으면 찾은 것
                answer = i; // 주어진 단어의 인덱스를 저장합니다. => result 저장
                break; // 주어진 단어를 찾았으므로 반복문을 종료합니다.
            }
        }
        return answer; // 단어의 순서를 반환합니다. => result 반환
    }

    // 백트래킹을 수행하는 backtracking 메서드입니다.
    public void backtracking(int depth, String word) {
        list.add(word); // 생성된 단어를 리스트에 추가합니다.
        if (depth == 5) { // 단어가 5글자가 되면 반환합니다.
            return;
        }
        // 주어진 문자 배열의 각 문자를 조합하여 재귀적으로 단어를 생성합니다.
        for (int i = 0; i < ch.length; i++) {
            backtracking(depth + 1, word + ch[i]); // 다음 글자를 추가하여 재귀 호출합니다. 호출 결과는 A, AA, AAA, AAAA, AAAAA, AAAAE... 로 진행
        }
    }
}

```