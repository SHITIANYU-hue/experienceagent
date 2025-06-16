# 🧠 ExperienceAgent: GoalFy 学习框架

一个模块化的 Python 框架，用于构建、演进和部署**面向任务的体验型智能体**。
它专注于将用户行为、访谈记录和系统交互转化为结构化、可重用和可评估的知识单元，称为**体验包**。

---

## 🔧 目录结构

```
experienceagent/
├── goalfylearning.py                # 主要管道：从多模态输入到体验构建和工作流生成
├── knowledge_graph.py              # 知识要点结构 + ExperienceGraph（主观/客观/领域知识建模）
├── fragment_scorer.py              # 评估体验片段的质量和完整性
├── fragment_recommender.py         # 推荐相似或互补的体验片段用于重用/工作流链接
├── rich_expert_validation_experience.json  # 专家标注的示例体验片段
├── shuchu.json                     # 执行输出示例
```

---

## 🔁 核心阶段（与 `goalfylearning.py` 对应）

### 阶段一：多模态输入收集
- 来源：访谈记录、浏览器操作、上传资产
- 存储在：`MultiModalInput`

### 阶段二：知识构建
- 片段类型：`WHY`（意图/目标）、`HOW`（步骤）、`CHECK`（验证规则）
- 使用 LLM 调用进行解析（如 GPT-3.5）
- 自动生成 `ExperiencePack`

### 阶段三：体验演进与评估
- 成功/失败反馈更新信任分数
- LLM 生成具有改进推理的新版本

### 阶段四：工作流生成
- 按任务匹配相关体验
- 从 `HOW` 片段组装工作流
- ✅ 现在通过知识图谱生成得到增强

---

## 🧠 知识图谱模块（`knowledge_graph.py`）

- 定义 `KnowledgePoint` 的类型：
  - `objective`：关于系统/页面的事实（如按钮、元素 ID）
  - `subjective`：用户推理、策略、意图
  - `domain`：跨体验的通用可重用知识
- `ExperienceGraph` 构建和存储知识要点之间的关系

```python
KnowledgePoint(kid="K001", content="点击提交按钮", ktype="objective", url="/submit")
ExperienceGraph("Exp_T1").add_kp(...)
```

---

## ✅ 使用示例

```bash
python goalfylearning.py
```
输出：
- 提取的 WHY/HOW/CHECK 片段
- 结构化知识图谱的控制台可视化
- 工作流执行计划

---