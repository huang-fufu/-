---
name: reanimai-script-creator
description: 自动化操作 ReanimAI 平台的剧本创作全流程（导入素材 → 生成大纲 → 结构细纲 → 分幕场次 → 故事审核 → 生成剧本 → 下载剧本）。当用户提到在 ReanimAI 上写剧本、创作剧本、生成剧本时使用。
---

# ReanimAI 剧本创作 Skill

自动化操作 ReanimAI 平台的剧本创作全流程，覆盖从导入素材到下载剧本的 7 个步骤。

## 触发条件

当用户提到以下关键词时自动激活：
- "在 ReanimAI 上写剧本" / "ReanimAI 剧本创作"
- "生成剧本" / "创作剧本" / "写短剧"
- "导入素材到 ReanimAI" / "生成项目大纲"
- "生成分幕场次" / "故事结构审核" / "下载剧本"

## 前置要求

1. **浏览器控制**：Playwright MCP 或 Trae 浏览器控制插件已可用
2. 用户已登录 ReanimAI 账号
3. 用户已准备好创作素材（故事创意、参考文本、角色设定等）

## 核心流程

```
Step 1: 导入素材/创意
    ↓
Step 2: 生成项目大纲
    ↓
Step 3: 生成结构细纲
    ↓
Step 4: 生成分幕场次
    ↓
Step 5: 故事结构审核
    ↓
Step 6: 生成正式剧本
    ↓
Step 7: 下载剧本
```

## 子 Skill 索引

| 步骤 | 子 Skill | 路径 | 功能 |
|------|---------|------|------|
| 1 | 导入素材 | sub-skills/01-import-material/SKILL.md | 上传素材或输入创意到 ReanimAI |
| 2 | 项目大纲 | sub-skills/02-project-outline/SKILL.md | 基于素材生成项目大纲 |
| 3 | 结构细纲 | sub-skills/03-structure-outline/SKILL.md | 生成详细的结构细纲 |
| 4 | 分幕场次 | sub-skills/04-act-scene/SKILL.md | 生成分幕和场次划分 |
| 5 | 故事审核 | sub-skills/05-story-review/SKILL.md | 对故事结构进行审核 |
| 6 | 正式剧本 | sub-skills/06-script-writing/SKILL.md | 生成正式剧本文本 |
| 7 | 下载剧本 | sub-skills/07-download-script/SKILL.md | 下载生成的剧本文件 |

## 使用方式

### 快速开始

用户只需说一句话，例如：
- "帮我在 ReanimAI 上写一个都市情感短剧的剧本"
- "用 ReanimAI 创作一个悬疑剧本，素材是这个..."
- "在 ReanimAI 上继续写剧本，到第3步了"

### 完整流程示例

```
用户: "帮我在 ReanimAI 上创作一个都市情感短剧"
→ 加载 01-import-material → 输入创意
→ 加载 02-project-outline → 生成大纲
→ 加载 03-structure-outline → 生成细纲
→ 加载 04-act-scene → 生成分幕
→ 加载 05-story-review → 审核结构
→ 加载 06-script-writing → 生成剧本
→ 加载 07-download-script → 下载
```

## 注意事项

1. **逐步确认**：每完成一个步骤，截图展示给用户确认后再进入下一步
2. **等待生成**：AI 生成需要时间，操作后需截图确认状态再继续
3. **登录态**：如果检测到未登录，先走登录流程（参考 reanimai-skill 的 login-navigate）
4. **错误处理**：如果某步失败，截图反馈给用户，不要盲目重试
5. **中断恢复**：如果用户中途打断，记录当前步骤，下次可以从断点继续
6. **逐个操作**：避免并发批量操作，防止触发平台数据库死锁（SQLSTATE 40P01）
