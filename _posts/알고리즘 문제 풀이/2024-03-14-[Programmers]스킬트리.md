---
title:  "스킬트리"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/49993

## 문제 제목 : 스킬트리

문제 설명
선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다.

예를 들어 선행 스킬 순서가 스파크 → 라이트닝 볼트 → 썬더일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.

위 순서에 없는 다른 스킬(힐링 등)은 순서에 상관없이 배울 수 있습니다. 따라서 스파크 → 힐링 → 라이트닝 볼트 → 썬더와 같은 스킬트리는 가능하지만, 썬더 → 스파크나 라이트닝 볼트 → 스파크 → 힐링 → 썬더와 같은 스킬트리는 불가능합니다.

선행 스킬 순서 skill과 유저들이 만든 스킬트리1를 담은 배열 skill_trees가 매개변수로 주어질 때, 가능한 스킬트리 개수를 return 하는 solution 함수를 작성해주세요.

제한 조건
스킬은 알파벳 대문자로 표기하며, 모든 문자열은 알파벳 대문자로만 이루어져 있습니다.
스킬 순서와 스킬트리는 문자열로 표기합니다.
예를 들어, C → B → D 라면 "CBD"로 표기합니다
선행 스킬 순서 skill의 길이는 1 이상 26 이하이며, 스킬은 중복해 주어지지 않습니다.
skill_trees는 길이 1 이상 20 이하인 배열입니다.
skill_trees의 원소는 스킬을 나타내는 문자열입니다.
skill_trees의 원소는 길이가 2 이상 26 이하인 문자열이며, 스킬이 중복해 주어지지 않습니다.
입출력 예
skill	skill_trees	return
"CBD"	["BACDE", "CBADF", "AECB", "BDA"]	2
입출력 예 설명
"BACDE": B 스킬을 배우기 전에 C 스킬을 먼저 배워야 합니다. 불가능한 스킬트립니다.
"CBADF": 가능한 스킬트리입니다.
"AECB": 가능한 스킬트리입니다.
"BDA": B 스킬을 배우기 전에 C 스킬을 먼저 배워야 합니다. 불가능한 스킬트리입니다.
스킬 트리: 유저가 스킬을 배울 순서 ↩

## 문제 풀이
```java
class Solution {
    // 주어진 스킬 트리 배열에서 주어진 스킬 순서를 만족하는 스킬 트리의 개수를 반환하는 함수
    public int solution(String skill, String[] skill_trees) {
        int answer = 0; // 유효한 스킬 트리의 개수를 저장하는 변수

        // 각 스킬 트리에 대해 순회
        for (int i = 0; i < skill_trees.length; i++) {
            // 현재 스킬 트리가 유효한지 확인하여 유효하다면 answer 증가
            if (isValidSkillTree(skill, skill_trees[i])) {
                answer++;
            }
        }

        return answer; // 유효한 스킬 트리의 개수 반환
    }

    // 주어진 스킬 트리가 주어진 스킬 순서를 만족하는지 확인하는 함수
    private boolean isValidSkillTree(String skill, String skill_tree) {
        int skillIndex = 0; // 스킬 순서를 나타내는 인덱스

        // 각 스킬 트리 문자에 대해 순회
        for (int j = 0; j < skill_tree.length(); j++) {
            char currentSkill = skill_tree.charAt(j); // 현재 스킬

            // 현재 스킬이 스킬 순서에 포함되는지 확인
            if (skill.indexOf(currentSkill) != -1) {
                // 현재 스킬이 스킬 순서의 다음 스킬인지 확인
                if (skill.charAt(skillIndex) == currentSkill) {
                    skillIndex++; // 다음 스킬로 인덱스 증가
                } else {
                    return false; // 올바른 순서가 아니라면 유효하지 않음
                }
            }
        }

        return true; // 유효한 스킬 트리인 경우 true 반환
    }
}

```