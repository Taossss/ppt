---
theme: default
title: 迭代法
info: |
  算法设计与分析 第 4 章 基本的算法策略 4.1 迭代算法
colorSchema: light
aspectRatio: 16/9
canvasWidth: 980
transition: slide-left
fonts:
  sans: Inter
  mono: JetBrains Mono
  provider: google
exportFilename: iterative-algorithms
download: true
---

<div class="kicker">算法设计与分析 · 第 4 章</div>

# <div class="cover-title">基本的算法策略</div>

<div class="cover-subtitle">先看全章地图，再进入 4.1 迭代算法</div>

<div class="chapter-map-cover">
  <div class="chapter-list-card">
    <div class="label">第 4 章内容</div>
    <div class="chapter-list-item active"><b>4.1</b><span>迭代算法</span></div>
    <div class="chapter-list-item"><b>4.2</b><span>蛮力法</span></div>
    <div class="chapter-list-item"><b>4.3</b><span>分而治之算法</span></div>
    <div class="chapter-list-item"><b>4.4</b><span>贪婪算法</span></div>
    <div class="chapter-list-item"><b>4.5</b><span>动态规划</span></div>
    <div class="chapter-list-item"><b>4.6</b><span>算法策略间的比较</span></div>
  </div>

  <div class="chapter-focus-card cover-ideas-card">
    <div>
      <div class="label">本节重点</div>
      <h2>迭代算法</h2>
      <p class="cover-idea-lead">用旧值算新值，通过有限或条件控制的重复过程逼近答案。</p>
      <div class="cover-idea-list">
        <div>
          <b>基本思想</b>
          <span>用旧值算新值，一般用于数值计算</span>
        </div>
        <div>
          <b>常见策略</b>
          <span>累加、累乘、状态反复更新</span>
        </div>
        <div>
          <b>基本步骤</b>
          <span>确定模型 → 建立关系式 → 控制迭代过程</span>
        </div>
        <div class="cover-stop-note">
          <span>结束条件：固定次数结束 / 特定条件结束</span>
        </div>
      </div>
    </div>
  </div>
</div>

---

<div class="kicker">内容提要</div>

# 本章结构

<div class="chapter-tree mt-9">
  <div class="agenda-item chapter-root">
    <div class="agenda-no">4.1</div>
    <div>
      <h2>迭代算法</h2>
      <p>基本思想、常见策略与迭代过程控制</p>
    </div>
  </div>

  <div class="chapter-branches" aria-hidden="true">
    <span></span><span></span><span></span>
  </div>

  <div class="chapter-subgrid">
    <div class="agenda-item chapter-child">
      <div class="agenda-no">4.1.1</div>
      <div>
        <h2>递推法</h2>
        <p>由已知状态正向推出后续状态</p>
        <span>兔子繁殖、最大公约数、循环不变式</span>
      </div>
    </div>
    <div class="agenda-item chapter-child">
      <div class="agenda-no">4.1.2</div>
      <div>
        <h2>倒推法</h2>
        <p>从目标状态反向还原初始条件</p>
        <span>猴子吃桃、杨辉三角、穿越沙漠问题</span>
      </div>
    </div>
    <div class="agenda-item chapter-child">
      <div class="agenda-no">4.1.3</div>
      <div>
        <h2>迭代法解方程</h2>
        <p>不断修正近似值直到满足精度</p>
        <span>方程组迭代、牛顿迭代法、二分法</span>
      </div>
    </div>
  </div>
</div>

---

<div class="kicker">4.1 迭代算法</div>

# 什么是迭代算法

<div class="grid-2 mt-8">
  <div class="panel strong">
    <div class="label">基本思想</div>
    <p class="text-xl leading-8">用旧值计算新值，常见于数值计算与状态推进。</p>
    <div class="formula">new_value = F(old_value)</div>
  </div>
  <div class="panel">
    <div class="label">常见策略</div>
    <ul class="note-list text-lg">
      <li>累加：sum = sum + item</li>
      <li>累乘：product = product × factor</li>
      <li>状态更新：x(n) = φ(x(n-1))</li>
    </ul>
  </div>
</div>

<div class="flow">
  <div class="node">确定模型</div><div class="arrow">→</div>
  <div class="node">建立关系式</div><div class="arrow">→</div>
  <div class="node">控制结束</div>
