---
title: CF1045I Palindrome Pairs
date: 2023-05-16 20:44:49
tags: [CF, 题解, OI, 数学,暴力, 位运算, 数据结构, map]
categories:
  - 编程
  - CF
---
# Palindrome Pairs

## 题面翻译

我们希望找到满足以下性质的字符串对$(i,j)$：$s_{i}+s_{j}$的其中一个排列是回文的（如，"aab"和"abcac"的和"aababcac"可以排列为"aabccbaa"，因此这两个串符合要求）。

输入$N$个小写字符串，输出满足要求的对数。**我们认为$(i,j)$和$(j,i)$是同一对。**

## 题目描述

After learning a lot about space exploration, a little girl named Ana wants to change the subject.

Ana is a girl who loves palindromes (string that can be read the same backwards as forward). She has learned how to check for a given string whether it's a palindrome or not, but soon she grew tired of this problem, so she came up with a more interesting one and she needs your help to solve it:

You are given an array of strings which consist of only small letters of the alphabet. Your task is to find how many palindrome pairs are there in the array. A palindrome pair is a pair of strings such that the following condition holds: at least one permutation of the concatenation of the two strings is a palindrome. In other words, if you have two strings, let's say "aab" and "abcac", and you concatenate them into "aababcac", we have to check if there exists a permutation of this new string such that it is a palindrome (in this case there exists the permutation "aabccbaa").

Two pairs are considered different if the strings are located on different indices. The pair of strings with indices$(i,j)$is considered the same as the pair$(j,i)$.

## 输入格式

The first line contains a positive integer$N$($1 \le N \le 100\,000$), representing the length of the input array.

Eacg of the next$N$lines contains a string (consisting of lowercase English letters from 'a' to 'z') — an element of the input array.

The total number of characters in the input array will be less than$1\,000\,000$.

## 输出格式

Output one number, representing how many palindrome pairs there are in the array.

## 样例 #1

### 样例输入 #1

```
3
aa
bb
cd
```

### 样例输出 #1

```
1
```

## 样例 #2

### 样例输入 #2

```
6
aab
abcac
dffe
ed
aa
aade
```

### 样例输出 #2

```
6
```

## 提示

The first example:

1. aa$+$bb$\to$abba.

The second example:

1. aab$+$abcac$=$aababcac$\to$aabccbaa
2. aab$+$aa$=$aabaa
3. abcac$+$aa$=$abcacaa$\to$aacbcaa
4. dffe$+$ed$=$dffeed$\to$fdeedf
5. dffe$+$aade$=$dffeaade$\to$adfaafde
6. ed$+$aade$=$edaade$\to$aeddea
```cpp
#include <bits/stdc++.h>
#define int long long
using namespace std;
const int N = 100001;
int n, Bit[N], ans, t;
bool parity[26];															// 只要管奇偶性
string s;
map<int, int> Cnt;															// 存储这种状态的个数。
signed main() {
	cin >> n;
	for (int i = 1; i <= n; i++) {
		memset(parity, 0, sizeof parity);
		cin >> s;
		for (char j : s) parity[j - 'a'] = !parity[j - 'a'];
		for (int j = 0; j < 26; j++) Bit[i] = 2 * Bit[i] + parity[j];
		Cnt[Bit[i]]++;
	}
	for (int i = 1; i <= n; i++) {
		ans--; 																// 自己不能和自己
		ans += Cnt[Bit[i]]; 												// 全部偶数，全部一样
		for (int j = 0; j < 26; j++) { 										// 选一个奇数
			ans += Cnt[Bit[i] ^ (1 << j)]; 									// 一个奇数，其他偶数
		}
	}
	cout << (ans >> 1)<< '\n';
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

