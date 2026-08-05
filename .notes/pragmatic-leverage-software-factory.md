# Pragmatic Leverage in the Software Factory

## 元信息

- 作者：dex (@dexhorthy) — building humanlayer_dev, YC alum, aitinkerers SF lead, 前 replicatedhq / SproutSocial / NASA
- 发布：2026-07-29
- 原文：https://x.com/dexhorthy/status/2082510831858893115
- 形态：X 推文长文（非博客），Software Factories Fail 系列的附录 / 支线
- 参考位置：Why Software Factories Fail part 2: Turning the lights back on 里被简要引用
- 数据：133.1K views, 165 replies, 667 retweets, 1.6K likes

## 核心观点

### 1. AI 加速的真实位置：不在写代码

早在 AI 出现之前，交付一个 feature 的时间构成：
- 写代码本身：**25-50%**
- 对齐 / 规划、code review / 返工、测试 / 验证：**剩下的 50-75%**

如果你只用 AI 写代码，等于把 2-4 小时压到 10-20 分钟——只加速了一小段，整体几乎没变快。让 AI 参与**规划和对齐**，才能接近 2-3x 的真实提速。

### 2. 80/20 杠杆图：三档投入的返工概率

假设一个连续频谱：
- **两句话 prompt 甩进工厂**：返工概率 ~50%
- **principal engineer 花一下午手写详尽 spec**：返工概率 ~10%（仍可能有"某处"重大返工）
- **每一行都自己写**：返工概率 0%（因为没什么留给 agent 出错）

**前期投入的精力和 expected pain（预期痛点）之间是反向关系。**

### 3. expected pain 的定义

```
expected pain = P(你需要改动) × 改动有多痛
```

概率和成本是两个独立变量，但为了讨论方便糅进一个数字。例子：模型 50% 概率把按钮样式写错，但修起来一句便宜 prompt 就够——综合 expected pain 就很低。

### 4. 反面：过度规划

**你最不想做的事**：花 6 小时规划一个前 10 分钟就能消掉 80% 预期痛点的任务。

这就是 leverage 的含义——**要务实**。

### 5. 什么时候该停下、下钻一层

不能过度纠结那些"不下钻一层就答不了"的开放问题。例子：在 Product 层做了一些工作但没答完所有开放问题——可能就该停在这层，缩到技术细节那一层看什么可行。**没有完美流程。**

### 6. 多阶段规划的操作方式

从 50kft（5 万英尺鸟瞰）一路缩到 10kft（1 万英尺近景），**每一阶段都做一点点方向修正**（steering），确保尽可能多地消掉预期痛点。不是一次性把所有细节都规划完，而是每层都 steer 一下再往下走。

## 关联阅读

- 系列正篇：Why Software Factories Fail part 2: Turning the lights back on
- 主题相邻：[[control-the-ideas-not-the-code]]（antirez 讲"掌控想法而非代码"，规划优先于代码）、[[understanding-is-the-new-bottleneck]]（Litt 讲理解是瓶颈、认知债）