</div>

<div class="grid-2 mt-5">
  <div class="panel"><b>固定次数结束</b><br>例如循环 10 次、输出前 n 项。</div>
  <div class="panel"><b>特定条件结束</b><br>例如误差小于阈值、余数为 0。</div>
</div>

---

<div class="kicker">4.1.1 递推法 · 例 1</div>

# 兔子繁殖问题

<div class="grid-2 mt-8">
  <div>
    <div class="panel strong">
      <div class="label">问题</div>
      <p class="leading-7">一对兔子从出生后第三个月开始，每月生一对小兔子。兔子只生不死，一月份抱来一对刚出生的小兔子，问一年中每个月各有多少只兔子。</p>
    </div>
    <div class="formula mt-5">y1 = y2 = 1<br>yn = y(n-1) + y(n-2), n = 3,4,...</div>
  </div>
  <div>
    <div class="timeline">
      <div class="month"><b>1 月</b>1</div>
      <div class="month"><b>2 月</b>1</div>
      <div class="month"><b>3 月</b>1+1=2</div>
      <div class="month"><b>4 月</b>2+1=3</div>
      <div class="month"><b>5 月</b>3+2=5</div>
    </div>
    <div class="panel mt-5">
      <div class="label">数据结构选择</div>
      <ul class="note-list">
        <li>数组：存储所有 y(n)</li>
        <li>变量：只存储前两项与当前项</li>
      </ul>
    </div>
  </div>
</div>

---

<div class="kicker">4.1.1 递推法 · 算法 1</div>

# 兔子数列：一次循环推进一步

<div class="grid-2 mt-8">
  <div class="panel">
    <div class="label">变量含义</div>
    <table class="compare">
      <tbody>
        <tr><th>a</th><td>前 2 个月的数量</td></tr>
        <tr><th>b</th><td>前 1 个月的数量</td></tr>
        <tr><th>c</th><td>当前月份的数量</td></tr>
      </tbody>
    </table>
    <div class="formula mt-5">循环不变式：c = a + b</div>
  </div>
  <CodeBlock id="fib1" />
</div>

---

<div class="kicker">4.1.1 递推法 · 算法 2</div>

# 兔子数列：一次循环推进三步

<div class="grid-2 mt-8">
  <CodeBlock id="fib2" />
  <div>
    <div class="panel strong">
      <div class="label">递推迭代表达式</div>
      <div class="formula">c = a + b<br>a = b + c<br>b = a + c</div>
      <p class="leading-7">一次循环内部完成三次状态更新，因此循环次数更少，但变量语义要随步骤变化。</p>
    </div>
    <div class="flow">
      <div class="node">a,b</div><div class="arrow">→</div>
      <div class="node">c</div><div class="arrow">→</div>
      <div class="node">a</div><div class="arrow">→</div>
      <div class="node">b</div>
    </div>
  </div>
</div>

---

<div class="kicker">4.1.1 递推法 · 算法 3</div>

# 兔子数列：双变量交替推进

<div class="grid-2 mt-8">
  <div>
    <div class="panel strong">
      <div class="label">递推迭代表达式</div>
      <div class="formula">a = a + b<br>b = a + b</div>
      <p class="leading-7">每轮循环输出一组新的 a、b。相比算法 1，代码更短；相比算法 2，推进节奏更规整。</p>
    </div>
    <table class="compare mt-5">
      <tbody>
        <tr><th>位置</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th><th>6</th></tr>
        <tr><td>变量</td><td>a</td><td>b</td><td>a=a+b</td><td>b=a+b</td><td>a=a+b</td><td>b=a+b</td></tr>
      </tbody>
    </table>
  </div>
  <CodeBlock id="fib3" />
</div>

---

<div class="kicker">4.1.1 递推法 · 例 2</div>

# 最大公约数：从短除到欧几里得

<div class="grid-2 mt-8">
  <div class="panel">
    <div class="label">算法设计思路</div>
    <ul class="note-list text-lg">
      <li>短除法：直观，但机械步骤多</li>
      <li>辗转相除法：重复利用余数，适合迭代</li>
    </ul>
  </div>
  <div class="panel strong">
    <div class="label">数学关系</div>
    <div class="formula">gcd(m, n) = gcd(n, m % n)</div>
  </div>
