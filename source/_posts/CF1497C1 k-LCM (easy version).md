---
title: CF1497C1 k-LCM (easy version)
date: 2023-05-09 20:53:52
tags: [CF,题解,构造,OI]
categories:
  - 编程
  - CF
---
# k-LCM (easy version)

## 题面翻译

**本题与 [CF1497C2](https://www.luogu.com.cn/problem/CF1497C2) 的不同之处是在本题中，$k=3$。**

给定一个整数$n$，请找到$k$个和为$n$的正整数$a_1,a_2,\dots,a_k$，使得$\operatorname{lcm}\{a_1,a_2,\dots,a_k\}\leqslant \dfrac n2$。

$t$组数据，$1\leqslant t\leqslant 10^4$，$3\leqslant n\leqslant 10^9$，$k=3$。

Translated by Eason_AC  
2021.3.20

## 题目描述

It is the easy version of the problem. The only difference is that in this version$k=3$.

You are given a positive integer$n$. Find$k$positive integers$a_1, a_2,\ldots, a_k$, such that:

-$a_1 + a_2 + \ldots + a_k = n$
-$LCM(a_1, a_2, \ldots, a_k) \le \frac{n}{2}$

Here$LCM$is the [least common multiple](https://en.wikipedia.org/wiki/Least_common_multiple) of numbers$a_1, a_2, \ldots, a_k$.

We can show that for given constraints the answer always exists.

## 输入格式

The first line contains a single integer$t$$(1 \le t \le 10^4)$— the number of test cases.

The only line of each test case contains two integers$n$,$k$($3 \le n \le 10^9$,$k = 3$).

## 输出格式

For each test case print$k$positive integers$a_1, a_2, \ldots, a_k$, for which all conditions are satisfied.

## 样例 #1

### 样例输入 #1

```
3
3 3
8 3
14 3
```

### 样例输出 #1

```
1 1 1
4 2 2
2 6 6
```
```cpp
#include <bits/stdc++.h>
using namespace std;
int t, n, k;
int main() {
	cin >> t;
	while (t--) {
		cin >> n >> k;
		for (int i = 1; i <= k - 3; i++) cout << 1 << ' ';
		n -= k - 3;
		if (n % 2) cout << 1 << ' ' << n / 2 << ' ' << n / 2 << '\n';
		else if (n % 4) cout << 2 << ' ' << n / 2 - 1 << ' ' << n / 2 - 1 << '\n';
		else cout << n / 2 << ' ' << n / 4  << ' ' << n / 4 << '\n';
	}
	return 0;
}
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
