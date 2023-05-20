---
title: CF1031C Cram Time
date: 2023-05-15 22:07:04
tags: [CF, 题解, OI, 数学,暴力]
categories:
  - 编程
  - CF
---
# Cram Time

## 题面翻译

## 题目描述

现在你有两天的时间备考，两天各有$a$小时,$b$小时。

每天可以看若干份笔记。编号为$k$的笔记需要看$k$小时(请不要忽略，最后输出有用)。为了考得更好，你需要最大化看的笔记份数。请你求出最多能看多少份笔记。

注意，看过的笔记需要都不相同。即使是不在同一天看的。

## 输入格式

一行两个正整数$a$,$b$$(1 \leq a, b \leq 10^9)$。

## 输出格式

一共四行。

第一行一个整数$n$表示第一天看的笔记份数。

第二行$n$个用空格隔开的正整数表示第一天看的笔记的编号。

第三行一个整数$m$表示第二天看的笔记份数。

第四行$m$个用空格隔开的正整数表示第二天看的笔记的编号。

请确保你的方案用时在$a$和$b$之内。

此题有 Special Judge。

## 题目描述

In a galaxy far, far away Lesha the student has just got to know that he has an exam in two days. As always, he hasn't attended any single class during the previous year, so he decided to spend the remaining time wisely.

Lesha knows that today he can study for at most$a$hours, and he will have$b$hours to study tomorrow. Note that it is possible that on his planet there are more hours in a day than on Earth. Lesha knows that the quality of his knowledge will only depend on the number of lecture notes he will read. He has access to an infinite number of notes that are enumerated with positive integers, but he knows that he can read the first note in one hour, the second note in two hours and so on. In other words, Lesha can read the note with number$k$in$k$hours. Lesha can read the notes in arbitrary order, however, he can't start reading a note in the first day and finish its reading in the second day.

Thus, the student has to fully read several lecture notes today, spending at most$a$hours in total, and fully read several lecture notes tomorrow, spending at most$b$hours in total. What is the maximum number of notes Lesha can read in the remaining time? Which notes should he read in the first day, and which — in the second?

## 输入格式

The only line of input contains two integers$a$and$b$($0 \leq a, b \leq 10^{9}$) — the number of hours Lesha has today and the number of hours Lesha has tomorrow.

## 输出格式

In the first line print a single integer$n$($0 \leq n \leq a$) — the number of lecture notes Lesha has to read in the first day. In the second line print$n$distinct integers$p_1, p_2, \ldots, p_n$($1 \leq p_i \leq a$), the sum of all$p_i$should not exceed$a$.

In the third line print a single integer$m$($0 \leq m \leq b$) — the number of lecture notes Lesha has to read in the second day. In the fourth line print$m$distinct integers$q_1, q_2, \ldots, q_m$($1 \leq q_i \leq b$), the sum of all$q_i$should not exceed$b$.

All integers$p_i$and$q_i$should be distinct. The sum$n + m$should be largest possible.

## 样例 #1

### 样例输入 #1

```
3 3
```

### 样例输出 #1

```
1
3 
2
2 1
```

## 样例 #2

### 样例输入 #2

```
9 12
```

### 样例输出 #2

```
2
3 6
4
1 2 4 5
```

## 提示

In the first example Lesha can read the third note in$3$hours in the first day, and the first and the second notes in one and two hours correspondingly in the second day, spending$3$hours as well. Note that Lesha can make it the other way round, reading the first and the second notes in the first day and the third note in the second day.

In the second example Lesha should read the third and the sixth notes in the first day, spending$9$hours in total. In the second day Lesha should read the first, second fourth and fifth notes, spending$12$hours in total.
```cpp
#include <bits/stdc++.h>
#define int long long
using namespace std;
const int N = 1e5 + 10;
int a, b, n, temp, cnt, i;
bool Used[N];
signed main() {
	cin >> a >> b;
	temp = a + b;
	for (i = 1; temp >= i; i++) n++, temp -= i;
	temp = a;
	for (i = n; i >= 1; i--)
		if (temp >= i) cnt++, Used[i] = 1, temp -= i;
		else break;
	if (temp <= i && temp != 0) cnt++, Used[temp] = 1;
	cout << cnt << '\n';
	for (int i = 1; i <= n; i++) if (Used[i]) cout << i << ' ';
	cout << '\n' << n - cnt << '\n';
	for (int i = 1; i <= n; i++) if (!Used[i]) cout << i << ' ';
	return  0;
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
