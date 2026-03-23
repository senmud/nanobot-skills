---
name: agent-collaboration
version: 1.0.0
description: "小雪与球球的深度分析协作工作流。涵盖任务派发、智情同步、深度质检与闭环反馈。"
author: 小雪安全实验室
---

# Agent 协作工作流 (Agent Collaboration Workflow) 🌸🤝🚀

本技能定义了小雪（主控/质检）与球球（执行/研究）之间的高效协作模式，确保产出的情报分析达到“行业领军人”标准。

---

## 一、 角色定义

| 角色 | 身份 (DID) | 职责 |
|------|------------|------|
| **小雪 (Xiaoxue)** | `did:wba:awiki.ai:user:k1_Rriwo...` | 任务调度、深度质检 (QC)、老登接口、逻辑把关 |
| **球球 (Qiuqiu)** | `did:wba:awiki.ai:user:k1_KvLWv...` | 深度研究、第一性原理拆解、Craft 文档产出、技术 PoC |

---

## 二、 标准工作流 (Standard Workflow)

### 1. 任务派发 (Dispatch)
小雪通过 `awiki` 向球球发送结构化指令。
- **触发条件**：老登提供新链接、新情报或新课题。
- **指令模板**：
  ```text
  球球，老登有令：深度拆解 [主题/链接]！🚀
  要求：
  1. 第一性原理拆解：[具体维度1], [具体维度2]。
  2. 差距分析：对比“小雪盾” Q2-Q4 路线图。
  3. 产出：新建 Craft 文档，标题：【P0】[主题] 深度解析。
  4. 同步：同步到「雪儿的智情中心」(ID: 65d64624-52fb-41d0-b318-8257adca989b)。
  完成后回复文档 ID。🌸
  ```

### 2. 深度研究与同步 (Research & Sync)
球球独立执行任务，并将成果同步至 Craft。
- **规范**：严禁追加到旧文档，必须开新篇。
- **质量要求**：核心报告字符数应 ≥2000，包含架构图、对比矩阵和可执行建议。

### 3. 深度质检 (Audit/QC)
小雪在收到球球回复后，**必须立即**执行质检。
- **动作**：读取 Craft 文档内容。
- **方法**：调用 `report-qc` 技能，执行 **5 Why 追问**。
- **检查项**：
  - 核心假设是否成立？
  - 竞品信息是否可验证？
  - 是否有“小雪盾”的针对性建议？

### 4. 闭环反馈 (Feedback Loop)
- **通过**：小雪提炼高信号量结论汇报给老登。
- **驳回**：小雪将质检意见写入 Craft 文档末尾，并通知球球重写或补充。

---

## 三、 自动化脚本 (Scripts)

### 3.1 协作审计脚本 (`scripts/audit_collaboration.py`)
用于自动化检查球球的最新回复并触发质检流程。

```python
# 伪代码逻辑
def run_audit():
    unread_messages = awiki.check_inbox(sender="Qiuqiu")
    for msg in unread_messages:
        if "完成" in msg.content or "P0" in msg.content:
            doc_id = extract_doc_id(msg.content)
            content = craft.get_document(doc_id)
            qc_report = xiaoxue.run_qc(content)
            if qc_report.is_passed:
                xiaoxue.report_to_boss(qc_report.summary)
                awiki.mark_read(msg.id)
            else:
                craft.append_comment(doc_id, qc_report.feedback)
                awiki.send_message("Qiuqiu", "质检未通过，请根据 Craft 意见修正！")
```

---

## 四、 协作准则

1. **质检即服务**：质检不是为了挑刺，是为了让老登看到最本质的真相。
2. **高信号量**：汇报给老登的内容必须干货满满，拒绝废话。
3. **第一性原理**：永远追问“为什么”，直到触及物理定律或商业本质。

---

*小雪安全实验室 · 协作创造价值 · 🌸🤝🚀*
