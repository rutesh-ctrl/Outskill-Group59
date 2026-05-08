# Vera

> **Honest about your money. Finally.**

[![Built with Bolt](https://img.shields.io/badge/Built%20with-Bolt-6C47FF?style=flat-square)](https://bolt.new)
[![Backend](https://img.shields.io/badge/Backend-Bolt_Native-6C47FF?style=flat-square)](https://bolt.new)
[![OpenAI](https://img.shields.io/badge/AI-OpenAI%20GPT--4o--mini-412991?style=flat-square)](https://openai.com)
[![Hackathon](https://img.shields.io/badge/Accelerator-Hackathon%202026-F5A623?style=flat-square)](#)

---

## What is Vera?

Most people have a vague, anxious relationship with their money. Their banking app shows every transaction — but gives zero interpretation. No categories. No patterns. No "here's what to do about it."

**Vera closes the gap between data and decision.**

Type an expense the way you'd say it out loud — *"grabbed a coffee, £4.50"* — and Vera's AI instantly categorises it, flags whether it was essential or avoidable, and updates your dashboard. Once a day, it delivers a plain-English summary in the voice of an encouraging financial mentor: honest, direct, and always ending with one clear action you can take.

No forms. No bank sync required. No spreadsheets. Just clarity.

---

## Features

### Core (MVP)

- **Natural language expense entry** — type expenses exactly how you'd say them; AI parses amount, category, and date automatically
- **Goal-aware AI** — Vera knows what you're trying to achieve (save more, spend less, clear debt) and frames every insight around it
- **AI micro-reaction** — a single sharp observation on every expense you log, even the very first one
- **AI auto-categorisation** — every expense instantly assigned to one of 8 categories: Food & Drink, Transport, Shopping, Entertainment, Health, Subscriptions, Bills, Other
- **Spending dashboard** — real-time weekly and monthly view with category breakdown chart
- **AI mentor summary** — a daily plain-English insight card in the voice of an encouraging financial mentor: warm, direct, and actionable
- **Currency support** — 5 currencies at launch (GBP, USD, EUR, INR, AUD) with locale-correct formatting
- **Secure auth** — email login with verification; your data persists across sessions

### Coming Soon

- Essential vs. avoidable tagging per expense
- Monthly budget caps per category
- Recurring subscription detection
- Spending streaks and habit nudges
- Expand currency support beyond the 5 MVP currencies
- Weekly mentor email (automated)

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend + Backend + Auth | [Bolt](https://bolt.new) (built-in database and authentication) |
| AI | [OpenAI GPT-4o-mini](https://openai.com) via [OpenRouter](https://openrouter.ai) (key protected) |
| Currency formatting | Native `Intl.NumberFormat` API |
| Hosting | Bolt deploy |

---

## Getting Started

### Prerequisites

- An [OpenRouter](https://openrouter.ai) API key (sign up free, set a £5 credit limit)
- A [Bolt](https://bolt.new) account

### Environment variables

Add the following in Bolt's environment variables panel:

```env
VITE_OPENROUTER_API_KEY=your_openrouter_api_key
```

### Running the project

Open the project in Bolt and click Run. No local setup required — Bolt handles the database, auth, and hosting natively.

---

## Hackathon Goals

Built in 3 days at the **Accelerator Hackathon, May 2026**.

**The must-have flow:**
> User signs up → states their financial goal → enters income and outgoings → selects currency → lands on a populated dashboard → types an expense in plain English → reads a goal-aware AI micro-reaction → sees the dashboard update live.

**Definition of done for the demo:**
> A judge types one expense, sees it categorised instantly, reads a micro-reaction that references their goal, and sees the dashboard update — all within 90 seconds of landing on the app.

**Judging criteria we are targeting:**
- Strength of the problem and pain point articulation
- Creativity of the AI integration — goal-aware, not bolted on
- Quality of the demo story and live flow

---

## The Problem We Are Solving

> UK adults living payday to payday have the anxiety but not the answers. Every tool that could help either demands bank access they don't trust, or delivers data without any meaning. The result is avoidance — they don't track, don't improve, and stay stuck. Vera removes both barriers: no bank link required, and AI that speaks to you like a mentor, not a machine.

---

## Why Vera?

Vera means truth. That is exactly what it gives you about your money.

---

## Contributors

| Name | Role |
|------|------|
| [Your Name] | Product, AI integration |
| [Teammate 2] | Frontend (Bolt) |
| [Teammate 3] | Design, demo |

*Built at the Accelerator Hackathon · May 2026*
