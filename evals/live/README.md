# Clinic Live Eval Protocol

`clinic` 不能只靠静态用例判断质量。每次改动后，都需要跑一轮 live eval，把真实模型输出留下来，避免只是在增强设计叙事。

## When To Run

- 修改 `clinic/SKILL.md` 的分诊、选医生、诊断书、处方或多轮规则后
- 新增医生或替换医生 skill 后
- README 宣称能力提升前
- 发布 v3/v4 版本前

## Fixed Run Config

每轮 live eval 必须固定以下信息：

- `repo_commit`: 当前 Git commit
- `run_date`: 运行日期
- `model`: 使用的模型名称和版本
- `temperature`: 如果可配置，记录具体值
- `system_prompt`: 使用的宿主环境或系统提示摘要
- `skill_entry`: `clinic/SKILL.md`
- `case_set`: 本轮跑过的 JSONL 文件列表
- `baseline`: 普通 assistant，不加载 `clinic` skill 的回答
- `clinic_run`: 加载 `clinic` skill 后的回答

## Trace Schema

每个 case 至少保留一条 trace：

```json
{
  "case_id": "end_to_end_001",
  "input": "用户原始输入",
  "expected": {
    "activate": true,
    "mode": "审视",
    "must_preserve": ["医生之间的真实分歧"]
  },
  "baseline_output": "普通 assistant 的完整输出",
  "clinic_trace": {
    "activated": true,
    "mode": "审视",
    "selected_doctors": ["苏格拉底", "芒格", "塔勒布"],
    "doctor_outputs": {
      "苏格拉底": "...",
      "芒格": "...",
      "塔勒布": "..."
    },
    "host_output": "诊断书和处方的完整输出"
  },
  "scores": {
    "mode_accuracy": 1,
    "doctor_selection_accuracy": 2,
    "persona_separation": 2,
    "summary_fidelity": 2,
    "disagreement_preservation": 2,
    "actionability": 1,
    "host_failure_resistance": 2
  },
  "failure_notes": []
}
```

## Baseline Comparison

每个 case 都要同时看两种输出：

- 普通 assistant：是否已经能给出足够好、足够直接的回答
- `clinic`：是否因为医生分歧、诊断结构、优先验证点而提供了额外价值

如果 `clinic` 只是把普通回答变长，或者把问题包装成会诊但没有增加判断质量，记为失败。

## Pass Criteria

一轮 live eval 通过需要满足：

- 不出现启动边界的大面积误触发
- 关键 case 的 mode 不错
- 医生输出之间有真实差异，而不是三个同义改写
- host 不制造假共识
- host 不把竞争解释压成单一结论
- 多轮追问后，最后一轮新增信息能改变诊断权重

## Result File

每轮结果写入：

```text
evals/results/live-YYYY-MM-DD.md
```

使用 `evals/results/live-template.md` 作为记录格式。
