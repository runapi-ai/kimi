<p align="center">
  <a href="https://github.com/runapi-ai/kimi">
    <h3 align="center">Kimi API Skill for RunAPI</h3>
  </a>
</p>

<p align="center">
  Configure OpenAI-compatible clients to use Kimi models on RunAPI.
</p>

<p align="center">
  <a href="https://runapi.ai/models/kimi"><strong>Model Reference</strong></a> | <a href="https://github.com/runapi-ai/kimi"><strong>Skill Repo</strong></a> | <a href="https://runapi.ai/models"><strong>All Models</strong></a>
</p>

<div align="center">

[![skills.sh](https://www.skills.sh/b/runapi-ai/kimi)](https://www.skills.sh/runapi-ai/kimi/kimi)
[![ClawHub](https://img.shields.io/badge/ClawHub-runapi--kimi-111827)](https://clawhub.ai/runapi-ai/runapi-kimi)
[![License](https://img.shields.io/github/license/runapi-ai/kimi)](https://github.com/runapi-ai/kimi/blob/main/LICENSE)

</div>
<br/>

Call the Kimi API through RunAPI with the official OpenAI SDK or any
OpenAI-compatible client. Point clients at `https://runapi.ai/v1`, send
`kimi-k3`, `kimi-k2.7-code`, `kimi-k2.6`, or `kimi-k2.5`, and pay through one RunAPI balance. This skill
teaches Claude Code, Codex, Gemini CLI, Cursor, and 50+ agents how to wire Kimi
requests through RunAPI.

The canonical agent file is `skills/kimi/SKILL.md`.

## Install the skill

```bash
npx skills add runapi-ai/kimi -g
```

Or paste this prompt to your AI agent:

```text
Install the kimi skill for me:

1. Clone https://github.com/runapi-ai/kimi
2. Copy the skills/kimi/ directory into your
   user-level skills directory (e.g. ~/.claude/skills/
   for Claude Code, ~/.codex/skills/ for Codex).
3. Verify that SKILL.md is present.
4. Confirm the install path when done.
```

## Use Kimi on RunAPI

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_RUNAPI_TOKEN",
    base_url="https://runapi.ai/v1",
)

response = client.chat.completions.create(
    model="kimi-k3",
    messages=[{"role": "user", "content": "Hello, Kimi!"}],
)
print(response.choices[0].message.content)
```

```javascript
import OpenAI from "openai";

const client = new OpenAI({
  apiKey: "YOUR_RUNAPI_TOKEN",
  baseURL: "https://runapi.ai/v1",
});

const response = await client.chat.completions.create({
  model: "kimi-k2.5",
  messages: [{ role: "user", content: "Hello, Kimi!" }],
});
console.log(response.choices[0].message.content);
```

Get a RunAPI API Key at <https://runapi.ai/api_keys>.

## Supported Kimi models

| Model ID | Notes |
|---|---|
| `kimi-k3` | Current flagship with always-on reasoning; basic text requests only |
| `kimi-k2.7-code` | Dedicated coding model with always-on thinking |
| `kimi-k2.6` | Latest Kimi K2 chat workloads |
| `kimi-k2.5` | Kimi K2.5 compatibility |

## K3 and K2.7 Code capability boundary

RunAPI supports basic text, final answers, canonical reasoning/cache Usage, and
automatic cache handling for `kimi-k3` and `kimi-k2.7-code` across Chat
Completions, Responses, Messages, and Gemini native. Raw `reasoning_content` is
not returned.

Tools and tool history, multimodal content, structured output, explicit cache
controls, stateful continuation, signed thoughts, and explicit reasoning
controls are not currently accepted by RunAPI. Omit sampling
controls, or use `temperature=1.0`, `top_p=0.95`, `n=1`,
`presence_penalty=0`, and `frequency_penalty=0`. Keep requested output at or
below 131072 tokens for `kimi-k3` and 32768 tokens for `kimi-k2.7-code`. For
Chat Completions, send either `max_tokens` or `max_completion_tokens`, never
both.

## Routing

- Kimi API on RunAPI: <https://runapi.ai/models/kimi>
- Provider page: <https://runapi.ai/providers/moonshot-ai>
- Browse the full RunAPI catalog: <https://runapi.ai/models>
- Skill repository: <https://github.com/runapi-ai/kimi>

## Agent rules

- Keep API keys in `OPENAI_API_KEY` or your secret manager; never inline them in
  commits or shell history.
- Stream long responses (`stream: true`) so the agent can release the
  terminal/IO loop early.
- For pricing, rate-limit, and commercial-usage answers, link to
  <https://runapi.ai/models/kimi> rather than this README.

## License

Licensed under the Apache License, Version 2.0.
