---
categories: [Algorithm]
use_math: true
---

## 1. 에라토스테네스의 체 란?
- 소수를 판별하는 알고리즘
- 특정 범위가 주어졌을 때 그 범위 내의 모든 소수를 찾아야 하는 경우 효율적

### 1.1 원리
1. 체에 존재하는 수들을 순차적으로 살펴봄
2. 아직 제거되지 않은 수를 소수로 선택하고, 그 배수들을 모두 제거
3. $\sqrt{n}$ 보다 작은 수의 배수를 제거할 때 까지 1과 2를 반복
4. 체에 남아있는 수들을 모두 소수로 선택

<p><img src="https://upload.wikimedia.org/wikipedia/commons/b/b9/Sieve_of_Eratosthenes_animation.gif"></p>

> 출처 : https://ko.wikipedia.org/wiki/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98_%EC%B2%B4

### 1.2 $\sqrt{n}$ 보다 작은 수의 배수를 제거할 때 까지 반복하는 이유
n보다 작은 어떤 수 m이 $m = ab$ 라면, $a$와 $b$ 중 적어도 하나는 $\sqrt{n}$ 보다 작거나 같다. 즉 m이 소수가 아니라면, $a$와 $b$ 중 작은 수의 배수를 제거할 때 m은 이미 제거된 상태일 것이다.

이는 n보다 작은 합성수 m은 $\sqrt{n}$ 보다 작은 수의 배수만 체크해도 전부 지워진다는 의미이므로, $\sqrt{n}$ 이하의 수의 배수만 지우면 된다.


## 2. 에라토스테네스의 체 구현

### 2.1 요약

1. 1은 소수가 아니므로 FALSE, 그 이후의 수들은 모두 TRUE로 초기화
2. 배열을 순차적으로 순회하며 값이 TRUE인 요소들은 소수로 선택, 그 배수에 해당하는 값은 FALSE로 변경
   - 값이 이미 FALSE로 설정된 수에 대해서는 이전에 탐색한 수의 배수이므로 체에서 걸러졌다고 판단하고 넘어감
3. $\sqrt{n}$ 보다 작은 수의 배수까지 반복
4. 2부터 시작하여 남아있는 수를 모두 출력

### 2.2 예제 코드

```
#include <bits/stdc++.h>
using namespace std;

const int n = 100;    // 구하고자 하는 소수의 범위
const int MAX = 101;  // n+1
bool isPrime[MAX];
int res = 0;  // 1~n 까지의 소수의 개수

// 1~n까지의 범위 내의 소수들과 그 개수를 출력
void eratosthenes() {
  isPrime[1] = false;
  // 1. 2이상의 수들을 일단 true로 초기화
  for(int i = 2; i <= n; i++) {
    isPrime[i] = true;
  }

  // 2. 배열을 순차적으로 순회하며 값이 TRUE인 요소들은 소수로 선택, 그 배수에 해당하는 값은 FALSE로 변경
  //    sqrt(n) 이하의 수의 배수만 지우면 됨
  for(int i = 2; i <= sqrt(n); i++) {
    // 값이 이미 FALSE로 설정된 수에 대해서는 이전에 탐색한 수의 배수이므로 지워졌다고 판단하고 넘어감
    if(!isPrime[i]) continue;

    // i의 배수들을 모두 제거
    for(int j = 2*i; j <= n; j += i) {
      isPrime[j] = false;
    }
  }

  // 2부터 시작하여 남아있는 수를 모두 출력
  for(int i = 2; i <= n; i++) {
    if(isPrime[i]) {
      printf("%d ", i);
      res++;
    }
  }

  printf("num of primes(1~n) : %d", res);
}

int main() {
  eratosthenes();

  return 0;
}
```