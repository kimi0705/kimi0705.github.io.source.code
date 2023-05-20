---
title: CF1582D Vupsen, Pupsen and 0
date: 2023-05-11 09:34:08
tags: [CF, 题解, 构造, 贪心,OI]
categories:
  - 编程
  - CF
---
# Vupsen, Pupsen and 0

## 题面翻译

### 题目描述
给一个长度为$n$的序列$a_1,a_2,\dots,a_n$，寻找一个长度为$n$序列$b_1,b_2,\dots,b_n$，满足$\forall i\in\left[1,n\right]b_i\not=0,\ \ \sum\limits_{i=1}^n |b_i|\le10^9,\ \ \sum\limits_{i=1}^n a_i\times b_i=0$，可以证明答案一定存在。
### 输入格式
第一行输入一个正整数$t$表示数据组数。

对于每一组数据，第一行输入一个正整数$n$表示序列长度，第二行$n$个整数表示序列$a$。
### 输出格式
对于每一组数据，输出一行$n$个整数表示序列$b$。如果有多种答案，输出任意一种。
### 数据范围
$1\le t\le100,2\le n\le10^5,2\le\sum n\le2\times10^5,-10^4\le a_i\le10^4,a_i\not=0$。

## 题目描述

Vupsen and Pupsen were gifted an integer array. Since Vupsen doesn't like the number$0$, he threw away all numbers equal to$0$from the array. As a result, he got an array$a$of length$n$.

Pupsen, on the contrary, likes the number$0$and he got upset when he saw the array without zeroes. To cheer Pupsen up, Vupsen decided to come up with another array$b$of length$n$such that$\sum_{i=1}^{n}a_i \cdot b_i=0$. Since Vupsen doesn't like number$0$, the array$b$must not contain numbers equal to$0$. Also, the numbers in that array must not be huge, so the sum of their absolute values cannot exceed$10^9$. Please help Vupsen to find any such array$b$!

## 输入格式

The first line contains a single integer$t$($1 \le t \le 100$) — the number of test cases. The next$2 \cdot t$lines contain the description of test cases. The description of each test case consists of two lines.

The first line of each test case contains a single integer$n$($2 \le n \le 10^5$) — the length of the array.

The second line contains$n$integers$a_1, a_2, \ldots, a_n$($-10^4 \le a_i \le 10^4$,$a_i \neq 0$) — the elements of the array$a$.

It is guaranteed that the sum of$n$over all test cases does not exceed$2 \cdot 10^5$.

## 输出格式

For each test case print$n$integers$b_1, b_2, \ldots, b_n$— elements of the array$b$($|b_1|+|b_2|+\ldots +|b_n| \le 10^9$,$b_i \neq 0$,$\sum_{i=1}^{n}a_i \cdot b_i=0$).

It can be shown that the answer always exists.

## 样例 #1

### 样例输入 #1

```
3
2
5 5
5
5 -2 10 -9 4
7
1 2 3 4 5 6 7
```

### 样例输出 #1

```
1 -1
-1 5 1 -1 -1
-10 2 2 -3 5 -1 -1
```

## 提示

In the first test case,$5 \cdot 1 + 5 \cdot (-1)=5-5=0$. You could also print$3$$-3$, for example, since$5 \cdot 3 + 5 \cdot (-3)=15-15=0$

In the second test case,$5 \cdot (-1) + (-2) \cdot 5 + 10 \cdot 1 + (-9) \cdot (-1) + 4 \cdot (-1)=-5-10+10+9-4=0$.
```cpp
#include <bits/stdc++.h>
using namespace std;
const int N = 1e5 + 10;
int t, n;
int Arr[N];
int main() {
	cin >> t;
	while (t--) {
		cin >> n;
		for (int i = 1; i <= n; i++) cin >> Arr[i];
		if (n % 2 == 0) {
			for (int i = 1; i <= n; i += 2) cout << -Arr[i + 1] << ' ' << Arr[i] << ' ';
			cout << '\n';
		} else {
			for (int i = 1; i <= n - 3; i += 2) cout << -Arr[i + 1] << ' ' << Arr[i] << ' ';
			if (Arr[n - 2] + Arr[n - 1] != 0) cout << -Arr[n] << ' ' << -Arr[n] << ' ' << Arr[n - 2] + Arr[n - 1] << '\n';
			else if (Arr[n - 2] + Arr[n] != 0) cout << -Arr[n - 1] << ' ' << Arr[n - 2] + Arr[n] << ' ' << -Arr[n - 1]  << '\n';
			else if (Arr[n - 1] + Arr[n] != 0) cout <<  Arr[n - 1] + Arr[n] << ' ' << -Arr[n - 2] << ' ' << -Arr[n - 2]  << '\n';
		}
	}
}
/*
  ax + by = -cz
  {
	  a + b != 0   x = y = -c z = a + b
  }
  ax + cz = -by
  {
	  a + c != 0   x = z = -b y = a + c
  }
  by + cz = -ax
  {
	  b + c != 0   y = z = -a x = b + c
  }
 */
```
<script src="https://giscus.app/client.js"
        data-repo="kimi0705/kimi0705.github.io"
        data-repo-id="R_kgDOJfkTvA"
        data-category="Q&A"
        data-category-id="DIC_kwDOJfkTvM4CWmkN"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="bottom"
        data-theme="preferred_color_scheme"
        data-lang="zh-CN"
        data-loading="lazy"
        crossorigin="anonymous"
        async>
</script>