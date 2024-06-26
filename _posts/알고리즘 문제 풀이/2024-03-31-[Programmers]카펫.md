---
title:  "카펫"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42842

## 문제 제목 : 카펫

문제 설명
Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.

carpet.png

Leo는 집으로 돌아와서 아까 본 카펫의 노란색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.

Leo가 본 카펫에서 갈색 격자의 수 brown, 노란색 격자의 수 yellow가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

제한사항
갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
노란색 격자의 수 yellow는 1 이상 2,000,000 이하인 자연수입니다.
카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.
입출력 예
brown	yellow	return
10	2	[4, 3]
8	1	[3, 3]
24	24	[8, 6]
출처

※ 공지 - 2020년 2월 3일 테스트케이스가 추가되었습니다.
※ 공지 - 2020년 5월 11일 웹접근성을 고려하여 빨간색을 노란색으로 수정하였습니다.

## 문제 풀이
```java
class Solution {
    public int[] solution(int brown, int yellow) {
        // 갈색 + 노란색 = 카펫 넓이로 카펫의 가로 * 세로를 구해야함
        // 카펫의 넓이는 갈색 + 노란색의 약수

        // 약수를 구성할 수 있는 다양한 가로 * 세로 중에 정답인 가로 * 세로가 존재함.
        
        // 노란색 격자 테두리로 갈색 격자 사용 => 노란색 격자 1 => 전체 격자 한 변 길이 3
        // i = 전체 세로, width =  전체 가로 (단 i, width >= 3 이여야 함)
        
        // 정답을 저장할 배열 선언
        int[] answer = new int[2];
        
        // 가능한 카펫의 세로 길이를 3부터 시작하여 확인
        for(int i = 3; i < brown + yellow; i++){
            // 전체 가로 길이 계산
            int width = (brown + yellow) / i; // 가로 = (갈색 + 노란색) / 세로 => 갈색 + 노란색의 약수들 추출
            // 가로가 세로보다 크거나 같을 경우에만 확인
            if(width >= i){ // 가로 >= 세로 일때 
                // 노란색 격자의 넓이와 일치하는지 확인
                if((i - 2) * (width - 2) == yellow){ // 노란색 넓이 확인
                    // 정답을 배열에 저장
                    answer[0] = width; // 가로 저장
                    answer[1] = i; // 세로 저장
                    // 정답 반환
                    return answer; // 반환
                }
            }
        }
        // 정답이 없을 경우 빈 배열 반환
        return answer;
    }
}

```
