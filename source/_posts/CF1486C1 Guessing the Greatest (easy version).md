---
title: CF1486C1 Guessing the Greatest (easy version)
date: 2023-05-12 19:56:07
tags: [CF, 题解, OI, 暴力]
categories:
  - 编程
  - CF
---
# Guessing the Greatest (easy version)

## 题面翻译

这是一道交互题。

有一个**数字各不相同**长度为$n(2\leq n\leq 10^5$的数组 `a`，在一个查询中，您可以询问子段$a[l...r]$中**次大值（第二大的值）**的位置。您需要在不超过 `40` 个查询中查找数组中最大元素的位置。

您可以通过输出$"? \;l\; r"(1\leq l \leq r\leq n)$询问,结果是从 `l` 到`r`中次大值的位置。数组事先已生成，无法在交互时更改。

您可以通过输出$"!\; p"$，在那里是数组中最大元素的坐标。

您可以进行不超过 `40`个查询。输出答案不算作查询。

请注意，样例仅用来表示交互的规则，不保证有逻辑性。

感谢@[听取MLE声一片](https://www.luogu.com.cn/user/253738)  提供翻译

## 题目描述

The only difference between the easy and the hard version is the limit to the number of queries.

This is an interactive problem.

There is an array$a$of$n$different numbers. In one query you can ask the position of the second maximum element in a subsegment$a[l..r]$. Find the position of the maximum element in the array in no more than 40 queries.

A subsegment$a[l..r]$is all the elements$a_l, a_{l + 1}, ..., a_r$. After asking this subsegment you will be given the position of the second maximum from this subsegment in the whole array.

## 输入格式

The first line contains a single integer$n$$(2 \leq n \leq 10^5)$— the number of elements in the array.

## 输出格式

You can ask queries by printing "?$l$$r$"$(1 \leq l < r \leq n)$. The answer is the index of the second maximum of all elements$a_l, a_{l + 1}, \ldots, a_r$. Array$a$is fixed beforehand and can't be changed in time of interaction.

You can output the answer by printing "!$p$", where $p$ is the index of the maximum element in the array.

You can ask no more than 40 queries. Printing the answer doesn't count as a query.

After printing a query do not forget to output end of line and flush the output. Otherwise, you will get Idleness limit exceeded. To do this, use:

- fflush(stdout) or cout.flush() in C++;
- System.out.flush() in Java;
- flush(output) in Pascal;
- stdout.flush() in Python;
- see documentation for other languages

Hacks

To make a hack, use the following test format.

In the first line output a single integer$n$$(2 \leq n \leq 10^5)$. In the second line output a permutation of$n$integers$1$to$n$. The position of$n$in the permutation is the position of the maximum

## 样例 #1

### 样例输入 #1

```
5

3

4
```

### 样例输出 #1

```
? 1 5

? 4 5

! 1
```

## 提示

In the sample suppose$a$is$[5, 1, 4, 2, 3]$. So after asking the$[1..5]$subsegment$4$is second to max value, and it's position is$3$. After asking the$[4..5]$subsegment$2$is second to max value and it's position in the whole array is$4$.

Note that there are other arrays$a$that would produce the same interaction, and the answer for them might be different. Example output is given in purpose of understanding the interaction.
```cpp
#include <bits/stdc++.h>
using namespace std;
int n, a[100001];
int query(int l, int r) {
	cout << "? " << l << " " << r << endl;
	cout.flush();
	int idx;
	cin >> idx;
	return idx;
}
void answer(int x) {
	cout << "! " << x << endl;
	cout.flush();
}
int main() {
	cin >> n;
	int l = 1, r = n;
	while (r - l > 1) {
		int mid = (l + r) / 2;
		int v = query(l, r);
		if (v <= mid) {
			if (l == mid) {
				l = mid + 1;
				continue;
			}
			if (query(l, mid) != v) {
				l = mid + 1;
			} else {
				r = mid;
			}
		} else {
			if (mid + 1 == r) {
				r = mid;
				continue;
			}
			if (query(mid + 1, r) != v) {
				r = mid;
			} else {
				l = mid + 1;
			}
		}
	}
	if (l == r) {
		answer(l);
		return 0;
	}
	if (query(l, r) == r)
		answer(l);
	else
		answer(r);
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
