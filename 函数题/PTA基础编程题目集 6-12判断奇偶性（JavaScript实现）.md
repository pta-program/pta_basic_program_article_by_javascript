# PTA基础编程题目集 6-12判断奇偶性（JavaScript实现）

## 题目描述

本题要求实现判断给定整数奇偶性的函数。

### 函数接口定义

```js
function even(n) { /* ... */ }
```

其中`n`是用户传入的整型参数。当`n`为偶数时，函数返回1；`n`为奇数时返回0。注意：0是偶数。

### 裁判测试程序样例

```js
const readline = require('readline'); // 引入 readline 模块
const rl = readline.createInterface({ input: process.stdin, output: process.stdout }); // 创建输入输出接口

function even(n) { /* 你的代码将被嵌在这里 */ }

rl.on('line', (line) => {
    const n = parseInt(line.trim(), 10); // 读取 n
    if (even(n))
        console.log(`${n} is even.`);    // 偶数
    else
        console.log(`${n} is odd.`);     // 奇数
    rl.close(); // 关闭接口
});
```

### 输入样例1

```in
-6
```

### 输出样例1

```out
-6 is even.
```

### 输入样例2

```in
5
```

### 输出样例2

```out
5 is odd.
```

## 解题思路

这道题的核心是**整数取余判奇偶**：偶数 mod 2 = 0，奇数 mod 2 = ±1。关键细节是正确处理 0 与负数。

### 核心问题分析

1. **数学性质**：奇偶性只与绝对值有关，-6 和 6 都是偶数。
2. **JavaScript 负数取余**：(-6)%2 的结果是 0（因为 2×(-3) = -6，余 0）；(-5)%2 = -1。因此对负数若直接取余判断"等于 1"会误判。
3. **零的特殊性**：0 是偶数，直接特判即可。

### 算法原理说明

统一处理为"取绝对值→取余→判断"：
- n == 0 → return 1（偶数）
- n < 0 → n = -n（取正）
- 再判断 n%2：结果 1 → 奇数返回 0；否则 → 偶数返回 1

或者也可以直接判断 n%2 == 0，避免绝对值步骤（因为负数 % 2 == 0 也是偶数）。

### 具体计算步骤

1. 若 n == 0：return 1
2. 若 n < 0：n = -n
3. temp = n % 2
4. temp == 1 → return 0（奇）；否则 return 1（偶）

## 完整代码

```javascript
// 题目：6-12 判断奇偶性
// 题目描述：
//   实现函数 even(n)，n 为偶数返回 1，奇数返回 0，0 视为偶数。
// 实现原理：
//   取绝对值后取余判断。n==0 直接判偶；n<0 取正；temp=n%2，temp==1 返回 0 否则 1。
// 参数说明：
//   n — 整数
// 时间复杂度：O(1) — 常数次运算
// 空间复杂度：O(1) — 仅使用常数个辅助变量

const readline = require('readline'); // 引入 readline 模块
const rl = readline.createInterface({ input: process.stdin, output: process.stdout }); // 创建输入输出接口

// 函数：even
// 功能：判断奇偶性
// 参数：
//   n — 整数
// 返回值：1 偶数，0 奇数
function even(n) {
    let temp;
    if (n === 0) return 1; // 0 是偶数
    if (n < 0) n = -n;     // 负数取正，奇偶性不变
    temp = n % 2;          // 取余判断
    if (temp === 1) return 0; // 奇数
    else return 1; // 偶数
}

rl.on('line', (line) => {
    const n = parseInt(line.trim(), 10); // 读取 n
    if (even(n))
        console.log(`${n} is even.`);    // 偶数
    else
        console.log(`${n} is odd.`);     // 奇数
    rl.close(); // 关闭接口
});
```


## 代码流程说明

### 1. 主函数
- 用 readline 读入 n（parseInt 解析）
- even(n) 返回真：输出 "... is even."（console.log）
- even(n) 返回假：输出 "... is odd."

### 2. even 函数：分支一 n === 0
- return 1（零是偶数）

### 3. even 函数：分支二 n < 0
- n = -n 取正，不改变奇偶性

### 4. even 函数：取余判断
- temp = n % 2
- temp === 1 → return 0（奇数）
- 否则 → return 1（偶数）

## 代码流程图

```mermaid
flowchart TD
  A["开始\neven(n)"] --> B{"n == 0 ?"}
  B -- "是" --> C["return 1（偶数）"]
  B -- "否" --> D{"n < 0 ?"}
  D -- "是" --> E["n = -n"]
  D -- "否" --> F["temp = n % 2"]
  E --> F
  F --> G{"temp == 1 ?"}
  G -- "是" --> H["return 0（奇数）"]
  G -- "否" --> I["return 1（偶数）"]
  C --> J["结束"]
  H --> J
  I --> J
```

## 解题流程图

```mermaid
flowchart TD
  A["开始"] --> B["读入整数 n"]
  B --> C{"n == 0 ?"}
  C -- "是" --> D["偶数"]
  C -- "否" --> E{"n < 0 ?"}
  E -- "是" --> F["取绝对值"]
  E -- "否" --> G["n % 2 == 0 ?"]
  F --> G
  G -- "是" --> H["偶数"]
  G -- "否" --> I["奇数"]
  D --> J["输出结果"]
  H --> J
  I --> J
  J --> K["结束"]
```
