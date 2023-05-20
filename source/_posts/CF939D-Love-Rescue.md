---
title: CF939D Love Rescue
date: 2023-05-10 17:48:18
tags: [CF,题解,OI,并查集,DSU]
categories:
  - 编程
  - CF
---
# Love Rescue

## 题面翻译

给定两个长度为n的由小写字母组成的字符串  
每次可以花费1的代价，指定两个字母，把其中一个全部变为另一个  
求使两个字符串相同的最小花费  
n <= 100000

## 题目描述

Valya and Tolya are an ideal pair, but they quarrel sometimes. Recently, Valya took offense at her boyfriend because he came to her in t-shirt with lettering that differs from lettering on her pullover. Now she doesn't want to see him and Tolya is seating at his room and crying at her photos all day long.

This story could be very sad but fairy godmother (Tolya's grandmother) decided to help them and restore their relationship. She secretly took Tolya's t-shirt and Valya's pullover and wants to make the letterings on them same. In order to do this, for one unit of mana she can buy a spell that can change some letters on the clothes. Your task is calculate the minimum amount of mana that Tolya's grandmother should spend to rescue love of Tolya and Valya.

More formally, letterings on Tolya's t-shirt and Valya's pullover are two strings with same length$n$consisting only of lowercase English letters. Using one unit of mana, grandmother can buy a spell of form$(c_{1},c_{2})$(where$c_{1}$and$c_{2}$are some lowercase English letters), which can arbitrary number of times transform a single letter$c_{1}$to$c_{2}$and vise-versa on both Tolya's t-shirt and Valya's pullover. You should find the minimum amount of mana that grandmother should spend to buy a set of spells that can make the letterings equal. In addition you should output the required set of spells.

## 输入格式

The first line contains a single integer$n$($1<=n<=10^{5}$) — the length of the letterings.

The second line contains a string with length$n$, consisting of lowercase English letters — the lettering on Valya's pullover.

The third line contains the lettering on Tolya's t-shirt in the same format.

## 输出格式

In the first line output a single integer — the minimum amount of mana$t$required for rescuing love of Valya and Tolya.

In the next$t$lines output pairs of space-separated lowercase English letters — spells that Tolya's grandmother should buy. Spells and letters in spells can be printed in any order.

If there are many optimal answers, output any.

## 样例 #1

### 样例输入 #1

```
3
abb
dad
```

### 样例输出 #1

```
2
a d
b a
```

## 样例 #2

### 样例输入 #2

```
8
drpepper
cocacola
```

### 样例输出 #2

```
7
l e
e d
d c
c p
p o
o r
r a
```

## 提示

In first example it's enough to buy two spells: ('a','d') and ('b','a'). Then first letters will coincide when we will replace letter 'a' with 'd'. Second letters will coincide when we will replace 'b' with 'a'. Third letters will coincide when we will at first replace 'b' with 'a' and then 'a' with 'd'.
```cpp
#include <bits/stdc++.h>
#define pow qpow
#define int long long
const int N = 30;
using namespace std;
int qpow(int x, int p) {
	if (p == 0)
		return 1;
	int t = qpow(x, p / 2);
	if (p & 1)
		return t * t * x;
	return t * t;
}
int n;
string s, t;
vector <pair<char, char>> Ans;
struct DSU {
	int Fa[N]; // 祖先
	int Si[N]; // 大小
	bool Bi[N]; // 祖先是否为自己
	void init() { // 初始化
		for (int i(1); i <= 26; ++i) Fa[i] = i;
		for (int i(1); i <= 26; ++i) Si[i] = 1;
		for (int i(1); i <= 26; ++i) Bi[i] = true;
		return;
	}
	int Find(int x) { // 寻找祖先
		if (Fa[x] == x) return x;
		else return Fa[x] = Find(Fa[x]);
	}
	bool merge(int x, int y) { // 把y归到x
		int Fx = Find(x), Fy = Find(y);
		if (Fx == Fy) return false; // 合并失败
		Fa[Fy] = Fx, Si[Fx] += Si[Fy], Si[Fy] = 0, Bi[Fy] = 0;
		return true; // 合并成功
	}
} dsu;
signed main() {
	dsu.init();
	cin >> n;
	cin >> s >> t;
	for (int i = 0; i < n; i++) {
		if (dsu.merge(s[i] - 'a' + 1, t[i] - 'a' + 1))
			Ans.push_back(make_pair(s[i], t[i]));
	}
	cout << Ans.size() << '\n';
	for (pair<char, char> i : Ans) {
		cout << i.first << ' ' << i.second << '\n';
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
