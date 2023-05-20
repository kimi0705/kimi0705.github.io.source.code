---
title: CF992C Nastya and a Wardrobe
date: 2023-05-18 21:29:18
tags: [CF, 题解, 数学,快速幂]
categories:
  - 编程
  - CF
---
# Nastya and a Wardrobe

## 题面翻译

## 题目描述

$Nastya$ 收到了一个神奇的“双倍衣柜”，在每个月底，衣柜中的裙子数量都会双倍。

在第 $1$ 年里，衣柜中有 $x$ 条裙子。前 $k$ 个月中，在双倍之后，$Nastya$ 都有 $50\%$ 的几率从衣柜中取出一条裙子（当然首先要保证衣柜内有裙子）。身为程序员，请你帮她求出第 $k + 1$ 个月底，衣柜中的裙子双倍后，裙子数的期望值。这个值可能很大，你只要输出它对 $10^9+7$ 取模的结果即可。

## 输入格式

仅 $1$ 行，有 $2$ 个整数，分别为衣柜中原有的裙子数 $x$，以及给定的 $k$。

（数据范围：$0 \leqslant x,\ k \leqslant 10^{18}$）

##输出格式

仅 $1$ 个整数，表示第 $k + 1$ 个月底衣柜中裙子数的期望值对 $10^9+7$ 取模的结果。

##提示与说明

- 第 $1$ 组样例的解释：

因为 $k = 0$，所以 $Nastya$ 无法取走任何裙子。因此期望值就是 $x$ 双倍的结果，也就是 $4$。

- 第 $2$ 组样例的解释：

第一个月底双倍之后，衣柜中有 $4$ 条裙子，$Nastya$ 有 $50\%$ 的几率取走 $1$ 条，这意味着衣柜中的裙子有 $50\%$ 的几率有 $3$ 条，$50\%$ 的几率有 $4$ 条。第二个月底她不会取裙子，因此此时衣柜中的裙子有 $50\%$ 的几率有 $6$ 条，$50\%$ 的几率有 $8$ 条。综上所述，期望值为 $(6+8)/2 = 7$。

感谢@Sooke 提供翻译

## 题目描述

Nastya received a gift on New Year — a magic wardrobe. It is magic because in the end of each month the number of dresses in it doubles (i.e. the number of dresses becomes twice as large as it is in the beginning of the month).

Unfortunately, right after the doubling the wardrobe eats one of the dresses (if any) with the$50%$probability. It happens every month except the last one in the year.

Nastya owns$x$dresses now, so she became interested in the [expected number](https://en.wikipedia.org/wiki/Expected_value) of dresses she will have in one year. Nastya lives in Byteland, so the year lasts for$k+1$months.

Nastya is really busy, so she wants you to solve this problem. You are the programmer, after all. Also, you should find the answer modulo$10^{9}+7$, because it is easy to see that it is always integer.

## 输入格式

The only line contains two integers$x$and$k$($0<=x,k<=10^{18}$), where$x$is the initial number of dresses and$k+1$is the number of months in a year in Byteland.

## 输出格式

In the only line print a single integer — the expected number of dresses Nastya will own one year later modulo$10^{9}+7$.

## 样例 #1

### 样例输入 #1

```
2 0
```

### 样例输出 #1

```
4
```

## 样例 #2

### 样例输入 #2

```
2 1
```

### 样例输出 #2

```
7
```

## 样例 #3

### 样例输入 #3

```
3 2
```

### 样例输出 #3

```
21
```

## 提示

In the first example a year consists on only one month, so the wardrobe does not eat dresses at all.

In the second example after the first month there are$3$dresses with$50%$probability and$4$dresses with$50%$probability. Thus, in the end of the year there are$6$dresses with$50%$probability and$8$dresses with$50%$probability. This way the answer for this test is$(6+8)/2=7$.
```cpp
#include <bits/stdc++.h>
#define int long long
using namespace std;
const int mod = 1e9 + 7;
int x, k;
int fpow(int x, int p) {
	if (p == 0)
		return 1;
	int t = fpow(x, p / 2);
	if (p & 1)
		return (t * t % mod) * x % mod;
	return (t * t) % mod;
}
signed main() {
	ios::sync_with_stdio(false);
	cin.tie(0);
	cout.tie(0);
	cin >> x >> k;
	if (x == 0) {
		cout << "0" << endl;
		return 0;
	}
	cout <<  (fpow(2, k + 1) * (x % mod) % mod - fpow(2, k) + 1 + mod)  % mod;
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