</div>

<div class="flow mt-10">
  <div class="node">a</div><div class="arrow">mod</div>
  <div class="node">b</div><div class="arrow">=</div>
  <div class="node">c</div><div class="arrow">→</div>
  <div class="node">a=b, b=c</div>
</div>

---

<div class="kicker">4.1.1 递推法 · gcd 代码</div>

# 欧几里得算法的循环不变式

<div class="grid-2 mt-8">
  <div class="panel strong">
    <div class="label">循环不变式</div>
    <div class="formula">c = a mod b<br>a = b<br>b = c</div>
    <p class="leading-7">当余数 c 为 0 时，当前 b 就是两个整数的最大公约数。</p>
  </div>
  <CodeBlock id="gcd" />
</div>

---

<div class="kicker">4.1.2 倒推法</div>

# 正推与倒推

<div class="grid-2 compare-panels mt-8">
  <div class="panel strong">
    <div class="label">迭代法</div>
    <h2>正推</h2>
    <p class="text-lg leading-8">由前向后解问题，初始状态已知，目标状态未知。</p>
    <div class="flow"><div class="node">起点</div><div class="arrow">→</div><div class="node">过程</div><div class="arrow">→</div><div class="node">终点</div></div>
  </div>
  <div class="panel strong">
    <div class="label">倒推法</div>
    <h2>反向还原</h2>
    <p class="text-lg leading-8">从后往前推解问题，目标状态清楚，初始状态待求。</p>
    <div class="flow"><div class="node">终点</div><div class="arrow">→</div><div class="node">逆过程</div><div class="arrow">→</div><div class="node">起点</div></div>
  </div>
</div>

---

<div class="kicker">4.1.2 倒推法 · 例 1</div>

# 猴子吃桃问题

<div class="grid-2 mt-8">
  <div>
    <div class="panel strong">
      <div class="label">题目</div>
      <p class="leading-7">小猴每天吃现有桃子的一半多一个，到第 10 天只剩 1 个桃子，求原来有多少个桃。</p>
    </div>
    <div class="formula mt-5">a(i) = (1 + a(i+1)) × 2<br>i = 9,8,7,...</div>
    <div class="formula">循环不变式：a = (1 + a) × 2</div>
  </div>
  <CodeBlock id="peach" />
</div>

---

<div class="kicker">4.1.2 倒推法 · 例 2</div>

# 杨辉三角：为什么要倒推

<div class="grid-2 mt-8">
  <div class="pascal-backtrack">
    <div class="label">倒推生成第 5 行</div>
    <div class="pascal-pyramid" aria-label="杨辉三角倒推生成过程">
      <div class="p-row"><span>1</span></div>
      <div class="p-row"><span>1</span><span>1</span></div>
      <div class="p-row"><span>1</span><span>2</span><span>1</span></div>
      <div class="p-row base-row"><span>1</span><span>3</span><span>3</span><span>1</span></div>
      <div class="p-row build-row">
        <span>1</span><span class="cell-j2">4</span><span class="cell-j3">6</span><span class="cell-j4">4</span><span>1</span>
      </div>
    </div>
    <div class="array-update">
      <div class="array-label">A[j] = A[j-1] + A[j]，j 从右往左</div>
      <div class="array-cells">
        <span>A1=1</span><span class="arr-j2">A2=4</span><span class="arr-j3">A3=6</span><span class="arr-j4">A4=4</span><span>A5=1</span>
      </div>
      <div class="update-steps">
        <span class="step-j4">j=4</span>
        <span class="step-j3">j=3</span>
        <span class="step-j2">j=2</span>
      </div>
    </div>
  </div>
  <div>
    <div class="panel strong">
      <div class="label">算法设计思路</div>
      <ul class="note-list">
        <li>一维数组 A[1..i] 存储第 i 行</li>
        <li>若正推更新，会覆盖上一行还未使用的值</li>
        <li>反向更新可以保留所需的旧值</li>
      </ul>
    </div>
    <table class="compare mt-5">
      <tbody>
        <tr><th>二维关系</th><td>a[i][j] = a[i-1][j-1] + a[i-1][j]</td></tr>
        <tr><th>反推关系</th><td>A[j] = A[j-1] + A[j], j = i-1,...,2</td></tr>
      </tbody>
    </table>
  </div>
