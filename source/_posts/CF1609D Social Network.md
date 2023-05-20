---
title: CF1609D Social Network
date: 2023-05-09 20:53:52
tags: [CF,题解,图,OI]
categories:
  - 编程
  - CF
---
# Social Network

## 题面翻译

给定$n$个点，$d$条规定，每条规定有两个参数$x_i,y_i$，表示$x_i$和$y_i$必须连通。

$\forall i\in[1,d]$，求在满足$[1,i]$的规定的前提下恰好连$i$条边的无向图中度数最大的点的度数最大可能是多少。

$2\le n\le 10^3,1\le d\le n-1,1\le x_i,y_i\le n,x_i\not=y_i$。

## 题目描述

![](https://cdn.luogu.com.cn/upload/vjudge_pic/CF1609D/bd782248ee184d971343d4489aa3f05723b81f9f.png)William arrived at a conference dedicated to cryptocurrencies. Networking, meeting new people, and using friends' connections are essential to stay up to date with the latest news from the world of cryptocurrencies.

The conference has$n$participants, who are initially unfamiliar with each other. William can introduce any two people,$a$and$b$, who were not familiar before, to each other.

William has$d$conditions,$i$'th of which requires person$x_i$to have a connection to person$y_i$. Formally, two people$x$and$y$have a connection if there is such a chain$p_1=x, p_2, p_3, \dots, p_k=y$for which for all$i$from$1$to$k - 1$it's true that two people with numbers$p_i$and$p_{i + 1}$know each other.

For every$i$($1 \le i \le d$) William wants you to calculate the maximal number of acquaintances one person can have, assuming that William satisfied all conditions from$1$and up to and including$i$and performed exactly$i$introductions. The conditions are being checked after William performed$i$introductions. The answer for each$i$must be calculated independently. It means that when you compute an answer for$i$, you should assume that no two people have been introduced to each other yet.

## 输入格式

The first line contains two integers$n$and$d$($2 \le n \le 10^3, 1 \le d \le n - 1$), the number of people, and number of conditions, respectively.

Each of the next$d$lines each contain two integers$x_i$and$y_i$($1 \le x_i, y_i \le n, x_i \neq y_i$), the numbers of people which must have a connection according to condition$i$.

## 输出格式

Output$d$integers.$i$th number must equal the number of acquaintances the person with the maximal possible acquaintances will have, if William performed$i$introductions and satisfied the first$i$conditions.

## 样例 #1

### 样例输入 #1

```
7 6
1 2
3 4
2 4
7 6
6 5
1 7
```

### 样例输出 #1

```
1
1
3
3
3
6
```

## 样例 #2

### 样例输入 #2

```
10 8
1 2
2 3
3 4
1 4
6 7
8 9
8 10
1 4
```

### 样例输出 #2

```
1
2
3
4
5
5
6
8
```

## 提示

The explanation for the first test case:

In this explanation, the circles and the numbers in them denote a person with the corresponding number. The line denotes that William introduced two connected people. The person marked with red has the most acquaintances. These are not the only correct ways to introduce people.
![](https://cdn.luogu.com.cn/upload/vjudge_pic/CF1609D/a4c52dc40d0c621cc37cb8aa412551d28349b4ab.png)
```cpp
#include <bits/stdc++.h>
using namespace std;
const int N = 1e3 + 10;
int n, m, cnt;
int F[N], S[N];
vector <int> ans;
void init() {
	for (int i = 1; i <= n; i++) F[i] = i, S[i] = 1;
}
int find(int x) {
	return F[x] = (F[x] == x ? x : find(F[x]));
}
void merge(int x, int y) {
	int Fx = find(x), Fy = find(y);
	if (Fx == Fy) {
		cnt++;
		return;
	}
	F[Fy] = Fx;
	S[Fx] += S[Fy];
	S[Fy] = 0;
}
int main() {
	ios::sync_with_stdio(false);
	cin.tie(0);
	cout.tie(0);
	cin >> n >> m;
	init();
	while (m--) {
		int x, y, Ans = 0;
		cin >> x >> y;
		merge(x, y);
		ans.clear();
		for (int i = 1; i <= n; i++)
			if (S[i]) {
				ans.push_back(S[i]);
			}
		sort(ans.rbegin(), ans.rend());
		for (int i = 0; i <= cnt; i++) Ans += ans[i];
		cout << --Ans << '\n';
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

