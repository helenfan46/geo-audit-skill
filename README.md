# GEO Audit Skill

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)
[![Version](https://img.shields.io/badge/version-4.1.0-green.svg)](./SKILL.md)
[![Built for](https://img.shields.io/badge/built_for-any_LLM_with_sub--agents-orange.svg)](#requirements)

> A self-serve audit that tells a professional services firm where it stands in AI-generated answers — and what content gaps to fix first.

Give an AI agent a firm name and website URL. It identifies competitors, generates 15 grounded test prompts, spawns isolated sub-agents to answer each one cold, and produces a narrative-first Word report (max 10 pages) showing where the firm is visible and invisible in AI answers.

Built during the [100-day OpenClaw Law experiment](https://helenlab.com/openclawlaw) by [Helen Fan](https://www.linkedin.com/in/helenfanlegalai/).

---

## What it does

1. **Auto-identifies 3–5 competitors** from the firm's website (you provide only the name + URL).
2. **Audits competitor content** — blogs, insights pages, newsletters, resource hubs.
3. **Generates 15 test prompts** from three real sources — competitor websites, Reddit, and Google "People Also Ask" — each source researched by a separate sub-agent.
4. **Spawns 15 isolated sub-agents** to answer each prompt with zero research context, then records which firms get mentioned and with what sentiment.
5. **Produces a narrative-first Word report** with executive summary, visibility scorecard, and prioritized content recommendations.

## What it cannot do

- **Produce a cross-model measurement.** Sub-agents run on the same model as the main agent — results are directional, not definitive. A true multi-model baseline requires testing across ChatGPT, Perplexity, Gemini, etc. in clean sessions.
- Scrape forums that aggressively block bots (Reddit may CAPTCHA; Quora/AVVO consistently block).
- Replace a dedicated marketing agency or technical SEO audit.

---

## Quick Start

1. Open this `SKILL.md` in any LLM agent that supports **web search + web browsing + sub-agent delegation** (Claude, GPT, Gemini, Kimi, Hermes, or any agent platform with isolated sub-tasks).
2. Paste the skill into the agent's instructions (or load it as a skill if your platform supports it).
3. Run a prompt like:

   > Run a GEO audit for **[Firm Name]** (**[firm-url.com]**). They are a **[size] [type]** firm. Practice areas: **[list]**.

4. Approve the auto-identified competitor list when the agent presents it.
5. Wait for the agent to finish Steps 1–5. Default deliverable is a `.docx` report.

## Requirements

This skill works with **any LLM that has:**

- Web search
- Web browsing
- Sub-agent / delegation capability (for the isolated-baseline step)

If your platform does not support sub-agents, you can still run Steps 0–2 and Step 4 (research + prompts + gap analysis). See [the fallback section](./SKILL.md#step-3-isolated-sub-agent-baseline-testing) in `SKILL.md`.

---

## Why isolated sub-agents?

When one agent does everything — researches the firm, audits competitors, generates prompts, AND answers those prompts — its answers are biased. By the time it reaches the testing step, it has spent thousands of tokens reading about the target firm. Asking it to "answer neutrally" doesn't work; it carries that context forward.

**The fix:** for each of the 15 test prompts, the main agent spawns a separate, isolated sub-agent that receives only the prompt and a generic "answer as a helpful AI" instruction — no firm name, no research context, no competitor data.

This gives a single-model visibility baseline that's more reliable than predicting from website content, but less reliable than a multi-model test across providers. The skill enforces a [transparency disclaimer](./SKILL.md#disclaimer-the-agent-must-include) on every report so readers know what they're looking at.

---

## Sample output

A sample executive-summary headline from a real audit:

> **"Knobbe Martens appears in 7 out of 15 AI-generated answers (47%). It is visible on FIND queries but invisible on RISK and COMPARE queries — the highest-converting question types."**

The full report includes:

- Visibility scorecard (firm × prompt × sentiment)
- The 15 prompts with source attribution (competitor blog, Reddit thread, or Google PAA)
- 5–8 prioritized content recommendations
- Competitor content audit summary
- Methodology, limitations, and full source list

See the [Sample Output section in SKILL.md](./SKILL.md#sample-output-visibility-scorecard) for a worked example.

---

## File structure

```
geo-audit-skill/
├── README.md       # This file
├── SKILL.md        # The full skill — load this into your LLM agent
├── LICENSE         # AGPL-3.0
└── .gitignore
```

---

## Versioning & origin

Current version: **4.1.0**

This skill evolved from v1 (content-analysis predictions) through v4 (isolated sub-agent testing with narrative-first reporting), iterated on real client work during the 100-day OpenClaw Law experiment.

Created by [Helen Fan](https://www.linkedin.com/in/helenfanlegalai/) × Morgan (an AI agent collaborator). The workflow was auto-generated into a skill by the agent, then reviewed and revised by a human attorney.

---

## Contributing

Issues and pull requests welcome. Real-world test results (which firms / which models / which queries) are especially valuable — they sharpen the prompt generation logic and the disclaimer language.

If you adapt the skill for a non-legal vertical (consulting, accounting, IB, healthcare advisory, etc.), please open a PR with the variant — that's exactly what an AGPL fork should look like.

---

## License

**AGPL-3.0** — free to use, modify, and share.

If you build a product or service on top of this skill, you must open-source your modifications under the same license. See [LICENSE](./LICENSE) for the full text, or [gnu.org/licenses/agpl-3.0](https://www.gnu.org/licenses/agpl-3.0.en.html) for a plain-language summary.

---

## Get a deeper assessment

This skill gives you a **single-model directional baseline**. For a comprehensive multi-model baseline across ChatGPT, Perplexity, and Gemini — or to discuss your firm's marketing strategy in the AI era — Helen offers it as a consultancy service: [helenlab.com/consultancy](https://www.helenlab.com/consultancy).

Contact: **helen@helenlab.com**
