---
name: VerifyMaster
description: 对文本、URL、图片、视频、PDF、音频进行事实核查与可信度评估
version: 1.0.0
env:
  - name: VERIFYMASTER_BASE_URL
    description: API 根地址，如 https://api.verifymaster.info（可选，默认生产）
  - name: VERIFYMASTER_TOKEN
    description: JWT token，通过 POST /v1/auth/login 获取
---

# Instruction

当用户需要**验证一段文字、链接、图片、视频或 PDF 的真伪或可信度**时，使用本技能调用 VerifyMaster API。

**典型流程**：
1. 使用 `login` 获取 token（若尚未有 token）。
2. 使用 `getQuota` 或 `getAccountUsage` 查看余额与配额。
3. 使用 `submitVerification` 提交待验证内容（type: text | url | image | video | pdf | audio，content: 字符串或 URL）。
4. 若返回 status 为 processing，则轮询 `getTaskStatus` 直至 status 为 completed 或 failed。
5. 使用 `getQueryResult` 获取完整查证结果。

**错误处理**：若响应中有 `hint` 字段，可根据提示修正参数后重试。

---

# Tool Definition (OpenAI Function Calling style)

```json
{
  "tools": [
    {
      "type": "function",
      "function": {
        "name": "login",
        "description": "Login with email and password to get JWT token for VerifyMaster API",
        "parameters": {
          "type": "object",
          "properties": {
            "email": { "type": "string", "description": "User email" },
            "password": { "type": "string", "description": "Password" }
          },
          "required": ["email", "password"]
        }
      }
    },
    {
      "type": "function",
      "function": {
        "name": "getQuota",
        "description": "Get current user quota and points balance. Use before submitting verification to check if user can proceed.",
        "parameters": { "type": "object", "properties": {} }
      }
    },
    {
      "type": "function",
      "function": {
        "name": "submitVerification",
        "description": "Submit content for fact-checking. type: text|url|image|video|pdf|audio; content: the text, URL, or content to verify.",
        "parameters": {
          "type": "object",
          "properties": {
            "type": { "type": "string", "enum": ["text", "url", "image", "video", "pdf", "audio"] },
            "content": { "type": "string", "description": "Text to verify, or URL for url/image/video/pdf/audio" }
          },
          "required": ["type", "content"]
        }
      }
    },
    {
      "type": "function",
      "function": {
        "name": "getTaskStatus",
        "description": "Poll async verification task status. Call until status is completed or failed.",
        "parameters": {
          "type": "object",
          "properties": {
            "query_id": { "type": "string", "description": "Query ID returned from submitVerification" }
          },
          "required": ["query_id"]
        }
      }
    },
    {
      "type": "function",
      "function": {
        "name": "getQueryResult",
        "description": "Get full verification result for a query_id",
        "parameters": {
          "type": "object",
          "properties": {
            "query_id": { "type": "string" }
          },
          "required": ["query_id"]
        }
      }
    }
  ]
}
```

**API 根地址**：环境变量 `VERIFYMASTER_BASE_URL` 或默认 `https://api.verifymaster.info`。  
**认证**：除 login 外，请求头需带 `Authorization: Bearer <VERIFYMASTER_TOKEN>`。  
**OpenAPI 规范**：`GET {base}/v1/openapi.json`；**AI 发现**：`GET {base}/.well-known/ai-plugin.json`。