</div>

---

<div class="kicker">4.1.2 倒推法 · 杨辉三角代码</div>

# 一维数组完成输出

<div class="grid-2 mt-8">
  <CodeBlock id="pascal" />
  <div>
    <div class="panel pascal-run-card">
      <div class="label">正推会出错</div>
      <div class="array-label">j=2 → 3 → 4，旧值被提前覆盖</div>
      <div class="pascal-output-triangle wrong-output">
        <div><span>1</span></div>
        <div><span>1</span><span>1</span></div>
        <div><span>1</span><span>2</span><span>1</span></div>
        <div><span>1</span><span>3</span><span>4</span><span>1</span></div>
        <div class="triangle-last-row"><span>1</span><span class="bad-1">4</span><span class="bad-2">8</span><span class="bad-3">9</span><span>1</span></div>
      </div>
    </div>
    <div class="panel mt-3 pascal-run-card">
      <div class="label">倒推得到正确结果</div>
      <div class="array-label">j=4 → 3 → 2，先用右侧旧值再覆盖</div>
      <div class="pascal-output-triangle right-output">
        <div><span>1</span></div>
        <div><span>1</span><span>1</span></div>
        <div><span>1</span><span>2</span><span>1</span></div>
        <div><span>1</span><span>3</span><span>3</span><span>1</span></div>
        <div class="triangle-last-row"><span>1</span><span class="good-3">4</span><span class="good-2">6</span><span class="good-1">4</span><span>1</span></div>
      </div>
    </div>
  </div>
</div>

---

<div class="kicker">4.1.2 倒推法 · 例 3</div>

# 穿越沙漠问题：模型

<div class="grid-2 mt-8">
  <div class="panel strong">
    <div class="label">问题设定</div>
    <p class="leading-7">吉普车穿越 1000 公里沙漠。总装油量 500 加仑，耗油率 1 加仑/公里。沙漠中没有油库，需要先建立临时油库，并以最少耗油量穿越。</p>
  </div>
  <div class="panel">
    <div class="label">变量定义</div>
    <ul class="note-list">
      <li>k：从 a 加满油向 b 出发的次数</li>
      <li>2k-1：a-b 之间被行驶的次数</li>
      <li>x：每一段 a-b 的距离</li>
      <li>S1、S2：每段 a、b 两点储油量</li>
    </ul>
  </div>
</div>

<div class="desert-model-bottom">
  <div class="desert-model-card">
    <div class="formula desert-formula">S1 = 500k<br>S2 = S1 - (2k - 1)x<br>S2 = 500k - (2k - 1)x</div>
  </div>
  <div class="desert">
    <svg class="desert-paths route-build" viewBox="0 0 760 150" role="img" aria-label="按代码从终点向起点倒推生成的非等长路线">
      <defs>
        <marker id="trip-arrow-red" markerWidth="7" markerHeight="7" refX="6" refY="3.5" orient="auto">
          <path d="M0,0 L7,3.5 L0,7" fill="#c94f45"></path>
        </marker>
        <marker id="trip-arrow-teal" markerWidth="7" markerHeight="7" refX="6" refY="3.5" orient="auto">
          <path d="M0,0 L7,3.5 L0,7" fill="#137f78"></path>
        </marker>
      </defs>
      <line class="route-base" x1="92" y1="74" x2="668" y2="74"></line>
      <line class="route-segment seg-1" x1="668" y1="74" x2="380" y2="74" marker-end="url(#trip-arrow-teal)" pathLength="1"></line>
      <line class="route-segment seg-2" x1="380" y1="74" x2="284" y2="74" marker-end="url(#trip-arrow-red)" pathLength="1"></line>
      <line class="route-segment seg-3" x1="284" y1="74" x2="226" y2="74" marker-end="url(#trip-arrow-red)" pathLength="1"></line>
      <line class="route-segment seg-4" x1="226" y1="74" x2="185" y2="74" marker-end="url(#trip-arrow-red)" pathLength="1"></line>
      <circle class="route-point endpoint" cx="668" cy="74" r="6"></circle>
      <circle class="route-point p1" cx="380" cy="74" r="6"></circle>
      <circle class="route-point p2" cx="284" cy="74" r="6"></circle>
      <circle class="route-point p3" cx="226" cy="74" r="6"></circle>
      <circle class="route-point p4" cx="185" cy="74" r="6"></circle>
      <text class="route-symbol route-node-label endpoint-label" x="668" y="112">终点 b</text>
      <text class="route-symbol route-stock-label endpoint-label" x="668" y="138">S2=0</text>
      <text class="route-symbol seg-label-1" x="524" y="48">x=500</text>
      <text class="route-symbol route-joint-label seg-label-1" x="380" y="112">a/S1</text>
      <text class="route-symbol seg-label-2" x="332" y="42">x=500/3</text>
      <text class="route-symbol route-joint-label seg-label-2" x="284" y="112">a/S1</text>
      <text class="route-symbol seg-label-3" x="254" y="58">x=500/5</text>
      <text class="route-symbol route-joint-label seg-label-3" x="226" y="112">a/S1</text>
      <text class="route-symbol seg-label-4" x="196" y="34">x=500/7</text>
      <text class="route-symbol route-joint-label seg-label-4" x="185" y="112">...</text>
      <text class="route-symbol route-code-note endpoint-label" x="376" y="28">倒推：dis += 500/(2k-1)</text>
    </svg>
  </div>
