---
title: CF1539D PriceFixed
date: 2023-05-11 17:42:26
tags: [贪心, CF, 题解, OI]
categories:
  - 编程
  - CF
---
# PriceFixed

## 题面翻译

市场上有$n$种商品，每种商品的价格都是$2$。现在你需要买第$i$种商品至少$a_i$件。但是对于第$i$种商品有一个属性$b_i$，意味着如果你已经买了$b_i$件商品（不一定是这一种商品），那么此商品打折，价格会降到$1$。

你需要最小化你的代价。

其中$1\le n \le 1\times 10^5,1\le a_i,b_i\le 1\times 10^{14}$。

## 题目描述

Lena is the most economical girl in Moscow. So, when her dad asks her to buy some food for a trip to the country, she goes to the best store — "PriceFixed". Here are some rules of that store:

- The store has an infinite number of items of every product.
- All products have the same price:$2$rubles per item.
- For every product$i$there is a discount for experienced buyers: if you buy$b_i$items of products (of any type, not necessarily type$i$), then for all future purchases of the$i$-th product there is a$50\%$discount (so you can buy an item of the$i$-th product for$1$ruble!).

Lena needs to buy$n$products: she must purchase at least$a_i$items of the$i$-th product. Help Lena to calculate the minimum amount of money she needs to spend if she optimally chooses the order of purchasing. Note that if she wants, she can buy more items of some product than needed.

## 输入格式

The first line contains a single integer$n$($1 \leq n \leq 100\,000$) — the number of products.

Each of next$n$lines contains a product description. Each description consists of two integers$a_i$and$b_i$($1 \leq a_i \leq 10^{14}$,$1 \leq b_i \leq 10^{14}$) — the required number of the$i$-th product and how many products you need to buy to get the discount on the$i$-th product.

The sum of all$a_i$does not exceed$10^{14}$.

## 输出格式

Output the minimum sum that Lena needs to make all purchases.

## 样例 #1

### 样例输入 #1

```
3
3 4
1 3
1 5
```

### 样例输出 #1

```
8
```

## 样例 #2

### 样例输入 #2

```
5
2 7
2 8
1 2
2 4
1 8
```

### 样例输出 #2

```
12
```

## 提示

In the first example, Lena can purchase the products in the following way:

1. one item of product$3$for$2$rubles,
2. one item of product$1$for$2$rubles,
3. one item of product$1$for$2$rubles,
4. one item of product$2$for$1$ruble (she can use the discount because$3$items are already purchased),
5. one item of product$1$for$1$ruble (she can use the discount because$4$items are already purchased).

In total, she spends$8$rubles. It can be proved that it is impossible to spend less.

In the second example Lena can purchase the products in the following way:

1. one item of product$1$for$2$rubles,
2. two items of product$2$for$2$rubles for each,
3. one item of product$5$for$2$rubles,
4. one item of product$3$for$1$ruble,
5. two items of product$4$for$1$ruble for each,
6. one item of product$1$for$1$ruble.

In total, she spends$12$rubles.
```cpp
#include <bits/stdc++.h>
#define int long long
using namespace std;
const int N = 1e5 + 10;
int n, l, r, ans, cnt;
struct Node{
	int a, b; // a 最少的数量, b降价的边界
}Arr[N];
bool cmp(Node x, Node y) {return x.b < y.b;}
signed main() {
	cin >> n;
	for(int i = 1; i <= n; i++) cin >> Arr[i].a >> Arr[i].b;
	sort(Arr + 1, Arr + n + 1, cmp);
	l = 1, r = n;
	while (l <= r){
		if(Arr[l].b <= cnt) ans += Arr[l].a, cnt += Arr[l].a, l++;
		else {
			if(Arr[r].a > Arr[l].b - cnt) { // 买一点就够了;不能=,因为刚刚好,这一个也买完了，要r--
				ans += (Arr[l].b - cnt) * 2;
				Arr[r].a -= (Arr[l].b - cnt);
				cnt = Arr[l].b;
			} else { // 全买了.
				ans += Arr[r].a * 2;
				cnt += Arr[r].a;
				r--;
			}
		}
	}
	cout << ans << '\n';
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