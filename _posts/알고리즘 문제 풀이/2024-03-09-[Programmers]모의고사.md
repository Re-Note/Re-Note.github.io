---
title:  "모의고사"
categories: "Algorithm_Test"
tag: [Algorithm_Test]
toc: true
---

### 문제 링크 : https://school.programmers.co.kr/learn/courses/30/lessons/42840

## 문제 제목 : 모의고사

문제 설명
수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

제한 조건
시험은 최대 10,000 문제로 구성되어있습니다.
문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.
입출력 예
answers	return
[1,2,3,4,5]	[1]
[1,3,2,4,2]	[1,2,3]
입출력 예 설명
입출력 예 #1

수포자 1은 모든 문제를 맞혔습니다.
수포자 2는 모든 문제를 틀렸습니다.
수포자 3은 모든 문제를 틀렸습니다.
따라서 가장 문제를 많이 맞힌 사람은 수포자 1입니다.

입출력 예 #2

모든 사람이 2문제씩을 맞췄습니다.

## 문제 풀이
```java
import java.util.*;

class Solution {
    public int[] solution(int[] answers) {
        int[] pattern1 = {1,2,3,4,5};
        int[] pattern2 = {2,1,2,3,2,4,2,5};
        int[] pattern3 = {3,3,1,1,2,2,4,4,5,5};
        int count1 = 0;
        int count2 = 0;
        int count3 = 0;

        // 각 학생이 맞힌 문제의 개수를 세는 부분
        for(int i = 0; i < answers.length; i++){
            if(answers[i] == pattern1[i % pattern1.length]) count1++;
            if(answers[i] == pattern2[i % pattern2.length]) count2++;
            if(answers[i] == pattern3[i % pattern3.length]) count3++;
        }

        // 가장 많은 문제를 맞힌 개수 구하기
        int maxCount = Math.max(count1, Math.max(count2, count3));

        // 가장 많은 문제를 맞힌 학생들을 저장할 배열
        int[] resultArray = new int[3];
        int index = 0;

        // 가장 많은 문제를 맞힌 학생들의 번호를 배열에 추가
        if (count1 == maxCount) resultArray[index++] = 1;
        if (count2 == maxCount) resultArray[index++] = 2;
        if (count3 == maxCount) resultArray[index++] = 3;

        // 결과 배열의 크기를 조정하여 중복된 값이 없도록 함
        int[] answer = new int[index];
        for (int i = 0; i < index; i++) {
            answer[i] = resultArray[i];
        }
        return answer;
    }
}

```