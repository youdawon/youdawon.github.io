---
layout: post
date: 2024-08-24
title: "[Data Structure] 비트연산자 및 Leetcode 문제"
tags: [Data Structure, Bit Manipulation, ]
categories: [Data Structure, ]
---


### 1. **비트 연산자 개요**


자바에서 비트 연산자는 정수형 숫자의 각 비트를 직접 조작하는 데 사용된다.


#### 1.1 비트 AND (`&`)

- 두 비트가 모두 1일 때 결과가 1이 되는 연산자이다.
- **예시**: `5 & 3`은 `101 & 011 = 001`로 결과는 `1` 이다.

#### 1.2 비트 OR (`|`)

- 두 비트 중 하나라도 1이면 결과가 1이 되는 연산자이다.
- **예시**: `5 | 3`은 `101 | 011 = 111`로 결과는 `7` 이다.

#### 1.3 비트 XOR (`^`)

- 두 비트가 다를 때 결과가 1이 되는 연산자이다.
- **예시**: `5 ^ 3`은 `101 ^ 011 = 110`로 결과는 `6` 이다.
- **특징**: 같은 값을 두 번 XOR하면 원래 값으로 돌아온다. 예를 들어, `x ^ y ^ y = x` 이다.

#### 1.4 비트 NOT (`~`)

- 비트를 반전시키는 연산자이다. 1은 0으로, 0은 1로 바뀐다.
- **예시**: `~5`는 `~101 = 010`으로 결과는 `6` 이다. (`6`은 `11111111111111111111111111111010`로 표현됩니다.)

#### 1.5 왼쪽 시프트 (`<<`)

- 모든 비트를 왼쪽으로 지정된 수만큼 이동시킵니다. 오른쪽 빈자리는 0으로 채워집니다.
- **예시**: `5 << 1`은 `101 << 1 = 1010`으로 결과는 `10`입니다.

#### 1.6 오른쪽 시프트 (`>>`)

- 모든 비트를 오른쪽으로 지정된 수만큼 이동시킵니다. 왼쪽 빈자리는 부호 비트로 채워집니다 (음수의 경우 1, 양수의 경우 0).
- **예시**: `5 >> 1`은 `101 >> 1 = 010`으로 결과는 `2`입니다.

#### 1.7 논리적 오른쪽 시프트 (`>>>`)

- 모든 비트를 오른쪽으로 이동시키며, 왼쪽 빈자리는 항상 0으로 채워집니다.
- **예시**: `5 >>> 1`은 `11111111111111111111111111111011 >>> 1 = 01111111111111111111111111111101`로 결과는 `2147483645`입니다.

#### 2. **비트 연산 응용**


#### 2.1 홀수/짝수 판별

- 숫자 `x`가 홀수인지 확인하려면 `x & 1`이 1이면 홀수, 0이면 짝수입니다.

	
{% raw %}
```java
	boolean isOdd = (x & 1) == 1;
```
{% endraw %}



#### 2.2 비트 마스크

- 특정 비트를 선택하거나 조작할 때 사용됩니다.
- 예를 들어, 숫자 `x`의 n번째 비트를 1로 설정하려면:

	
{% raw %}
```java
	x |= (1 << n);
```
{% endraw %}



#### 2.3 두 수의 교환 (XOR 사용)

- XOR 연산을 사용하여 두 변수의 값을 임시 변수 없이 교환할 수 있습니다.

	
{% raw %}
```java
	x = x ^ y;
	y = x ^ y;
	x = x ^ y;
```
{% endraw %}



#### 2.4 두 수의 동일성 비교

- XOR 연산을 통해 두 수가 동일한지 확인할 수 있습니다. `x ^ y`의 결과가 0이면 두 수는 동일합니다.

	
{% raw %}
```java
	boolean isEqual = (x ^ y) == 0;
```
{% endraw %}



#### 2.5 특정 비트 제거

- `x`에서 n번째 비트를 제거하려면:

	
{% raw %}
```java
	x &= ~(1 << n);
```
{% endraw %}



#### 2.6 2의 거듭제곱 판별

