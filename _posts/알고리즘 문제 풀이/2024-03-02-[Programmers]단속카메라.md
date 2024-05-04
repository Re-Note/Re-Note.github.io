---
title:  "단속카메라"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42884

## 문제 제목 : 단속카메라

문제 설명
고속도로를 이동하는 모든 차량이 고속도로를 이용하면서 단속용 카메라를 한 번은 만나도록 카메라를 설치하려고 합니다.

고속도로를 이동하는 차량의 경로 routes가 매개변수로 주어질 때, 모든 차량이 한 번은 단속용 카메라를 만나도록 하려면 최소 몇 대의 카메라를 설치해야 하는지를 return 하도록 solution 함수를 완성하세요.

제한사항

차량의 대수는 1대 이상 10,000대 이하입니다.
routes에는 차량의 이동 경로가 포함되어 있으며 routes[i][0]에는 i번째 차량이 고속도로에 진입한 지점, routes[i][1]에는 i번째 차량이 고속도로에서 나간 지점이 적혀 있습니다.
차량의 진입/진출 지점에 카메라가 설치되어 있어도 카메라를 만난것으로 간주합니다.
차량의 진입 지점, 진출 지점은 -30,000 이상 30,000 이하입니다.
입출력 예

routes	return
[[-20,-15], [-14,-5], [-18,-13], [-5,-3]]	2
입출력 예 설명

-5 지점에 카메라를 설치하면 두 번째, 네 번째 차량이 카메라를 만납니다.

-15 지점에 카메라를 설치하면 첫 번째, 세 번째 차량이 카메라를 만납니다.

## 문제 풀이
```java
import java.util.*;

class Solution {
    // 메인 solution 메소드
    public int solution(int[][] routes) {
        // routes 배열을 차량의 진입 지점을 기준으로 오름차순으로 정렬한다.
        Arrays.sort(routes, (a, b) -> Integer.compare(a[0], b[0]));
        // 카메라 설치 개수를 나타내는 변수를 1로 초기화한다.
        int answer = 1;
        // 카메라의 위치를 차량의 첫 번째 진출 지점으로 초기화한다.
        int camera = routes[0][1];
        
        // routes 배열을 순회하면서 카메라 설치 여부를 판단한다.
        for(int i = 1; i < routes.length; i++){
            // 현재 카메라의 위치(camera)가 다음 차량의 진입 지점보다 뒤에 있을 때
            if(camera < routes[i][0]){ // 새로운 카메라를 설치한다.
                camera = routes[i][1]; // 카메라의 위치를 다음 차량의 진출 지점으로 업데이트한다.
                answer++; // 카메라 설치 개수를 증가시킨다.
            } 
            // 현재 카메라의 위치(camera)가 다음 차량의 진입 지점보다 앞에 있거나 같을 때
            else { 
                // 다음 차량의 진입 지점보다 카메라 위치가 앞에 있거나 같으면 카메라를 그대로 유지한다.
                // 이전 카메라와 현재 차량의 진출 지점 중 더 작은 값을 선택하여 카메라 위치를 업데이트한다.
                camera = Math.min(camera, routes[i][1]); 
            }
        }
        // 최종적으로 설치된 카메라 개수를 반환한다.
        return answer;
    }
}

```