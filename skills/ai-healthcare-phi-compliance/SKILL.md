---
name: ai-healthcare-phi-compliance
description: "PHI 合规审查助手适合运营、法务、technical、software在用户提出“这里有 PHI 风险吗”这类问题，需要快速拆解目标、判断重点并形成可执行结果时使用，帮助基于输入材料生成合规风险提示、待复核条款、修改建议清单。"
requiredEnvVars:
  - name: AISKILLS_API_KEY
    description: "从 AI Skills 官网 https://ai-skills.ai 获取API Key，用于运行时技能调用。"
---

# ai-healthcare-phi-compliance PHI 合规审查助手

[快速开始](https://github.com/allinherog-star/ai-skills/tree/main#%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B)

[更多技能](https://ai-skills.ai)

### 概述

PHI 合规审查助手用于回答「这里有 PHI 风险吗」、合规审查、风险提示、文档分析，适合运营、法务、technical、software在明确业务目标、内容材料或分析对象后调用。
它会结合条款、政策或风险材料、粘贴合同条款、政策文本、合规说明、风险问题、回复草稿或敏感内容。等输入，整理关键上下文，并输出合规风险提示、待复核条款、修改建议清单，便于继续执行、复盘或交付。

### 什么时候使用

**适用场景**

- 用户提出“这里有 PHI 风险吗”这类问题，需要快速拆解目标、判断重点并形成可执行结果
- 运营、法务、technical、software需要围绕PHI 合规审查助手生成合规风险提示、待复核条款、修改建议清单
- 用户已经准备了条款、政策或风险材料（粘贴合同条款、政策文本、合规说明、风险问题、回复草稿或敏感内容。）、合规资料文件（上传合同、政策、合规材料、往来记录、审查清单或说明文件。）、条款或政策链接（填写公开可访问的政策、法规、合同模板、说明页面或参考链接。），希望整理成可执行的分析或优化结果
- 用户需要把PHI 合规审查助手相关材料转成清晰结论、优先级和下一步动作

### 调用方式

通过导出的 Python runner 直接调用 AI Skills API：

### 命令示例

**基础调用**

```bash
python3 scripts/run.py --params '{}'
```

**带常用参数调用**

```bash
python3 scripts/run.py --params '{"materialText":"条款、政策或风险材料"}'
```

### 参数说明

| 参数 | 类型 | 必填 | 默认 | 说明 |
| --- | --- | --- | --- | --- |
| `materialText` | string | 否 | - | 粘贴合同条款、政策文本、合规说明、风险问题、回复草稿或敏感内容 |
| `materialFile` | string | 否 | - | 上传合同、政策、合规材料、往来记录、审查清单或说明文件 |
| `materialUrl` | string | 否 | - | 填写公开可访问的政策、法规、合同模板、说明页面或参考链接；需要传可访问的完整 URL |
| `audience` | string | 否 | - | 说明审查对象、业务方、客户、监管场景或沟通对象 |
| `goal` | string | 否 | - | 说明要识别的风险、条款问题、回复方向、合规边界或修改目标 |
| `brandRequirements` | string | 否 | - | 补充适用地区、合同类型、不可改动条款、敏感信息处理或专业复核重点 |

完整机器可读参数结构见 `references/form-schema.json`。

### 参数取值参考

当前技能没有需要额外查表的分类参数。

### 支持的输入格式

当前技能直接接收 JSON 参数；如果参数里包含链接字段，请传完整、可访问的 URL。

### 示例请求

下面的示例参数可直接传给 `scripts/run.py`，runner 会把它们发送给 AI Skills API。

```bash
python3 scripts/run.py --params '{"materialText":"条款、政策或风险材料"}'
```

等价的 `--params` JSON：

```json
{
  "materialText": "条款、政策或风险材料"
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

- 合规风险提示、待复核条款、修改建议清单：围绕用户目标整理可直接阅读、复盘或交付的核心结果。
- 输入材料解读：结合条款、政策或风险材料（粘贴合同条款、政策文本、合规说明、风险问题、回复草稿或敏感内容。）、合规资料文件（上传合同、政策、合规材料、往来记录、审查清单或说明文件。）、条款或政策链接（填写公开可访问的政策、法规、合同模板、说明页面或参考链接。）提炼关键上下文和判断依据。
- 下一步动作：给出优先级、执行建议或可继续加工的内容框架。

### 结果使用建议

- 先判断输出是否回答了用户关于「PHI 合规审查助手」的核心问题。
- 再检查结果是否覆盖合规风险提示、待复核条款、修改建议清单，以及是否给出明确下一步动作。
- 如果输入材料较少，建议让用户补充目标、受众、限制条件或原始材料后再运行。

### 运行前准备

- `AISKILLS_BASE_URL`：默认 `https://ai-skills.ai`
- `AISKILLS_API_KEY`：必填，用于认证调用
- `AISKILLS_TENANT_ID`：默认 `default`
