# 복잡도
- `시간 복잡도` : 알고리즘을 위해 필요한 연산의 횟수
- `공간 복잡도` : 알고리즘을 위해 필요한 메모리의 양
- trade-off
  - 메모리를 조금 더 사용하며 반복되는 연산 생략
  - or 더 많은 정보를 관리하면서 계산의 복잡도 감소

## 시간 복잡도
- 점근적 표기법 Asymptotic notation
  - 가장 빠르게 증가하는 항만을 고려하는 표기법

케이스 | 표기법
--- | ---
최상의 경우 | 오메가 표기법 (Big-Ω Notation)
평균의 경우 | 세타 표기법(Big-θ Notation)
최악의 경우 | 빅오 표기법(Big-O Notation)

- 알고리즘을 평가할 때는 보통 최악의 경우를 우선적으로 고려

## Big-O 표기법
- 불필요한 연산을 제거하여 알고리즘 분석을 쉽게 하기 위함
- 실행시간은 하드웨어, 프로그래밍 언어에 따라 달라질 수 있으므로 실행 횟수를 고려

빅오 표기법 | 명칭 | 설명 
--- | --- | ---
O(1) | 상수 시간 | 오직 한 단계의 처리
O(logN) | 로그 시간 | 문제 해결 단계들이 연산마다 특정 요인에 의해 감소 
O(N) | 선형 시간 | 문제 해결 단계의 수와 입력값 n이 1:1 관계
O(NlogN) | 로그 선형 시간
O(N^2) | 이차 시간 | 문제 해결 단계의 수는 입력값 N의 제곱
O(N^3) | 삼차 시간
O(2^n) | 지수 시간 | 문제 해결 단계의 수는 주어진 상수값의 n제곱

![https://dzone.com/articles/what-is-big-o-notation](.%5B20210416%5D_complexity_images/18afa40e.png)

복잡도 | 1 | 10 | 100
--- | --- | --- | ---
O(1) | 1 | 1 | 1
O(logN) | 0 | 2 | 5
O(N) | 1 | 10 | 100
O(NlogN) | 0 | 20 | 461
O(N^2) | 1 | 100 | 10000
O(2^N) | 1 | 1024 | 1267650600228229401496703205376
O(N!) | 1 | 3628800 | 화면에 표현할 수 없음!

### Data Structure Operations
![Data Structure Operations](.%5B20210416%5D_complexity_images/01c49f93.png)

### Sorting Algorithms chart
![Sorting Algorithms chart](.%5B20210416%5D_complexity_images/1c730c85.png)
- https://medium.com/@george.seif94/a-tour-of-the-top-5-sorting-algorithms-with-python-code-43ea9aa02889

##### * References
- 책 ⌜이것이 코딩 테스트다⌟ - 나동빈 지음
- [알고리즘의 시간 복잡도와 Big-O 쉽게 이해하기 - Chulgil.Lee](https://blog.chulgil.me/algorithm/#:~:text=%EC%BB%B4%ED%93%A8%ED%84%B0%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EC%97%90%EC%84%9C%EB%8F%84%20%EC%8B%9C%EA%B0%84%EB%B3%B5%EC%9E%A1%EB%8F%84,%EB%A5%BC%20%EC%8B%9C%EA%B0%84%EB%B3%B5%EC%9E%A1%EB%8F%84%EB%A1%9C%20%EB%82%98%ED%83%80%EB%82%B8%EB%8B%A4.)
