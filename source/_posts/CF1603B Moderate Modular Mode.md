---
title: CF1603B Moderate Modular Mode
date: 2023-05-09 20:53:52
tags: [CF,题解,构造,数学,OI]
categories:
  - 编程
  - CF
---
# Moderate Modular Mode

## 题面翻译

给定两个**偶数**$x,y$

求一个$n \in [1,2\times10^{18}]$满足$n \bmod x = y \bmod n$

一个测试点有多组数据，数据保证有解

## 题目描述

YouKn0wWho has two even integers$x$and$y$. Help him to find an integer$n$such that$1 \le n \le 2 \cdot 10^{18}$and$n \bmod x = y \bmod n$. Here,$a \bmod b$denotes the remainder of$a$after division by$b$. If there are multiple such integers, output any. It can be shown that such an integer always exists under the given constraints.

## 输入格式

The first line contains a single integer$t$($1 \le t \le 10^5$) — the number of test cases.

The first and only line of each test case contains two integers$x$and$y$($2 \le x, y \le 10^9$, both are even).

## 输出格式

For each test case, print a single integer$n$($1 \le n \le 2 \cdot 10^{18}$) that satisfies the condition mentioned in the statement. If there are multiple such integers, output any. It can be shown that such an integer always exists under the given constraints.

## 样例 #1

### 样例输入 #1

```
4
4 8
4 2
420 420
69420 42068
```

### 样例输出 #1

```
4
10
420
9969128
```

## 提示

In the first test case,$4 \bmod 4 = 8 \bmod 4 = 0$.

In the second test case,$10 \bmod 4 = 2 \bmod 10 = 2$.

In the third test case,$420 \bmod 420 = 420 \bmod 420 = 0$.
```cpp
//CF1603B Moderate Modular Mode
#include <bits/stdc++.h>
#define int long long
using namespace std;
int t, a, b;
signed main() {
	cin >> t;
	while(t--) {
		int a, b;
		cin >> a >> b;
		if(a > b) cout << a + b << '\n';
		else cout << b - b % a / 2 << '\n';
	}
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