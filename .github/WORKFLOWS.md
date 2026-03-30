# 自动同步翻译工作流配置指南

## 功能说明

本仓库配置了两个 GitHub Actions workflow，用于自动从上游仓库同步更新并翻译为中文。

### 1. auto-sync-translate.yml (主要)

**触发条件**：
- 每天 UTC 2:00（北京时间 10:00）自动检查上游更新
- 可手动触发（支持强制重新翻译）

**功能**：
- 从上游仓库 `walkinglabs/awesome-harness-engineering` 拉取最新变更
- 自动翻译变更的 markdown 文件为中文
- 将中文版替换为默认文件（README.md, CONTRIBUTING.md 等）
- 自动提交并推送

### 2. sync-upstream.yml (备用)

**触发条件**：
- 每 6 小时检查一次
- 仅同步代码，不自动翻译

**功能**：
- 同步上游变更
- 创建 issue 提醒需要翻译

---

## API Key 配置

要启用自动翻译功能，需要在 GitHub Secrets 中配置翻译 API：

### 步骤

1. 进入仓库 **Settings** → **Secrets and variables** → **Actions**
2. 点击 **New repository secret**
3. 添加以下任一 API Key：

| Secret Name | Description | Get from |
|-------------|-------------|----------|
| `DEEPL_API_KEY` | DeepL 翻译 API（推荐，支持中文较好） | https://www.deepl.com/pro-api |
| `ANTHROPIC_API_KEY` | Claude API | https://console.anthropic.com/ |

---

## 翻译流程

```
上游仓库更新
       ↓
检测到变更
       ↓
拉取最新代码
       ↓
翻译 markdown 文件 (DeepL/Claude)
       ↓
生成 *-zh.md 文件
       ↓
替换为中文版 (README-zh.md → README.md)
       ↓
提交并推送
```

---

## 手动触发

1. 进入仓库 **Actions** 标签页
2. 选择 **Sync Upstream and Auto Translate** workflow
3. 点击 **Run workflow**
4. 可选：勾选 "Force re-translate all files"

---

## 文件命名规范

| 源文件 | 翻译后 | 最终使用 |
|--------|--------|----------|
| README.md | README-zh.md | README.md (中文) |
| CONTRIBUTING.md | CONTRIBUTING-zh.md | CONTRIBUTING.md (中文) |
| .github/pull_request_template.md | .github/pull_request_template-zh.md | .github/pull_request_template.md (中文) |

---

## 故障排查

### Workflow 不执行

1. 检查 **Actions** 标签页是否启用了 workflow
2. 确认有权限执行 Actions

### 翻译失败

1. 检查 API Key 是否有效
2. 查看 workflow run 的日志

### 冲突处理

如果上游变更与本地翻译有冲突，手动解决后推送即可。

---

## 注意事项

- CC0 1.0 许可证允许翻译和修改
- 保留原文备份（*.en.bak）以便对照
- 机器翻译可能需要人工校对
