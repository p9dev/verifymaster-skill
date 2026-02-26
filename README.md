# VerifyMaster — Skill Repository

> For the public skill repo: use this file as **README.md** and **README.verifymaster-skill.zh-CN.md** as **README.zh-CN.md**.

This repository provides the **VerifyMaster** AI Agent skill definition (`skill.md`) for use with [OpenClaw](https://github.com/OpenClaw) or other agents that support skill discovery.

---

## What is VerifyMaster?

**VerifyMaster** (查证大师) is an intelligent content verification platform that helps users assess the **accuracy** and **logical validity** of information found online.

### Core capabilities

- **Fact-checking**: Verifies key claims in articles, news, and social media against authoritative sources.
- **Logic analysis**: Identifies common logical fallacies and rhetorical tricks (e.g. straw man, slippery slope, appeal to authority, hasty generalization).
- **Multiple input types**: Supports **text**, **URLs**, **images**, **PDF**, **audio**, and **video** in a single submission, with a unified report.
- **Multilingual**: Interface and results support Chinese, English, and more.

### Example use cases

| Use case | Description |
|----------|-------------|
| Health & wellness | Verify claims like “X prevents cancer” or “Y cures all”; reduce exposure to health myths. |
| News & trending topics | Check breaking news, viral screenshots, or chat logs for accuracy and sources. |
| Social media | Quickly judge whether posts, group messages, or short videos are trustworthy. |
| Study & writing | Check whether arguments are well-supported and free of logical flaws; support critical thinking. |
| AI agents & automation | Use the API or this skill to integrate verification into assistants, workflows, etc. |

### What’s in the report?

- **Fact-check list**: Each main claim is labeled (verified true / partially true / false / unverifiable).
- **Logic analysis**: Types and locations of logical fallacies in the text, with short explanations.
- **Overall assessment**: Fact reliability and logical rigor scores, plus a verdict (reliable / partially reliable / misleading / false).
- **References**: Links to authoritative sources for further reading.

---

## Links and resources

| Resource | URL |
|----------|-----|
| **Website** | [https://verifymaster.info](https://verifymaster.info) |
| **API docs** | [https://verifymaster.info/docs](https://verifymaster.info/docs) |
| **For AI / Agent guide** | [https://verifymaster.info/docs/for-ai](https://verifymaster.info/docs/for-ai) |
| **OpenAPI spec** | [https://api.verifymaster.info/v1/openapi.json](https://api.verifymaster.info/v1/openapi.json) |
| **AI plugin manifest** | [https://api.verifymaster.info/.well-known/ai-plugin.json](https://api.verifymaster.info/.well-known/ai-plugin.json) |
| **Skill file (this skill)** | [https://api.verifymaster.info/.well-known/skill.md](https://api.verifymaster.info/.well-known/skill.md) |

---

## Contents of this repository

- **`skill.md`**: Skill definition for OpenClaw and similar agents (YAML frontmatter + OpenAI Function Calling–style tools: login, get quota, submit verification, poll status, get result).
- **`README.md`**: This file (English).
- **`README.zh-CN.md`**: Same overview in Chinese.

### How to use this skill

1. **Option A: Add this repo as a skill source**  
   In OpenClaw or any agent that supports “load skill from Git repo,” add this repository as a skill source. The agent will use the tools defined in `skill.md` to call the VerifyMaster API.

2. **Option B: Use the skill URL**  
   If your tool supports “add skill by URL,” use the **Skill file** link above:  
   `https://api.verifymaster.info/.well-known/skill.md`

3. **API and authentication**  
   Call `POST /v1/auth/login` to obtain a JWT, then send `Authorization: Bearer <token>` on all other requests. Full details are in the [API docs](https://verifymaster.info/docs) and [For AI guide](https://verifymaster.info/docs/for-ai).

---

## Sign up and usage

- Register at [verifymaster.info](https://verifymaster.info) to use verification in the browser or via the API / this skill.
- The free tier includes a daily allowance of text verifications; subscriptions or points unlock more quota and types (image, PDF, audio, video). See the website and API docs for pricing.

---

## License and contact

- The `skill.md` and README in this repo are for documentation and integration only.
- Use of the verification service is subject to [VerifyMaster terms and policies](https://verifymaster.info).
- Questions or feedback: support@verifymaster.info.
