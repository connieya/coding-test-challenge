# 알고리즘 문제 풀이 정리

---

## 📚 이분 탐색 (Binary Search)

### 매개변수 탐색 (Parametric Search)

### 일반 이분 탐색

### Lower Bound

- [프로그래머스 - 퍼즐 게임 챌린지](https://github.com/connieya/coding-test-challenge/pull/2) - 최적의 레벨 찾기

### Upper Bound

---

## 🔍 완전 탐색 (Brute Force)

### 모든 경우의 수 탐색

- [프로그래머스 - 수식 최대화](https://github.com/connieya/coding-test-challenge/pull/3) - 연산자 우선순위의 모든 순열 탐색
- [프로그래머스 - 비밀 코드 해독](https://github.com/connieya/coding-test-challenge/pull/4) - 5개 숫자 조합의 모든 경우 탐색
- [프로그래머스 - 바탕 화면 정리](https://github.com/connieya/coding-test-challenge/pull/6) - 모든 칸을 순회하며 파일 위치의 최소/최대 좌표 탐색
- [프로그래머스 - 광물 캐기](https://github.com/connieya/coding-test-challenge/pull/8) - 곡괭이 선택 순서를 DFS로 탐색해 최소 피로도 계산

---

## 🔄 백트래킹 (Backtracking)

### 상태 공간 탐색

- [프로그래머스 - 완전 범죄](https://github.com/connieya/coding-test-challenge/pull/1) - 두 가지 선택지가 있는 DFS
- [프로그래머스 - 광물 캐기](https://github.com/connieya/coding-test-challenge/pull/8) - 남은 곡괭이를 선택하며 최소 피로도를 찾는 DFS
- [프로그래머스 - N-Queen](https://github.com/connieya/coding-test-challenge/pull/25) - 각 행에 퀸을 배치하며 세로와 대각선 방향 공격 가능 여부를 체크하는 백트래킹

### 순열/조합 생성

- [프로그래머스 - 수식 최대화](https://github.com/connieya/coding-test-challenge/pull/3) - visited 배열을 사용한 연산자 우선순위 순열 생성
- [프로그래머스 - 비밀 코드 해독](https://github.com/connieya/coding-test-challenge/pull/4) - start 파라미터를 사용한 조합 생성
- [프로그래머스 - 양궁대회](https://github.com/connieya/coding-test-challenge/pull/19) - 각 점수에 대해 남은 화살을 0개부터 남은 화살까지 모든 경우를 시도하는 완전 탐색으로 최대 점수 차이 계산
- [프로그래머스 - 메뉴 리뉴얼](https://github.com/connieya/coding-test-challenge/pull/24) - DFS로 모든 조합을 생성하고 HashMap으로 주문 횟수를 카운팅하여 각 길이별 최대 주문 조합 찾기

---

## 🎯 그리디 (Greedy)

### 간격 스케줄링 (Interval Scheduling)

- [프로그래머스 - 요격 시스템](https://github.com/connieya/coding-test-challenge/pull/5) - 정렬 후 끝점 기준으로 겹치는 구간 처리
- [프로그래머스 - 호텔 대실](https://github.com/connieya/coding-test-challenge/pull/7) - 시작 시각 정렬 후 종료시각+청소시간으로 최소 객실 계산

### 자원 할당 (Resource Allocation)

- [프로그래머스 - 서버 증설](https://github.com/connieya/coding-test-challenge/pull/9) - 만료 시간 관리 큐로 운영 중 서버를 유지하며 부족분만 증설

### 최적 경로 찾기

- [프로그래머스 - 조이스틱](src/main/java/programmers/day21.md) - 각 알파벳 변경 최소 조작과 연속된 'A'를 건너뛰는 최적 커서 이동 경로 계산

---

## 💾 동적 프로그래밍 (Dynamic Programming)

### 2D DP

- [프로그래머스 - 공원](https://github.com/connieya/coding-test-challenge/pull/16) - 각 위치에서 만들 수 있는 가장 큰 정사각형 크기를 DP로 계산

---

## 🔁 시뮬레이션 (Simulation)

### 이동 시뮬레이션

- [프로그래머스 - 충돌 위험 찾기](https://github.com/connieya/coding-test-challenge/pull/10) - 시간+좌표 맵으로 동선 충돌 횟수 시뮬레이션
- [프로그래머스 - 리코쳇 로봇](https://github.com/connieya/coding-test-challenge/pull/12) - BFS로 장애물까지 미끄러지는 최단 경로 탐색

### 스택 기반 시뮬레이션

- [프로그래머스 - 과제 진행하기](https://github.com/connieya/coding-test-challenge/pull/11) - 스택으로 중단된 과제를 관리하며 시간 순서대로 처리

### 시간 기반 시뮬레이션

- [프로그래머스 - 붕대 감기](https://github.com/connieya/coding-test-challenge/pull/15) - 공격 시간 순서대로 체력 회복과 공격을 시뮬레이션
- [프로그래머스 - 동영상 재생기](https://github.com/connieya/coding-test-challenge/pull/17) - 명령어를 순차 처리하며 재생 위치를 관리하고 오프닝 구간 자동 건너뛰기

### 해시맵 기반 시뮬레이션

- [프로그래머스 - 달리기 경주](https://github.com/connieya/coding-test-challenge/pull/20) - HashMap으로 선수 등수를 관리하며 추월 시뮬레이션

### 거리 계산 시뮬레이션

- [프로그래머스 - 키패드 누르기](https://github.com/connieya/coding-test-challenge/pull/27) - 맨해튼 거리로 가운데 열 숫자 입력 시 더 가까운 손 선택

---

## 🔍 그래프 탐색 (Graph Traversal)

### BFS (너비 우선 탐색)

- [프로그래머스 - 리코쳇 로봇](https://github.com/connieya/coding-test-challenge/pull/12) - Queue를 사용한 최단 경로 탐색
- [프로그래머스 - 미로 탈출](https://github.com/connieya/coding-test-challenge/pull/13) - 2차원 배열로 거리를 저장하며 최단 경로 탐색

### Union-Find (Disjoint Set Union)

- [프로그래머스 - 혼자 놀기의 달인](https://github.com/connieya/coding-test-challenge/pull/18) - Union-Find로 상자 그룹을 찾고 가장 큰 두 그룹의 크기를 곱하여 최고 점수 계산

---

## 🔢 수학 (Mathematics)

### 비율/관계식

- [프로그래머스 - 시소 짝꿍](https://github.com/connieya/coding-test-challenge/pull/14) - 토크 균형 방정식(w1×d1 = w2×d2)과 비율(1:1, 1:2, 2:3, 3:4)을 활용한 문제

### 기하학/최대공약수

- [프로그래머스 - 멀쩡한 사각형](https://github.com/connieya/coding-test-challenge/pull/23) - 대각선이 지나가는 정사각형 개수를 최대공약수로 계산하여 사용 가능한 정사각형 개수 구하기

---

## 🔁 재귀/분할 정복 (Recursion/Divide and Conquer)

### 문자열 처리

- [프로그래머스 - 괄호 변환](https://github.com/connieya/coding-test-challenge/pull/22) - 균형잡힌 괄호 문자열을 재귀적으로 분리하여 올바른 괄호 문자열로 변환

### 하노이 탑

- [프로그래머스 - 하노이 탑](https://github.com/connieya/coding-test-challenge/pull/26) - n개의 원판을 3단계로 분해하여 재귀적으로 최소 이동 방법 구하기

---
