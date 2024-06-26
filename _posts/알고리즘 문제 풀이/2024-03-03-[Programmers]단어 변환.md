---
title:  "단어 변환"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/43163

## 문제 제목 : 단어 변환

문제 설명
두 개의 단어 begin, target과 단어의 집합 words가 있습니다. 아래와 같은 규칙을 이용하여 begin에서 target으로 변환하는 가장 짧은 변환 과정을 찾으려고 합니다.

1. 한 번에 한 개의 알파벳만 바꿀 수 있습니다.
2. words에 있는 단어로만 변환할 수 있습니다.
예를 들어 begin이 "hit", target가 "cog", words가 ["hot","dot","dog","lot","log","cog"]라면 "hit" -> "hot" -> "dot" -> "dog" -> "cog"와 같이 4단계를 거쳐 변환할 수 있습니다.

두 개의 단어 begin, target과 단어의 집합 words가 매개변수로 주어질 때, 최소 몇 단계의 과정을 거쳐 begin을 target으로 변환할 수 있는지 return 하도록 solution 함수를 작성해주세요.

제한사항
각 단어는 알파벳 소문자로만 이루어져 있습니다.
각 단어의 길이는 3 이상 10 이하이며 모든 단어의 길이는 같습니다.
words에는 3개 이상 50개 이하의 단어가 있으며 중복되는 단어는 없습니다.
begin과 target은 같지 않습니다.
변환할 수 없는 경우에는 0를 return 합니다.
입출력 예
begin	target	words	return
"hit"	"cog"	["hot", "dot", "dog", "lot", "log", "cog"]	4
"hit"	"cog"	["hot", "dot", "dog", "lot", "log"]	0
입출력 예 설명
예제 #1
문제에 나온 예와 같습니다.

예제 #2
target인 "cog"는 words 안에 없기 때문에 변환할 수 없습니다.

## 문제 풀이
```java
class Solution {
    boolean[] visited; // 방문한 단어를 추적하기 위한 배열
    int answer = 0; // 최소 변경 횟수를 저장하기 위한 변수

    // 주어진 시작 단어(begin), 목표 단어(target), 그리고 단어 리스트(words)로부터 최소 변경 횟수를 구하는 메서드
    public int solution(String begin, String target, String[] words) {
        visited = new boolean[words.length]; // 방문 배열 초기화
        
        // 깊이 우선 탐색 실행
        dfs(begin, target, words, 0);
        
        return answer; // 최소 변경 횟수 반환
    }
    
    // 깊이 우선 탐색 메서드
    public void dfs(String begin, String target, String[] words, int cnt){
        // 시작 단어와 목표 단어가 같으면 최소 변경 횟수를 설정하고 종료
        if(begin.equals(target)){
            answer = cnt;
            return;
        }
        
        // 단어 리스트를 탐색하여 시작 단어와 한 글자만 다른 단어를 찾음
        for(int i = 0; i < words.length; i++){
            // 이미 방문한 단어인 경우 건너뜀
            if(visited[i]){
                continue;
            }
            int k = 0;
            // 시작 단어와 현재 단어를 비교하여 한 글자만 다른지 확인
            for(int j = 0; j < begin.length(); j++){
                if(begin.charAt(j) != words[i].charAt(j)){
                    k++;
                }
            }
            // 한 글자만 다른 경우 깊이 우선 탐색 실행
            if(k == 1){
                visited[i] = true; // 단어를 방문했음을 표시
                dfs(words[i], target, words, cnt + 1); // 다음 단계의 깊이 우선 탐색 실행
                visited[i] = false; // 깊이 우선 탐색 이후 해당 단어의 방문 표시 해제 (backtracking)
            }
        }
    }
}

```