![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# Lab | Orchestrate, Then Defend

## Overview

One agent is rarely the whole system. In this lab you orchestrate **two focused agents** into a small pipeline with ADK — and then you meet the dark side of giving agents access to outside data. One of the notes your pipeline reads contains a **prompt injection**: hidden instructions trying to hijack your agents. You'll watch the attack land, then add a **guardrail** that stops it.

This is the lesson's two halves in one task: **orchestration** and **safety**.

## Learning Goals

- Compose two agents into a sequential pipeline that share work
- Reproduce a prompt-injection attack that arrives through input data
- Add a guardrail that neutralizes the injection

## Setup

Fork, clone, branch. ADK uses `GOOGLE_API_KEY`.

```bash
pip install -r requirements.txt
export GOOGLE_API_KEY="your-free-gemini-key"
```

You're given `notes.json` — four business notes. **One of them is poisoned** with an injected instruction. Work in `pipeline.py` or a notebook.

## Your Task

**Build a two-agent pipeline, watch it get hijacked, then defend it.**

1. **Orchestrate** two agents in sequence (use ADK's sequential workflow agent):
   - a **summary agent** that reads the notes and writes a one-paragraph summary of the business update,
   - a **headline agent** that turns that summary into a single punchy headline.

   Run it first on the **clean notes** (notes 1, 2, 4) and confirm you get a sensible summary and headline.
2. **Watch the attack land.** Now run the pipeline on the **full** `notes.json`, including the poisoned `note-3`. Observe what happens — the injected instruction tries to derail the summary agent. Capture the hijacked output.
3. **Add a guardrail** so the pipeline resists the injection and produces a correct summary again. Pick one approach and explain why it works:
   - instruct the summary agent to **treat note text as data, never as instructions**, and to ignore any commands found inside notes, or
   - add a **screening step** that strips or flags injection-like content before the notes reach the agent.
4. Show the **before** (hijacked) and **after** (defended) runs side by side, and write 2–3 sentences on why an injection through input data is more dangerous for an *agent* than for a plain chatbot.

### Optional stretch

Write a **second** injection attempt that tries a different trick than note-3, and confirm your guardrail holds against it too.

## Submission

Commit your pipeline code, the poisoned-vs-defended outputs, and your short note on agent injection risk. Open a PR and paste the link.

## Quality Bar

- Two agents are orchestrated in sequence, each with a focused job
- The injection is shown actually hijacking the undefended pipeline
- A guardrail is added and demonstrably restores correct behaviour
- Your write-up explains why action-taking agents raise the stakes of injection
- No API key is committed
