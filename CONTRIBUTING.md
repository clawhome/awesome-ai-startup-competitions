# 贡献指南 Contributing

## 提交一条新比赛

1. 编辑 `data/competitions.json`，按下方 schema 增加一条记录；
2. **语言规则**：国内比赛（`region: "cn"`）全中文填写；国际比赛（`region: "intl"`）全英文填写；
3. 运行 `node scripts/build-readme.mjs` 重新生成 README 与 CSV；
4. `README.md` 是脚本生成文件，**禁止直接手改**。

## 字段定义

| 字段 | 必填 | 说明 |
|---|---|---|
| slug | 必填 | 唯一 ID，小写字母数字与连字符 |
| name | 必填 | 官方名称，用来源语言书写 |
| region | 必填 | `cn` / `intl`，决定归属板块与呈现语言 |
| organizer | 必填 | 主办方 |
| eligibility | 必填 | 参赛资格（学生 / 企业 / 个人、成立年限等硬门槛） |
| stage | 必填 | 要求所处阶段：idea / 有原型 / 有收入 |
| deadline | 条件 | 报名截止日 `YYYY-MM-DD`；不填且非常年时按「预告」处理 |
| rolling | 条件 | `true` 表示常年开放、不设截止（与 deadline 二选一） |
| status_override | 可选 | `announced` = 已官宣但报名未开始 |
| opens_at | 可选 | 预告条目的预计开报日期 |
| event_date | 可选 | 决赛 / 活动日期 |
| prize | 必填 | 奖金与非现金权益（投资对接、云额度、加速名额等） |
| tracks | 可选 | 赛道数组 |
| format | 可选 | 参赛形式（线上提交 / 现场路演 / 黑客马拉松） |
| name_zh | 可选 | 国际条目可选的中文名注释 |
| url | 必填 | 官网链接，提交前必须验证可打开 |
| last_verified | 必填 | 最后人工核实日期 `YYYY-MM-DD` |

## 规则

- `status` 不需要填：脚本按 `deadline` 与当天日期自动计算（正在报名 / 常年开放 / 预告 / 已结束）；
- 提交前请打开官网核对报名资格、截止日、奖金三项，并把 `last_verified` 填为当天；
- 已结束的比赛不删除，保留在「已结束归档」分组中，供研究历届；
- 状态分组的名称与顺序由脚本控制，PR 中请勿手动调整。
