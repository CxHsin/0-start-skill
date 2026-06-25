# 0-start-skill

`0-start` 是一个用于“从 0 建立陌生领域第一印象”的 Codex skill。它不是一上来给你灌课程表，而是先从真实招聘语言和高质量一手资料切入，帮你看懂这个领域在做什么、常见术语是什么、接下来该从哪里开始。

## 它解决什么问题

很多人一头扎进新领域时，最先遇到的不是知识不够，而是不知道该先看什么、该信谁、该怎么判断自己有没有入门。`0-start` 解决的就是这个冷启动问题。

它会先做三件事：

1. 从 JD 风格信号里提炼这个领域的真实工作语言。
2. 推荐少量高质量的一手资料，帮你形成第一印象。
3. 在你卡住的时候继续追问和解释，直到你真的能看懂这个领域的结构，再给学习路径。

## 适合谁

- 想从 0 进入一个新领域的人
- 已经有一点背景，但还不懂这个领域的人
- 想先看懂岗位语言，再决定要不要深入的人

## 它会怎么工作

你只要给一个方向名，比如：

- `我想学 Agent Engineer`
- `我想学 growth`
- `我想了解 quant research`

它会输出四块内容：

1. `JD Signal Snapshot`
2. `Core Term Cards`
3. `First-Party Source Entry Points`
4. `Next Best Step`

之后它会继续做问答式陪跑，直到你具备第一印象，再转向学习路径。

## 它不会做什么

- 不会直接塞给你一整套大而全的课程
- 不会把低质量二手总结当成核心材料
- 不会把短期热点包装成领域本体
- 不会在没必要的时候一直追问你

## 仓库内容

- [SKILL.md](./SKILL.md): skill 的核心行为定义
- [agents/openai.yaml](./agents/openai.yaml): UI 元数据
- [docs/spark/2026-06-25-0-start-skill-design.md](./docs/spark/2026-06-25-0-start-skill-design.md): 设计过程与规格说明

## 维护原则

- 先稳定，再扩展
- 一手资料优先，必要时才降级
- 只有在真的会改变输出时才追问
- 让新人先建立感觉，再谈路线

## 触发示例

```text
Use $0-start to help me understand an unfamiliar field before giving me a learning path.
```