- 숫자 `x`가 2의 거듭제곱인지 확인하려면:

	
{% raw %}
```java
	boolean isPowerOfTwo = (x > 0) && ((x & (x - 1)) == 0);
```
{% endraw %}



#### 2.7 비트 개수 세기 (Hamming Weight)

- 숫자 `x`의 이진 표현에서 1의 개수를 세려면:

	
{% raw %}
```java
	public int hammingWeight(int x) {
	    int count = 0;
	    while (x != 0) {
	        count += x & 1;
	        x >>>= 1;
	    }
	    return count;
	}
```
{% endraw %}



#### 2.8 비트 반전 (비트 NOT)

- 모든 비트를 반전시키는 방법은 `~` 연산자를 사용합니다.

	
{% raw %}
```java
	int inverted = ~x;
```
{% endraw %}



#### 3. **비트 연산 관련 문제**


#### 3.1 [**Number of 1 Bits**](https://leetcode.com/problems/number-of-1-bits/)

- 문제 설명: 주어진 정수의 이진수 표현에서 1의 개수를 세는 문제입니다.
- **풀이**: 반복문을 사용하여 정수를 오른쪽으로 시프트하면서 1의 개수를 센다.

	
{% raw %}
```java
	public int hammingWeight(int n) {
	    int count = 0;
	    while (n != 0) {
	        count += n & 1;
	        n >>>= 1;
	    }
	    return count;
	}
```
{% endraw %}



#### 3.2 [**Counting Bits**](https://leetcode.com/problems/counting-bits/)

- 문제 설명: 0부터 n까지의 모든 정수의 이진수 표현에서 1의 개수를 계산하는 문제입니다.
- **풀이**: 동적 계획법(DP)을 사용하여 각 숫자의 1의 개수를 계산한다.

	
{% raw %}
```java
	public int[] countBits(int n) {
	    int[] dp = new int[n + 1];
	    for (int i = 1; i <= n; i++) {
	        dp[i] = dp[i >> 1] + (i & 1);
	    }
	    return dp;
	}
```
{% endraw %}



#### 3.3 [**Reverse Bits**](https://leetcode.com/problems/reverse-bits/)

- 문제 설명: 주어진 32비트 정수의 비트 순서를 반대로 뒤집는 문제입니다.
- **풀이**: 비트를 하나씩 이동하며 반대 위치에 저장한다.

	
{% raw %}
```java
	public int reverseBits(int n) {
	    int result = 0;
	    for (int i = 0; i < 32; i++) {
	        result <<= 1;
	        result |= (n & 1);
	        n >>>= 1;
	    }
	    return result;
	}
```
{% endraw %}



#### 3.4 [**Missing Number**](https://leetcode.com/problems/missing-number/)

- 문제 설명: 0부터 n까지의 숫자 중 하나가 빠진 배열에서 그 숫자를 찾는 문제입니다.
- **풀이**: XOR 연산을 통해 배열에 없는 숫자를 찾는다.

	
{% raw %}
```java
	public int missingNumber(int[] nums) {
	    int result = nums.length;
	    for (int i = 0; i < nums.length; i++) {
	        result ^= i;
	        result ^= nums[i];
	    }
	    return result;
	}
```
{% endraw %}



#### 3.5 [**Sum of Two Integers**](https://leetcode.com/problems/sum-of-two-integers/)

- 문제 설명: + 연산자를 사용하지 않고 두 정수의 합을 계산하는 문제입니다.
- **풀이**: 비트 연산을 사용하여 합을 계산한다.

	
{% raw %}
```java
	public int getSum(int a, int b) {
	    while (b != 0) {
	        int carry = (a & b) << 1;
	        a = a ^ b;
	        b = carry;
	    }
	    return a;
	}
```
{% endraw %}



#### 4. **실제 코딩 테스트 문제에서의 활용**

- **XOR 연산**: 비트 연산을 이용하여 빠르고 효율적으로 배열의 중복 요소나 누락된 숫자를 찾을 수 있습니다.
- **비트 시프트**: 비트 이동 연산을 활용해 빠르게 곱셈, 나눗셈 연산을 수행하거나 특정 비트를 조작할 수 있습니다.
- **비트 마스크**: 특정 비트만을 선택하거나 변경하는 데 사용됩니다.
