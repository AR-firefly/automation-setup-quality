# Automation Setup Quality（自动化设置质量保证）

你写自动化之前，看数据源长什么样了吗？

没看？那你一定翻过车。把 bitable 当文件夹扫、假设 API 返回 `items` 实际是 `data.repositories`、信了预设的 skip 标记结果该处理的被跳了——**这些不是写代码时犯的错，是在写第一行之前就埋下的。**

这套流程就是让你在动手之前，把这些假设全验证一遍。仅需三步即可。

详细使用指南请参阅 [USAGE.md](USAGE.md)，包含三个常见场景的完整演练。

## 设计哲学

- **先验证再动手**：不假设结构。每条数据源先看原始结构长什么样。省成本最好的时机是开始之前，不是跑完发现错了之后。
- **人机协作闭环**：方案必须有人点头。验证必须手动+自动结合。AI 不能给自己做 final sign-off。
- **失败是预期的一部分**：三轮验证不通过就报错，不假装成功。总比交个废的好。

## 工作流

```
Step 0：复用判断
  ├─ 验证过的数据源 → 跳过 Step 1
  ├─ "老样子" → 跳过 Step 1+2
  ├─ "你先动" → 跳过 Step 2
  └─ 首次 / 数据源不同 → 完整三步

Step 1：验证数据源
  → 读原始结构，确认类型对、筛选生效
  → 贴结果确认

Step 2：确认方案
  → 数据来源 + 筛选条件 + 评估标准 + 输出格式
  → 等人点头再写

Step 3：验证交付
  → 逐项验证：数据可读 / 筛选正确 / 逻辑可行 / 格式符合
  → 不过就退 Step 1。3 轮不通就报错
```

## 文件结构

```
automation-setup-quality/
├── README.md                        # 本文件
├── USAGE.md                         # 使用指南（场景 + 演练）
├── SKILL.md                         # 方法论全文
├── LICENSE                          # MIT
├── .gitignore
└── references/
    └── data-source-guide.md         # 数据源验证指南
```

## 适用人群

- **AI Agent 用户**：把 `SKILL.md` 加载成 skill，设置自动化时自动触发
- **自动化配置人员**：当操作手册用，少返工
- **提示词工程师**：参考怎么在 prompt 里嵌验证逻辑
- **任何要设定时任务 / 数据推送 / 自动化工作流的人**

## 致谢

以下项目直接影响了这套流程的设计：

- [guard-skills](https://github.com/amElnagdy/guard-skills) — 让我意识到 skill 本身也要 QA，不只是代码才要测。"验证交付"环节直接抄了它的思路。
- [mission](https://github.com/tackeyy/mission) — 任务拆解的分层设计，Step 0→1→2→3 的结构受它影响——先判断能不能复用，再一层层往下。
- [sequant](https://www.npmjs.com/package/sequant) — 顺序化编排的思路，Step 3 的逐项检查表是受它启发。
- [fable5-mode](https://github.com/cozytab/fable5-mode) — 边界定义方法，Step 2 四要素框架的参考来源。
- [autonomous-coding-toolkit](https://github.com/parthalon025/autonomous-coding-toolkit) — 自主编码场景下的质量控制实践，让我相信动手前先验证这事可以流程化。
- [skill-tools](https://github.com/skill-tools/skill-tools) — Skill 开发工具链的思路，影响了本仓库的结构。
- [agentskills-ci](https://pypi.org/project/agentskills-ci/) — CI 集成方法论——哪些能自动验证，哪些必须人工看。
- [ai-workflow-evals](https://github.com/ollieb89/ai-workflow-evals) — 工作流评估的系统方法，Step 3 验证标准的设计思路来源。

## 许可

MIT License — 随意使用、修改、分享。欢迎大家来提 issue 进行改进！

## 作者

AR-26710