</div>

---

<div class="kicker">4.1.2 倒推法 · 沙漠问题</div>

# 从终点倒推油库位置

<div class="desert-stage-grid mt-8">
  <div class="panel strong">
    <div class="label">第一段</div>
    <p>倒数第 1 个点 → 终点</p>
    <div class="formula">k=1, S2=0<br>x=500, S1=500</div>
  </div>
  <div class="panel strong">
    <div class="label">第二段</div>
    <p>倒数第 2 个点 → 第 1 个点</p>
    <div class="formula">k=2, S1=1000<br>x=500/3</div>
  </div>
  <div class="panel strong">
    <div class="label">第三段</div>
    <p>倒数第 3 个点 → 第 2 个点</p>
    <div class="formula">k=3, S1=1500<br>x=500/5</div>
  </div>
  <div class="panel strong">
    <div class="label">后续段</div>
    <p>倒数第 4、5、6 …… 个点</p>
    <div class="formula">k=4,5,6,...<br>x=500/(2k-1)</div>
  </div>
</div>

<div class="panel route-demo-panel mt-6">
  <svg class="desert-paths route-build route-build-wide" viewBox="0 0 1060 170" role="img" aria-label="从终点向起点倒推油库位置，分段长度依次为 500、500/3、500/5">
    <defs>
      <marker id="slide15-arrow-coral" markerWidth="7" markerHeight="7" refX="6" refY="3.5" orient="auto">
        <path d="M0,0 L7,3.5 L0,7" fill="#c94f45"></path>
      </marker>
      <marker id="slide15-arrow-teal" markerWidth="7" markerHeight="7" refX="6" refY="3.5" orient="auto">
        <path d="M0,0 L7,3.5 L0,7" fill="#137f78"></path>
      </marker>
    </defs>
    <line class="route-base" x1="118" y1="82" x2="942" y2="82"></line>
    <line class="route-segment seg-1" x1="942" y1="82" x2="530" y2="82" marker-end="url(#slide15-arrow-teal)" pathLength="1"></line>
    <line class="route-segment seg-2" x1="530" y1="82" x2="393" y2="82" marker-end="url(#slide15-arrow-coral)" pathLength="1"></line>
    <line class="route-segment seg-3" x1="393" y1="82" x2="310" y2="82" marker-end="url(#slide15-arrow-coral)" pathLength="1"></line>
    <line class="route-segment seg-4" x1="310" y1="82" x2="251" y2="82" marker-end="url(#slide15-arrow-coral)" pathLength="1"></line>
    <circle class="route-point endpoint" cx="942" cy="82" r="6"></circle>
    <circle class="route-point p1" cx="530" cy="82" r="6"></circle>
    <circle class="route-point p2" cx="393" cy="82" r="6"></circle>
    <circle class="route-point p3" cx="310" cy="82" r="6"></circle>
    <circle class="route-point p4" cx="251" cy="82" r="6"></circle>
    <text class="route-symbol route-code-note endpoint-label" x="530" y="32">倒推：dis = 500 → 500 + 500/3 → 500 + 500/3 + 500/5 → ...</text>
    <text class="route-symbol seg-label-1" x="736" y="58">x=500</text>
    <text class="route-symbol route-joint-label seg-label-1" x="530" y="120">倒数第 1 个储油点</text>
    <text class="route-symbol seg-label-2" x="462" y="48">x=500/3</text>
    <text class="route-symbol route-joint-label seg-label-2" x="393" y="120">倒数第 2 个</text>
    <text class="route-symbol seg-label-3" x="352" y="62">x=500/5</text>
    <text class="route-symbol route-joint-label seg-label-3" x="310" y="120">倒数第 3 个</text>
    <text class="route-symbol seg-label-4" x="281" y="40">x=500/7</text>
    <text class="route-symbol route-joint-label seg-label-4" x="251" y="120">...</text>
    <text class="route-symbol route-node-label endpoint-label" x="942" y="120">终点</text>
  </svg>
