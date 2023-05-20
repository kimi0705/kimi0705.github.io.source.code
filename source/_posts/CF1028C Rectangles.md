---
title: CF1028C Rectangles
date: 2023-05-13 19:56:07
tags: [CF, 题解, OI, 数学]
categories:
  - 编程
  - CF
---
# Rectangles

## 题面翻译

### 题目大意

在平面直角坐标系中给定$n$个矩形，要求找到一个点$(x,y)$，这个点在至少$n-1$个给定矩形的内部或边界

### 输入格式

第一行一个整数$n$，表示矩形个数

下面$n$行每行$4$个整数$x1,y1,x2,y2$，表示矩形的左下和右上坐标

### 输出格式

两个整数$x,y$

## 题目描述

You are given$n$rectangles on a plane with coordinates of their bottom left and upper right points. Some$(n-1)$of the given$n$rectangles have some common point. A point belongs to a rectangle if this point is strictly inside the rectangle or belongs to its boundary.

Find any point with integer coordinates that belongs to at least$(n-1)$given rectangles.

## 输入格式

The first line contains a single integer$n$($2 \le n \le 132\,674$) — the number of given rectangles.

Each the next$n$lines contains four integers$x_1$,$y_1$,$x_2$and$y_2$($-10^9 \le x_1 < x_2 \le 10^9$,$-10^9 \le y_1 < y_2 \le 10^9$) — the coordinates of the bottom left and upper right corners of a rectangle.

## 输出格式

Print two integers$x$and$y$— the coordinates of any point that belongs to at least$(n-1)$given rectangles.

## 样例 #1

### 样例输入 #1

```
3
0 0 1 1
1 1 2 2
3 0 4 1
```

### 样例输出 #1

```
1 1
```

## 样例 #2

### 样例输入 #2

```
3
0 0 1 1
0 1 1 2
1 0 2 1
```

### 样例输出 #2

```
1 1
```

## 样例 #3

### 样例输入 #3

```
4
0 0 5 5
0 0 4 4
1 1 4 4
1 1 4 4
```

### 样例输出 #3

```
1 1
```

## 样例 #4

### 样例输入 #4

```
5
0 0 10 8
1 2 6 7
2 3 5 6
3 4 4 5
8 1 9 2
```

### 样例输出 #4

```
3 4
```

## 提示

The picture below shows the rectangles in the first and second samples. The possible answers are highlighted.

 ![](https://cdn.luogu.com.cn/upload/vjudge_pic/CF1028C/afe32198a5a9eb1ff9e8a20f68bff3bd1db43611.png)The picture below shows the rectangles in the third and fourth samples.

 ![](https://cdn.luogu.com.cn/upload/vjudge_pic/CF1028C/1f383f98b80a1cee6f760c4ae11ccf4d5b79e3ad.png)
```cpp
#include <bits/stdc++.h>
#define int long long
using namespace std;
int a,   b,   c,   d;
int X1 = LLONG_MIN,  X2 = LLONG_MAX,  Y1 = LLONG_MIN,  Y2 = LLONG_MAX;      // 最
int XX1 = LLONG_MIN, XX2 = LLONG_MAX, YY1 = LLONG_MIN, YY2 = LLONG_MAX;     // 次
int Xid1, Xid2, Yid1, Yid2;
int n;
signed main() {
	cin >> n;
	for (int i = 1; i <= n; i++) {
		cin >> a >> b >> c >> d;
		if (X1 <= a) 
			XX1 = X1, X1 = a, Xid1 = i;
		else if (XX1 <= a)
			XX1 = a;
		if (Y1 <= b)
			YY1 = Y1, Y1 = b, Yid1 = i;
		else if (YY1 <= b)
			YY1 = b;
		if (X2 >= c)
			XX2 = X2, X2 = c, Xid2 = i;
		else if (XX2 >= c)
			XX2 = c;
		if (Y2 >= d) 
			YY2 = Y2, Y2 = d, Yid2 = i;
		else if (YY2 >= d)
			YY2 = d;
	}
	for (int i = 1; i <= n; i++) {
		int A, B, C, D;
		A = (i == Xid1) ? XX1 : X1;
		B = (i == Yid1) ? YY1 : Y1;
		C = (i == Xid2) ? XX2 : X2;
		D = (i == Yid2) ? YY2 : Y2;
		if (A <= C && B <= D) {
			printf("%lld %lld", A, B);
			return 0;
		}
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
