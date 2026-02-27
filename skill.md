---
name: VerifyMaster
description: Fact-checking and credibility assessment for text, URLs, images, video, PDF, and audio
version: 1.0.0
env:
  - name: VERIFYMASTER_BASE_URL
    description: API base URL, e.g. https://api.verifymaster.info
  - name: VERIFYMASTER_TOKEN
    description: JWT token obtained via POST /v1/auth/login
---

# Instruction

Use this skill to call the VerifyMaster API when the user wants to **verify the accuracy or credibility of text, a link, an image, a video, or a PDF**.

**Typical flow**:
1. Use `login` to get a token (if you do not have one yet).
2. Use `getQuota` or `getAccountUsage` to check balance and quota.
3. Use `submitVerification` to submit content (type: text | url | image | video | pdf | audio; content: string or URL).
4. If the response status is processing, poll `getTaskStatus` until status is completed or failed.
5. Use `getQueryResult` to get the full verification result.

**Error handling**: If the response includes a `hint` field, correct parameters according to the hint and retry.

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

**API base URL**: Environment variable `VERIFYMASTER_BASE_URL` or default `https://api.verifymaster.info`.  
**Authentication**: For all requests except login, send header `Authorization: Bearer <VERIFYMASTER_TOKEN>`.  
**OpenAPI spec**: `GET {base}/v1/openapi.json`; **AI discovery**: `GET {base}/.well-known/ai-plugin.json`.