</div>

---

<div class="kicker">4.1.2 倒推法 · 沙漠问题代码</div>

# 用距离与油量控制倒推过程

<div class="grid-2 mt-8">
  <CodeBlock id="desert" />
  <div class="panel strong">
    <div class="label">控制思想</div>
    <ul class="note-list text-lg">
      <li>dis 表示已经从终点向前覆盖的距离</li>
      <li>k 决定当前段需要来回的次数</li>
      <li>油量公式随 k 的增长而更新</li>
      <li>当 dis ≥ 1000 时，完成从终点到起点的倒推</li>
    </ul>
  </div>
</div>

---

<div class="kicker">4.1.3 迭代法解方程</div>

<h1>解方程：逐步逼近</h1>

<div class="grid-2 mt-8">
  <div class="panel strong">
    <div class="label">基本思想</div>
    <p class="text-xl leading-8">选择初值，构造迭代关系，不断得到更接近真实解的近似值。</p>
  </div>
  <div class="panel">
    <div class="label">基本步骤</div>
    <div class="grid grid-cols-1 gap-2">
      <div>1. 确定初值 x0</div>
      <div>2. 建立迭代关系：f(x)=0 → x=phi(x)</div>
      <div>3. 构造数列：x(n)=phi(x(n-1))</div>
      <div>4. 直到满足停止条件</div>
    </div>
  </div>
</div>

<div class="flow mt-8">
  <div class="node">x0</div><div class="arrow">→</div>
  <div class="node">x1</div><div class="arrow">→</div>
  <div class="node">x2</div><div class="arrow">→</div>
  <div class="node">...</div><div class="arrow">→</div>
  <div class="node">精度满足</div>
</div>

---

<div class="kicker">4.1.3 迭代法解方程 · 例 1</div>

# 方程组根：整体向量迭代

<div class="grid-2 mt-8">
  <div class="panel strong">
    <div class="label">算法说明</div>
    <p class="leading-7">方程组解的初值为 X=(x0,x1,...,xn-1)，迭代关系方程组为：</p>
    <div class="formula">xi = gi(X), i=0,1,...,n-1</div>
    <p class="leading-7">w 为解的精度，maxn 为最大迭代次数。</p>
  </div>
  <CodeBlock id="system"></CodeBlock>
</div>

---

<div class="kicker">4.1.3 迭代法解方程 · 例 2</div>

<h1>牛顿迭代法：切线逼近根</h1>

<div class="newton-statement">牛顿迭代法解求形如 <b>ax<sup>3</sup>+bx<sup>2</sup>+cx+d=0</b> 方程的根</div>

