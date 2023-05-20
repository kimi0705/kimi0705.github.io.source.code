---
title: OJ题目跳转 - Html在线版
date: 2023-05-15 19:56:07
tags: [OnlineJudgeJumper]
---
<!DOCTYPE html>
<main class="main">
  <div id="searchbox">
    <input id="keyword" autofocus placeholder="题目编号 ↵" aria-label="search" type="search" onkeyup="onKeyUp(event)">
    <div id="searchResults"></div>
  </div>
  <script>
    let input = "";
let urls = [];
function onKeyUp(event) {
 var e = event || window.event || arguments.callee.caller.arguments[0];
 load();
 if (e && e.keyCode == 13) {
  window.open(urls[0], '_blank');
 }
}
window.onload = load;
function load() {
 input = document.getElementById("keyword").value;
 input = input.toUpperCase().replaceAll(/\s/g, "");
 urls = [];
 match();
 let d = "";
 for (let i in urls) {
  d += `<li class="post-entry"><header class="entry-header">${urls[i]}&nbsp;\xBB</header><a href="${urls[i]}" aria-label="${urls[i]}"></a></li>`;
 }
 document.getElementById("searchResults").innerHTML = d;
}
function test(site, preffix, extra) {
 if (extra == null) {
  let reg = new RegExp(`^${preffix}\\d*$`);
  if (reg.test(input)) {
addURL(site, input.substring(preffix.length));
  }
 } else if (extra === 'cf-problem') {
  let len = input.length;
  let reg = new RegExp(`^${preffix}\\d+[A-Z]$`);
  if (reg.test(input)) {
addURL(site, input.substring(preffix.length, len - 1), input.substring(len - 1));
return;
  }
  reg = new RegExp(`^${preffix}\\d+[A-Z]\\d$`);
  if (reg.test(input)) {
addURL(site, input.substring(preffix.length, len - 2), input.substring(len - 2));
return;
  }
 }
}
function match() {
 let len = input.length;
 test('luogu', 'P');
 test('zhimaoi','智码')
 test('luogu', 'LUOGU');
 test('hdu', 'HDU');
 test('hdu', 'HDOJ');
 test('poj', 'POJ');
 test('loj', 'LOJ');
 test('uoj', 'UOJ');
 test('bzoj', 'BZOJ');
 test('codeforces-contest', 'CF');
 test('codeforces', 'CF', 'cf-problem');
 let allow_remote_oj = true;
 if (allow_remote_oj) {
  test('luogu-codeforces', 'CF', 'cf-problem');
  test('vjudge-codeforces', 'CF', 'cf-problem');
  test('vjudge-uva', 'UVA');
 }
}
function addURL(site, code, extra) {
 let url = "https://";
 if (site === 'luogu')
  url += `www.luogu.com.cn/problem/P${code}`;
 else if (site === 'hdu')
  url += `acm.hdu.edu.cn/showproblem.php?pid=${code}`;
 else if (site === 'loj')
  url += `loj.ac/p/${code}`;
 else if (site === 'uoj')
  url += `uoj.ac/problem/${code}`;
 else if (site === 'poj')
  url = 'http://' + `poj.org/problem?id=${code}`; //
 else if (site === 'codeforces')
  url += `codeforces.com/problemset/problem/${code}/${extra}`;
 else if (site === 'codeforces-contest')
  url += `codeforces.com/contest/${code}`;
 else if (site === 'codeforces-contest')
  url += `codeforces.com/contest/${code}`;
 else if (site === 'bzoj')
  url += `darkbzoj.tk/problem/${code}`;
 //////// REMOTE OJ /////////
 else if (site === 'luogu-codeforces')
  url += `www.luogu.com.cn/problem/CF${code}${extra}`;
 else if (site === 'vjudge-codeforces')
  url += `vjudge.net/problem/CodeForces-${code}${extra}`;
 else if (site === 'vjudge-lightoj')
  url += `vjudge.net/problem/LightOJ-${code}`;
 else if (site === 'vjudge-uva')
  url += `vjudge.net/problem/UVA-${code}`;
 urls.push(url);
}
  </script>
</main>
<a href="#top" id="gototop" aria-label="go to top" title="Go to Top (Alt + G)">
  </body>
  </html>

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
