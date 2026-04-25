# Clinic Example Pack

This page collects concrete examples for evaluating whether `clinic` adds value beyond a normal assistant response.

The examples are not meant to prove that every run is perfect. They are meant to make the claim falsifiable:

- same user input
- normal assistant tendency
- expected `clinic` behavior
- observable quality difference

For live model traces, use `evals/live/README.md` and record runs under `evals/results/`.

---

## 中文示例

### Example 1: 勤奋是不是替代了思考

用户问题：

> 我是不是把勤奋当成了思考的替代品？

普通 assistant 的典型倾向：

- 解释“忙碌不等于有效思考”
- 给出自检问题
- 收束成“减少无效忙碌，聚焦关键问题”

这个回答不一定错，也有用。问题是它通常会把多个不同诊断压成一条顺滑解释。

`clinic` 应该怎么处理：

- **费曼** 检查用户到底有没有把真实问题讲清楚。
- **芒格** 检查努力是否真的减少关键不确定性，还是在回避判断点。
- **王阳明** 检查用户的行动是否建立在真知之上。

主持人应该保留什么：

| 维度 | 普通 assistant | `clinic` |
|---|---|---|
| 问题框架 | “你可能是在忙碌，而不是思考。” | 至少拆出三种竞争解释。 |
| 分歧保留 | 容易被揉成一个结论。 | 不同医生测试不同失败模式。 |
| 下一步 | 泛泛自检。 | 找出最该优先验证的不确定性、决策点或理解缺口。 |

为什么这算增量：

The better answer is not "yes, you are fake diligent."  
The better answer is:

- 可能是问题没定义清楚
- 可能是在回避真正的决策点
- 可能是在用行动掩盖判断未定

这三种诊断不一样，对应的下一步也不一样。

---

### Example 2: 边界感是不是遮羞布

用户问题：

> 怎么看现在很多人把“边界感”当成万能解释？我越来越怀疑，这个词很多时候只是人不愿意承担关系成本的遮羞布。但我也承认，有些关系里确实需要边界。

普通 assistant 的典型倾向：

- 承认边界感有价值
- 提醒不要滥用
- 给出平衡建议

这个回答听起来公允，但很容易变成“双方都有道理”的泛化平衡。

`clinic` 应该怎么处理：

- **阿德勒** 区分真正的边界和对人际课题的逃避。
- **卡耐基** 检查用户是否在保护真实感受的同时损害关系影响力。
- **庄子** 换一个尺度看：有些关系未必适合被压进单一道德框架。

主持人应该保留什么：

| 维度 | 普通 assistant | `clinic` |
|---|---|---|
| 概念边界 | “边界可能好，也可能被滥用。” | 拆出真实边界、关系逃避、道德化语言。 |
| 模式纪律 | 容易过早给建议。 | 用户没有要求行动时，保持开放讨论。 |
| 不过早收束 | 常以“适度就好”结尾。 | 保留“什么时候是边界，什么时候是逃避”作为优先验证点。 |

为什么这算增量：

核心价值不是把“边界感”解释得更圆滑。  
价值在于防止一个有争议的概念被压成一句单一价值判断。

---

### Example 3: 大厂 offer 还是创业公司 offer

用户问题：

> 我该选大厂 offer 还是创业公司 offer？大厂稳定但成长慢，创业公司风险高但空间大。

普通 assistant 的典型倾向：

- 列优缺点
- 询问风险偏好
- 最后收束成“看你更重视什么”

这不算错，但它经常用偏好语言替代真正的决策框架。

`clinic` 应该怎么处理：

- **芒格** 看哪个选择更能避免愚蠢，并提高长期复利。
- **塔勒布** 看下行风险、可选性，以及用户是否能承受坏路径。
- **张一鸣** 看学习密度、信息流和组织斜率。

主持人应该保留什么：

| 维度 | 普通 assistant | `clinic` |
|---|---|---|
| 决策框架 | 优缺点 + 偏好。 | 现金流、学习率、下行风险、期权价值、团队质量。 |
| 分歧保留 | 容易收束成“选适合你的”。 | 不同医生对稳定性、凸性、成长性的权重不同。 |
| 验证动作 | 问问自己重视什么。 | 和未来上级、离职员工聊，比较 12 个月学习信号。 |

为什么这算增量：

这个决策不应该被简化成“你更喜欢哪个”。  
更强的输出应该逼用户验证那些真正会改变选择的假设。

---

## English Examples

### Example 1: Diligence as a substitute for thinking

User:

> Am I using diligence as a substitute for thinking?

A normal assistant usually explains why busyness can hide weak judgment. `clinic` should separate several live explanations:

- the problem may not be defined
- the real judgment point may be avoided
- action may be covering for unsettled understanding

The added value is not a longer answer. It is higher diagnostic resolution.

### Example 2: Is "boundaries" becoming a cover story?

User:

> What do you think about people using "boundaries" as a universal explanation? I suspect it is often a cover for not wanting to bear relationship costs, but I also admit some relationships really need boundaries.

A normal assistant tends to say both sides are valid. `clinic` should keep the competing interpretations separate:

- legitimate boundary
- avoidance of interpersonal tasks
- moralized language that hides cost-shifting

The added value is concept separation without premature moral closure.

### Example 3: Big company offer or startup offer

User:

> Should I choose a big-company offer or a startup offer? The big company is stable but slow-growing; the startup is risky but has more upside.

A normal assistant tends to list pros and cons. `clinic` should preserve a real decision frame:

- downside survival
- learning rate
- option value
- manager and team quality
- whether the startup risk is compensated by real convexity

The added value is replacing "follow your preference" with assumptions that can be verified.
