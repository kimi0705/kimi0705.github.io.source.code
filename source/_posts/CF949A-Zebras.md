---
title: CF949A Zebras
date: 2023-05-19 22:34:48
tags: [CF, 题解, OI, 构造]
categories:
  - 编程
  - CF
---
# Zebras

## 题面翻译

给你一个01串，要求将它划分成多个子序列，子序列不一定是连续的，子序列要满足以0开头，以0结尾，中间01交替出现。

输入格式：

输入一个只有01的字符串

输出格式：

输出第1行子序列的个数k，后面k行的第1个数n为子序列的长度，第2个数到第n+1个数表示子序列中的数在原串中的位置。
如果没有合法的方案则输出-1。
不需要最大化或者最小化k的值。

感谢@zhaotiensn 提供的翻译

## 题目描述

Oleg writes down the history of the days he lived. For each day he decides if it was good or bad. Oleg calls a non-empty sequence of days a zebra, if it starts with a bad day, ends with a bad day, and good and bad days are alternating in it. Let us denote bad days as 0 and good days as 1. Then, for example, sequences of days 0, 010, 01010 are zebras, while sequences 1, 0110, 0101 are not.

Oleg tells you the story of days he lived in chronological order in form of string consisting of 0 and 1. Now you are interested if it is possible to divide Oleg's life history into several subsequences, each of which is a zebra, and the way it can be done. Each day must belong to exactly one of the subsequences. For each of the subsequences, days forming it must be ordered chronologically. Note that subsequence does not have to be a group of consecutive days.

## 输入格式

In the only line of input data there is a non-empty string$s$consisting of characters 0 and 1, which describes the history of Oleg's life. Its length (denoted as$|s|$) does not exceed$200000$characters.

## 输出格式

If there is a way to divide history into zebra subsequences, in the first line of output you should print an integer$k$($1<=k<=|s|$), the resulting number of subsequences. In the$i$-th of following$k$lines first print the integer$l_{i}$($1<=l_{i}<=|s|$), which is the length of the$i$-th subsequence, and then$l_{i}$indices of days forming the subsequence. Indices must follow in ascending order. Days are numbered starting from 1. Each index from$1$to$n$must belong to exactly one subsequence. If there is no way to divide day history into zebra subsequences, print -1.

Subsequences may be printed in any order. If there are several solutions, you may print any of them. You do not have to minimize nor maximize the value of$k$.

## 样例 #1

### 样例输入 #1

```
0010100
```

### 样例输出 #1

```
3
3 1 3 4
3 2 5 6
1 7
```

## 样例 #2

### 样例输入 #2

```
111
```

### 样例输出 #2

```
-1
```
```cpp
#include<bits/stdc++.h>
using namespace std;
char s[200005];
int len, cnt, k;
vector<int> Ans[200005];
int main() {
	cin >> (s + 1);
	len = strlen(s + 1);
	for (int i = 1; i <= len; i++) {
		if (s[i] == '0')Ans[cnt++].push_back(i);
		else {
			if (cnt == 0) {
				cout << -1 << endl;
				return 0;
			}
			Ans[--cnt].push_back(i);
		}
		k = max(k, cnt);
	}
	if (cnt != k) {
		cout << -1 << endl;
		return 0;
	}
	cout << cnt << endl;
	for (int i = 0; i < cnt; i++) {
		cout << Ans[i].size();
		for (int j = 0; j < Ans[i].size(); j++)
			cout << " " << Ans[i][j];
		cout << endl;
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
