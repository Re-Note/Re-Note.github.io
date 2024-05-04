---
title:  "섬 연결하기"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42861

## 문제 제목 : 섬 연결하기

문제 설명
n개의 섬 사이에 다리를 건설하는 비용(costs)이 주어질 때, 최소의 비용으로 모든 섬이 서로 통행 가능하도록 만들 때 필요한 최소 비용을 return 하도록 solution을 완성하세요.

다리를 여러 번 건너더라도, 도달할 수만 있으면 통행 가능하다고 봅니다. 예를 들어 A 섬과 B 섬 사이에 다리가 있고, B 섬과 C 섬 사이에 다리가 있으면 A 섬과 C 섬은 서로 통행 가능합니다.

제한사항

섬의 개수 n은 1 이상 100 이하입니다.
costs의 길이는 ((n-1) * n) / 2이하입니다.
임의의 i에 대해, costs[i][0] 와 costs[i] [1]에는 다리가 연결되는 두 섬의 번호가 들어있고, costs[i] [2]에는 이 두 섬을 연결하는 다리를 건설할 때 드는 비용입니다.
같은 연결은 두 번 주어지지 않습니다. 또한 순서가 바뀌더라도 같은 연결로 봅니다. 즉 0과 1 사이를 연결하는 비용이 주어졌을 때, 1과 0의 비용이 주어지지 않습니다.
모든 섬 사이의 다리 건설 비용이 주어지지 않습니다. 이 경우, 두 섬 사이의 건설이 불가능한 것으로 봅니다.
연결할 수 없는 섬은 주어지지 않습니다.
입출력 예

n	costs	return
4	[[0,1,1],[0,2,2],[1,2,5],[1,3,1],[2,3,8]]	4
입출력 예 설명

costs를 그림으로 표현하면 다음과 같으며, 이때 초록색 경로로 연결하는 것이 가장 적은 비용으로 모두를 통행할 수 있도록 만드는 방법입니다.

image.png

## 문제 풀이
```java
import java.util.*;

// Solution 클래스 시작
class Solution {
    // solution 메소드 시작
    public int solution(int n, int[][] costs) {
        // answer 변수 초기화
        int answer = 0;
        // island 배열 초기화: 섬의 개수만큼 생성
        int[] island = new int[n];

        // 각 섬의 대표(부모)를 자기 자신으로 설정
        for (int i = 0; i < n; i++) {
            island[i] = i;
        }

        // 건설 비용을 기준으로 비용 오름차순으로 정렬
        Arrays.sort(costs, (a, b) -> Integer.compare(a[2], b[2]));

        // 모든 연결 가능한 섬 쌍을 확인하여 최소 비용으로 연결하기
        for (int i = 0; i < costs.length; i++) {
            // 두 섬의 대표가 다를 경우에만 연결하고 비용을 더함
            if (find(island, costs[i][0]) != find(island, costs[i][1])) {
                // 두 섬을 연결하고 연결 비용을 더함
                unite(island, costs[i][0], costs[i][1]);
                answer += costs[i][2];
            }
        }

        // 최소 비용 반환
        return answer;
    }
    // solution 메소드 끝

    // 대표(부모) 찾기 메소드 시작
    private int find(int[] island, int x) {
        // 현재 섬이 자신을 대표로 가질 때까지 재귀적으로 대표를 찾음
        if (island[x] == x) {
            return x;
        }
        return find(island, island[x]);
    }
    // 대표(부모) 찾기 메소드 끝

    // 두 섬을 연결하는 메소드 시작
    private void unite(int[] island, int x, int y) {
        // 두 섬의 대표(부모)를 찾음
        int a = find(island, x);
        int b = find(island, y);
        // 한 섬의 대표를 다른 섬의 대표로 변경하여 연결
        island[a] = b;
    }
    // 두 섬을 연결하는 메소드 끝
}
// Solution 클래스 끝

```