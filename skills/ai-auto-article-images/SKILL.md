---
name: ai-auto-article-images
description: "智能配图助手适合内容创作者、运营、technical、内容媒体在用户提出“还要配图，好麻烦”这类问题，需要快速拆解目标、判断重点并形成可执行结果时使用，帮助基于输入材料生成摘要、诊断结论、行动建议和可复用交付物。"
requiredEnvVars:
  - name: AISKILLS_API_KEY
    description: "从 AI Skills 官网 https://ai-skills.ai 获取API Key，用于运行时技能调用。"
---

# ai-auto-article-images 智能配图助手

[快速开始](https://github.com/allinherog-star/ai-skills/tree/main#%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B)

[更多技能](https://ai-skills.ai)

### 概述

智能配图助手用于回答「还要配图，好麻烦」、配图、封面、文章图片，适合内容创作者、运营、technical、内容媒体在明确业务目标、内容材料或分析对象后调用。
它会结合正文、文章正文或 Markdown等输入，整理关键上下文，并输出摘要、诊断结论、行动建议和可复用交付物，便于继续执行、复盘或交付。

### 什么时候使用

**适用场景**

- 用户提出“还要配图，好麻烦”这类问题，需要快速拆解目标、判断重点并形成可执行结果
- 内容创作者、运营、technical、内容媒体需要围绕智能配图助手生成摘要、诊断结论、行动建议和可复用交付物
- 用户已经准备了视觉风格、标题、配图数量，希望整理成可执行的分析或优化结果
- 用户需要把智能配图助手相关材料转成清晰结论、优先级和下一步动作

### 调用方式

通过导出的 Python runner 直接调用 AI Skills API：

### 命令示例

**基础调用**

```bash
python3 scripts/run.py --params '{}'
```

**带常用参数调用**

```bash
python3 scripts/run.py --params '{"style":"clean-commercial"}'
```

### 参数说明

| 参数 | 类型 | 必填 | 默认 | 说明 |
| --- | --- | --- | --- | --- |
| `style` | string | 否 | `clean-commercial` | 视觉风格；可选值：清爽商业（`clean-commercial`）、杂志摄影（`editorial-photo`）、柔和插画（`soft-illustration`）、科技图解（`tech-diagram`） |
| `title` | string | 否 | - | 标题 |
| `imageCount` | integer | 否 | `4` | 配图数量 |
| `sourceText` | string | 否 | - | 文章正文或 Markdown |
| `coverRatios` | array | 否 | `["2.35:1","1:1","16:9","3:4","9:16"]` | 封面比例 |
| `watermarkMode` | string | 否 | `off` | 水印；可选值：不加（`off`）、右下角（`corner`）、平铺（`tiled`）、两者（`both`） |
| `sourceDocument` | string | 否 | - | 支持 docx、md、txt 等文本文件 |
| `publishPlatform` | string | 否 | `all` | 发布平台；可选值：全平台（`all`）、公众号（`wechat`）、小红书（`xhs`）、博客（`blog`）、知乎（`zhihu`） |
| `brandRequirements` | string | 否 | - | 品牌要求 |

完整机器可读参数结构见 `references/form-schema.json`。

### 参数取值参考

当前技能没有需要额外查表的分类参数。

### 支持的输入格式

当前技能直接接收 JSON 参数，不涉及分享链接解析。

### 示例请求

下面的示例参数可直接传给 `scripts/run.py`，runner 会把它们发送给 AI Skills API。

```bash
python3 scripts/run.py --params '{"style":"clean-commercial"}'
```

等价的 `--params` JSON：

```json
{
  "style": "clean-commercial"
}
```

### 返回结果示例

```json
{
  "success": true,
  "data": {
    "message": "示例结果请以技能真实返回结构为准。"
  },
  "meta": {
    "executionTime": 842,
    "cached": false
  }
}
```

### 交付内容

- 摘要、诊断结论、行动建议和可复用交付物：围绕用户目标整理可直接阅读、复盘或交付的核心结果。
- 输入材料解读：结合视觉风格、标题、配图数量提炼关键上下文和判断依据。
- 下一步动作：给出优先级、执行建议或可继续加工的内容框架。

### 结果使用建议

- 先判断输出是否回答了用户关于「智能配图助手」的核心问题。
- 再检查结果是否覆盖摘要、诊断结论、行动建议和可复用交付物，以及是否给出明确下一步动作。
- 如果输入材料较少，建议让用户补充目标、受众、限制条件或原始材料后再运行。

### 运行前准备

- `AISKILLS_BASE_URL`：默认 `https://ai-skills.ai`
- `AISKILLS_API_KEY`：必填，用于认证调用
- `AISKILLS_TENANT_ID`：默认 `default`
