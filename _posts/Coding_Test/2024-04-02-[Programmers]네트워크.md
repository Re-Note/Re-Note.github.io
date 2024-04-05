---
title:  "네트워크"
categories: "coding_test"
tag: [coding_test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/43162

## 문제 제목 : 네트워크

문제 설명
네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.

컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

제한사항
컴퓨터의 개수 n은 1 이상 200 이하인 자연수입니다.
각 컴퓨터는 0부터 n-1인 정수로 표현합니다.
i번 컴퓨터와 j번 컴퓨터가 연결되어 있으면 computers[i][j]를 1로 표현합니다.
computer[i][i]는 항상 1입니다.
입출력 예
n	computers	return
3	[[1, 1, 0], [1, 1, 0], [0, 0, 1]]	2
3	[[1, 1, 0], [1, 1, 1], [0, 1, 1]]	1
입출력 예 설명
예제 #1
아래와 같이 2개의 네트워크가 있습니다.
image0.png

예제 #2
아래와 같이 1개의 네트워크가 있습니다.
image1.png

## 문제 풀이
```java
class Solution {
    public int solution(int n, int[][] computers) {
        boolean[] visited = new boolean[n]; // 각 컴퓨터의 방문 여부를 저장할 배열 생성
        int networkCount = 0; // 네트워크의 개수를 저장할 변수 초기화
        
        for (int i = 0; i < n; i++) { // 모든 컴퓨터에 대해 반복
            if (!visited[i]) { // 해당 컴퓨터를 방문하지 않았을 경우
                dfs(computers, visited, i); // 깊이 우선 탐색으로 컴퓨터 네트워크를 탐색
                networkCount++; // 새로운 네트워크 발견 시 네트워크 개수 증가
            }
        }
        
        return networkCount; // 모든 컴퓨터의 네트워크 탐색을 마친 후 네트워크 개수 반환
    }
    
    // 깊이 우선 탐색 함수
    private void dfs(int[][] computers, boolean[] visited, int node) {
        visited[node] = true; // 현재 노드를 방문했음을 표시
        for (int i = 0; i < computers.length; i++) { // 현재 노드와 연결된 모든 노드에 대해 반복
            if (computers[node][i] == 1 && !visited[i]) { // 현재 노드와 연결되어 있고 방문하지 않은 노드일 경우
                dfs(computers, visited, i); // 해당 노드를 방문하고 그 노드로부터 다시 깊이 우선 탐색 수행
            }
        }
    }
}

```