<div class="newton-rebuild">
  <div class="newton-formula-box">
    <div class="newton-formula dark">f(x)=0</div>
    <div class="newton-formula blue"><span>f(x0)+▽f(x0)(x-x0)≈0</span></div>
    <div class="newton-formula dark"><span>x=x0 --f(x0)/▽f(x0)</span></div>
  </div>
  <div class="newton-modern-figure">
    <div class="newton-modern-callout">y=f(x0)+▽f(x0)(x-x0)</div>
    <svg class="newton-modern-graph" viewBox="0 0 420 300" role="img" aria-label="牛顿迭代法函数曲线与两次切线逼近">
      <line class="modern-axis" x1="72" y1="228" x2="372" y2="228" pathLength="1"></line>
      <polyline class="modern-axis-arrow" points="348,214 372,228 348,242"></polyline>
      <line class="modern-axis" x1="72" y1="228" x2="72" y2="44" pathLength="1"></line>
      <polyline class="modern-axis-arrow" points="58,70 72,44 86,70"></polyline>
      <path class="modern-curve" d="M58 122 C76 214 98 272 138 272 C176 272 202 205 226 150 C252 90 271 50 286 24" pathLength="1"></path>
      <line class="modern-guide" x1="286" y1="24" x2="286" y2="228" pathLength="1"></line>
      <line class="modern-guide" x1="226" y1="150" x2="226" y2="228" pathLength="1"></line>
      <line class="modern-red-tangent" x1="204" y1="228" x2="226" y2="150" pathLength="1"></line>
      <line class="modern-green-tangent" x1="226" y1="228" x2="290" y2="24" pathLength="1"></line>
      <text class="modern-x-label" x="194" y="256">x2</text>
      <text class="modern-x-label" x="220" y="256">x1</text>
      <text class="modern-x-label" x="276" y="256">x0</text>
    </svg>
  </div>
</div>

---

<div class="kicker">4.1.3 迭代法解方程 · 牛顿法代码</div>

# 三次方程求根

<div class="grid-2 mt-8">
  <CodeBlock id="newton" />
  <div class="panel strong">
    <div class="label">示例</div>
    <div class="formula">x³ + 2x² + 3x + 4 = 0</div>
    <p class="leading-7">停止条件使用相邻两次近似根的差值：fabs(x1 - x0) &lt; 1e-4。</p>
  </div>
</div>

---

<div class="kicker">4.1.3 迭代法解方程 · 二分法</div>

# 二分法求方程根

<div class="grid-2 mt-8">
  <div class="panel strong">
    <div class="label">求解目标</div>
    <p class="leading-7">二分法求解方程 x³/2 + 2x² - 8 = 0 在区间 [0,1] 上的近似根。</p>
    <div class="formula">前提：f(x) 连续，且 f(a) × f(b) &lt; 0</div>
  </div>
  <div class="panel">
    <div class="label">算法设计</div>
    <ol class="note-list">
      <li>[a0,b0]=[a,b]，c0=(a0+b0)/2</li>
      <li>若 f(c0)=0，则 c0 为根</li>
      <li>若 f(a0)×f(c0)&lt;0，则新区间为 [a0,c0]</li>
      <li>若 f(b0)×f(c0)&lt;0，则新区间为 [c0,b0]</li>
    </ol>
  </div>
</div>

<div class="flow mt-8">
  <div class="node">a0</div><div class="arrow">——</div>
  <div class="node accent-coral">c0</div><div class="arrow">——</div>
  <div class="node">b0</div><div class="arrow">→</div>
  <div class="node">新区间</div>
</div>

---

<div class="kicker">4.1.3 迭代法解方程 · 二分法代码</div>

# 用区间缩小控制精度

<div class="grid-2 mt-8">
  <CodeBlock id="bisection" />
  <div class="panel strong">
    <div class="label">示例补充</div>
    <div class="formula">3x³ + 4x² + 2x + 8 = 0</div>
    <p class="leading-7">二分法不依赖导数，只依赖区间两端函数值异号；每次迭代把候选区间缩小一半。</p>
  </div>
</div>

---
layout: center
class: text-center
---

<div class="kicker">4.1 小结</div>

# 三种迭代思维

<table class="compare mt-8 text-left">
  <tbody>
    <tr><th>方法</th><th>适合问题</th><th>关键控制</th></tr>
    <tr><td><b class="accent-teal">递推法</b></td><td>兔子数列、最大公约数</td><td>用前序状态推出当前状态</td></tr>
    <tr><td><b class="accent-amber">倒推法</b></td><td>猴子吃桃、杨辉三角、沙漠油库</td><td>从结果反向还原初始条件</td></tr>
    <tr><td><b class="accent-coral">迭代解方程</b></td><td>方程组、牛顿法、二分法</td><td>通过精度阈值或最大次数停止</td></tr>
  </tbody>
</table>

<div class="footer-tag">迭代的核心：模型、关系式、停止条件</div>
