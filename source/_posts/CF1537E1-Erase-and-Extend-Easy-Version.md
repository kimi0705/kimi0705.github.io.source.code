---
title: CF1537E1 - Erase and Extend (Easy Version)
date: 2023-05-11 19:47:55
tags: [字符串,暴力,OI]
categories:
  - 编程
  - CF
---
# Erase and Extend (Easy Version)

## 题面翻译

你有一个字符串$s$，你可以进行两种操作。
- 删去字符串的最后一个字符。
- 将$s$变为$s+s$，$+$表示字符串连接，也就是复制一次字符串。

你可以随意的进行操作，也可以不进行操作。

你需要找到$s$进行操作后获得的所有长度为$k$的字符串中**字典序最小**的字符串。

## 题目描述

This is the easy version of the problem. The only difference is the constraints on$n$and$k$. You can make hacks only if all versions of the problem are solved.

You have a string$s$, and you can do two types of operations on it:

- Delete the last character of the string.
- Duplicate the string:$s:=s+s$, where$+$denotes concatenation.

You can use each operation any number of times (possibly none).

Your task is to find the lexicographically smallest string of length exactly$k$that can be obtained by doing these operations on string$s$.

A string$a$is lexicographically smaller than a string$b$if and only if one of the following holds:

-$a$is a prefix of$b$, but$a\ne b$;
- In the first position where$a$and$b$differ, the string$a$has a letter that appears earlier in the alphabet than the corresponding letter in$b$.

## 输入格式

The first line contains two integers$n$,$k$($1 \leq n, k \leq 5000$) — the length of the original string$s$and the length of the desired string.

The second line contains the string$s$, consisting of$n$lowercase English letters.

## 输出格式

Print the lexicographically smallest string of length$k$that can be obtained by doing the operations on string$s$.

## 样例 #1

### 样例输入 #1

```
8 16
dbcadabc
```

### 样例输出 #1

```
dbcadabcdbcadabc
```

## 样例 #2

### 样例输入 #2

```
4 5
abcd
```

### 样例输出 #2

```
aaaaa
```

## 提示

In the first test, it is optimal to make one duplication: "dbcadabc"$\to$"dbcadabcdbcadabc".

In the second test it is optimal to delete the last$3$characters, then duplicate the string$3$times, then delete the last$3$characters to make the string have length$k$.

"abcd"$\to$"abc"$\to$"ab"$\to$"a"$\to$"aa"$\to$"aaaa"$\to$"aaaaaaaa"$\to$"aaaaaaa"$\to$"aaaaaa"$\to$"aaaaa".
```cpp
#include <bits/stdc++.h>
#pragma GCC optimize(3,"Ofast")
#define int long long
using namespace std;
int n, m;
string s, t, ans;
signed main() {
	ios::sync_with_stdio(false);
	cin.tie(0);cout.tie(0);
	cin >> n >> m >> s;
	for (int i = 0; i < n; i++) {
		t = t + s[i];
		if(t + ans <= ans + t) ans = t;
	}
	for (int i = 0; i < m; i++) cout << ans[i % ans.size()];
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