---
title: CF1609D Social Network
date: 2023-05-10 17:48:18
tags: [CF,题解,dp,暴力,再做一遍,OI]
categories:
  - 编程
  - CF
---
# Color with Occurrences

## 题面翻译

给定一段黑色文本$t$和多个字符串$s_1,s_2...s_n$。

一次操作可以将$t$中任意一个与任意$s$相等的子串涂成红色。两次涂红的字母仍然是红色。$s$没有使用次数限制。求全涂成红色最小次数和方案，任意输出一种解。

一共有$q$组测试数据。

举例：

$t=\texttt{bababa} \ \  s_1=\texttt{ba}$,$s_2=\texttt{aba}$
 
 一步可以得到$t=\color{red}{\texttt{ba}}\color{black}\texttt{baba}$,$t=\texttt{b}\color{red}{\texttt{aba}}\color{black}\texttt{ba}$or$t=\texttt{bab}\color{red}{\texttt{aba}}$中的一个。
 
 全部涂黑所需$3$步如下：
 
 - 涂红$t[2 \dots 4]=s_2=\texttt{aba}$得$t=\texttt{b}\color{red}\texttt{aba}\color{black}\texttt{ba}$;
- 涂红$t[1 \dots 2]=s_1=\texttt{ba}$得$t=\color{red}\texttt{baba}\color{black}\texttt{ba}$;
- 涂红$t[4 \dots 6]=s_2=\texttt{aba}$得$t=\color{red}{\texttt{bababa}}$.

## 题目描述

You are given some text$t$and a set of$n$strings$s_1, s_2, \dots, s_n$.

In one step, you can choose any occurrence of any string$s_i$in the text$t$and color the corresponding characters of the text in red. For example, if$t=\texttt{bababa}$and$s_1=\texttt{ba}$,$s_2=\texttt{aba}$, you can get$t=\color{red}{\texttt{ba}}\texttt{baba}$,$t=\texttt{b}\color{red}{\texttt{aba}}\texttt{ba}$or$t=\texttt{bab}\color{red}{\texttt{aba}}$in one step.

You want to color all the letters of the text$t$in red. When you color a letter in red again, it stays red.

In the example above, three steps are enough:

- Let's color$t[2 \dots 4]=s_2=\texttt{aba}$in red, we get$t=\texttt{b}\color{red}{\texttt{aba}}\texttt{ba}$;
- Let's color$t[1 \dots 2]=s_1=\texttt{ba}$in red, we get$t=\color{red}{\texttt{baba}}\texttt{ba}$;
- Let's color$t[4 \dots 6]=s_2=\texttt{aba}$in red, we get$t=\color{red}{\texttt{bababa}}$.

Each string$s_i$can be applied any number of times (or not at all). Occurrences for coloring can intersect arbitrarily.

Determine the minimum number of steps needed to color all letters$t$in red and how to do it. If it is impossible to color all letters of the text$t$in red, output -1.

## 输入格式

The first line of the input contains an integer$q$($1 \le q \le 100$) —the number of test cases in the test.

The descriptions of the test cases follow.

The first line of each test case contains the text$t$($1 \le |t| \le 100$), consisting only of lowercase Latin letters, where$|t|$is the length of the text$t$.

The second line of each test case contains a single integer$n$($1 \le n \le 10$) — the number of strings in the set.

This is followed by$n$lines, each containing a string$s_i$($1 \le |s_i| \le 10$) consisting only of lowercase Latin letters, where$|s_i|$— the length of string$s_i$.

## 输出格式

For each test case, print the answer on a separate line.

If it is impossible to color all the letters of the text in red, print a single line containing the number -1.

Otherwise, on the first line, print the number$m$— the minimum number of steps it will take to turn all the letters$t$red.

Then in the next$m$lines print pairs of indices:$w_j$and$p_j$($1 \le j \le m$), which denote that the string with index$w_j$was used as a substring to cover the occurrences starting in the text$t$from position$p_j$. The pairs can be output in any order.

If there are several answers, output any of them.

## 样例 #1

### 样例输入 #1

```
6
bababa
2
ba
aba
caba
2
bac
acab
abacabaca
3
aba
bac
aca
baca
3
a
c
b
codeforces
4
def
code
efo
forces
aaaabbbbcccceeee
4
eeee
cccc
aaaa
bbbb
```

### 样例输出 #1

```
3
2 2
1 1
2 4
-1
4
1 1
2 6
3 3
3 7
4
3 1
1 2
2 3
1 4
2
4 5
2 1
4
3 1
4 5
2 9
1 13
```

## 提示

The first test case is explained in the problem statement.

In the second test case, it is impossible to color all the letters of the text in red.
```cpp
//CF1714D Color with Occurrences
#include <bits/stdc++.h>
using namespace std;
int t;
char s[120];
int len;
int n;
char a[12][12];
int ai[12];
int dp[120];
int cov[120];
int pos[120];
bool check(int x, int t) {
	if (ai[t] > x) return false;
	for (int i = x, j = ai[t]; j >= 1; --i, --j) {
		if (s[i] != a[t][j]) return false;
	}
	return true;
}
int main() {
	cin >> t;
	while (t--) {
		cin >> (s + 1);
		len = strlen(s + 1);
		cin >> n;
		for (int i = 1; i <= n; ++i) {
			cin >> (a[i] + 1);
			ai[i] = strlen(a[i] + 1);
		}
		dp[0] = 0;
		for (int i = 1; i <= len; ++i) {
			dp[i] = 1e9;
			cov[i] = pos[i] = 0;
		}
		for (int i = 1; i <= len; ++i) {
			for (int j = 1; j <= n; ++j) {
				if (check(i, j)) {
					for (int k = i - ai[j]; k <= i - 1; ++k) {
						if (dp[k] + 1 < dp[i]) {
							dp[i] = dp[k] + 1;
							cov[i] = j;
							pos[i] = k;
						}
					}
				}
			}
		}
		if (dp[len] >= 1e9)
			cout << "-1\n";
		else {
			cout << dp[len] << '\n';
			for (int i = len; i; i = pos[i]) {
				cout << cov[i] << ' ' << i - ai[cov[i]] + 1 << '\n';
			}
		}
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
