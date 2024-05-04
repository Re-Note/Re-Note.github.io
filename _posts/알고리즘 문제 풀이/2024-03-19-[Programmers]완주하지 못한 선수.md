---
title:  "완주하지 못한 선수"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

https://school.programmers.co.kr/learn/courses/30/lessons/42576

## 완주하지 못한 선수

문제 설명
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

제한사항
마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
completion의 길이는 participant의 길이보다 1 작습니다.
참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
참가자 중에는 동명이인이 있을 수 있습니다.
입출력 예
participant	completion	return
["leo", "kiki", "eden"]	["eden", "kiki"]	"leo"
["marina", "josipa", "nikola", "vinko", "filipa"]	["josipa", "filipa", "marina", "nikola"]	"vinko"
["mislav", "stanko", "mislav", "ana"]	["stanko", "ana", "mislav"]	"mislav"
입출력 예 설명
예제 #1
"leo"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #2
"vinko"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #3
"mislav"는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.

※ 공지 - 2023년 01월 25일 테스트케이스가 추가되었습니다.

## 문제 풀이
```java
import java.util.*;

class Solution {
    // 주어진 참가자 배열과 완주자 배열을 받아서 완주하지 못한 참가자를 찾는 메소드
    public String solution(String[] participant, String[] completion) {
        String answer = "";

        // 해시 맵 생성 - 이름과 해당 이름의 출현 횟수를 저장하는데 사용
        HashMap<String, Integer> map = new HashMap<>();

        // participant 배열의 각 이름과 개수 저장
        for (int i = 0; i < participant.length; i++) {
            String p = participant[i];
            // put 메소드를 이용해 이름을 key로 하고, 해당 이름의 출현 횟수를 value로 하는 해시 맵을 생성
            // getOrDefault 메소드는 주어진 키에 해당하는 값이 있으면 그 값을 반환하고 없으면 기본값인 0을 반환한다.
            // 이를 활용하여 해당 이름이 이전에 등장한 적이 없으면 0을 반환하고, 그 외의 경우에는 해당 값에 1을 더해 출현 횟수를 업데이트한다.
            map.put(p, map.getOrDefault(p, 0) + 1);
        }

        // completion 배열의 각 이름에 해당하는 개수 감소
        for (int i = 0; i < completion.length; i++) {
            String c = completion[i];
            // 해당 이름이 완주자 명단에 있으면 출현 횟수를 감소시킨다.
            map.put(c, map.get(c) - 1);
        }

        // 해시 맵을 순회하며 개수가 0보다 큰 경우 answer에 저장
        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            if (entry.getValue() > 0) {
                // 출현 횟수가 0보다 큰 경우, 해당 이름은 완주하지 못한 참가자이다.
                // 따라서 이 이름을 정답으로 저장하고 루프를 종료한다.
                answer = entry.getKey();
                break;
            }
        }

        return answer;
    }
}

```