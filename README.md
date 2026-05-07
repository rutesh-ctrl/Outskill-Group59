# Clarifin 💸

> **Your money, finally making sense.**
> An AI-powered budget tracker that speaks to you like a mentor — not a spreadsheet.

[![Built with Bolt](https://img.shields.io/badge/Built%20with-Bolt-6C47FF?style=flat-square)](https://bolt.new)
[![Supabase](https://img.shields.io/badge/Backend-Supabase-3ECF8E?style=flat-square)](https://supabase.com)
[![OpenAI](https://img.shields.io/badge/AI-OpenAI%20GPT--4o--mini-412991?style=flat-square)](https://openai.com)
[![Hackathon](https://img.shields.io/badge/Accelerator-Hackathon%202026-F5A623?style=flat-square)](#)

---

## What is Clarifin?

Most people have a vague, anxious relationship with their money. Their banking app shows every transaction — but gives zero interpretation. No categories. No patterns. No "here's what to do about it."

**Clarifin closes the gap between data and decision.**

Type an expense the way you'd say it out loud — *"grabbed a coffee, £4.50"* — and Clarifin's AI instantly categorises it, flags whether it was essential or avoidable, and updates your dashboard. Once a day, it delivers a plain-English summary in the voice of an encouraging financial mentor: honest, direct, and always ending with one clear action you can take.

No forms. No bank sync required. No spreadsheets. Just clarity.

---

## Features

### Core (MVP)
- **Natural language expense entry** — type expenses exactly how you'd say them; AI parses amount, category, and date automatically
- **AI auto-categorisation** — every expense instantly assigned to one of 8 categories (Food & Drink, Transport, Shopping, Entertainment, Health, Subscriptions, Bills, Other)
- **Essential vs. avoidable tagging** — AI flags each expense so you can see what's truly discretionary
- **Spending dashboard** — real-time weekly and monthly view with category breakdown chart
- **AI mentor summary** — a daily plain-English insight card inspired by the tone of Suze Orman: warm, direct, and actionable
- **Global currency support** — 15 currencies at launch (USD, GBP, EUR, JPY, INR, CAD, AUD, BRL, ZAR, AED, SGD, CHF, MXN, KRW, NGN) with locale-correct formatting via `Intl.NumberFormat`
- **Secure auth** — email login powered by Supabase Auth; your data persists across sessions

### Coming Soon
- Monthly budget caps per category
- Recurring subscription detection
- Spending streaks and habit nudges
- CSV export
- Spanish, French, and Portuguese UI

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | [Bolt](https://bolt.new) |
| Backend & Auth | [Supabase](https://supabase.com) (PostgreSQL + Auth) |
| AI | [OpenAI GPT-4o-mini](https://openai.com) |
| Currency formatting | Native `Intl.NumberFormat` API |
| Hosting | Supabase Edge Functions + Bolt deploy |

---

## Getting Started

### Prerequisites

- Node.js 18+
- A [Supabase](https://supabase.com) account (free tier works)
- An [OpenAI](https://platform.openai.com) API key

### 1. Clone the repository

```bash
git clone https://github.com/your-org/clarifin.git
cd clarifin
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up environment variables

Create a `.env` file in the project root:

```env
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
OPENAI_API_KEY=your_openai_api_key
```

### 4. Set up the Supabase database

Run the following SQL in your Supabase SQL editor to create the required tables:

```sql
-- User profiles (extends Supabase Auth)
create table user_profiles (
  id uuid references auth.users on delete cascade primary key,
  currency_code text not null default 'GBP',
  currency_symbol text not null default '£',
  created_at timestamptz default now()
);

-- Expenses
create table expenses (
  id uuid primary key default gen_random_uuid(),
  user_id uuid references auth.users on delete cascade not null,
  amount numeric(14,2) not null,
  currency_code text not null,
  description text not null,
  category text not null,
  is_essential boolean default true,
  raw_input text,
  ai_confidence numeric(3,2),
  expense_date date not null default current_date,
  created_at timestamptz default now()
);

-- AI mentor summaries (cached daily)
create table ai_summaries (
  id uuid primary key default gen_random_uuid(),
  user_id uuid references auth.users on delete cascade not null,
  summary_text text not null,
  generated_at timestamptz default now(),
  week_start date not null
);

-- Row-level security
alter table user_profiles enable row level security;
alter table expenses enable row level security;
alter table ai_summaries enable row level security;

create policy "Users can manage their own profile" on user_profiles
  for all using (auth.uid() = id);

create policy "Users can manage their own expenses" on expenses
  for all using (auth.uid() = user_id);

create policy "Users can manage their own summaries" on ai_summaries
  for all using (auth.uid() = user_id);
```

### 5. Start the development server

```bash
npm run dev
```

Visit `http://localhost:5173` to see Clarifin running locally.

---

## Project Structure

```
clarifin/
├── src/
│   ├── components/
│   │   ├── ExpenseInput.jsx       # Natural language entry field
│   │   ├── ConfirmationCard.jsx   # AI parse review before saving
│   │   ├── Dashboard.jsx          # Main spending overview
│   │   ├── CategoryChart.jsx      # Donut / bar breakdown chart
│   │   ├── MentorSummary.jsx      # AI insight card
│   │   └── CurrencySelector.jsx   # Onboarding currency picker
│   ├── lib/
│   │   ├── supabase.js            # Supabase client
│   │   ├── openai.js              # AI parsing + summary calls
│   │   └── formatCurrency.js      # Intl.NumberFormat wrapper
│   ├── pages/
│   │   ├── Onboarding.jsx         # First-run currency selection
│   │   ├── Home.jsx               # Dashboard + entry
│   │   └── Auth.jsx               # Login / sign up
│   └── main.jsx
├── .env.example
├── package.json
├── README.md
└── phase1-ideation.md             # Hackathon ideation document
```

---

## Hackathon Goals

Built in 3 days at the **Accelerator Hackathon, May 2026**.

**The must-have flow:**
> User signs up → selects currency → types an expense in plain English → AI categorises it and tags it essential/avoidable → user confirms → dashboard updates with category chart and AI mentor summary.

**Definition of done for the demo:**
> A judge types one expense, sees it categorised instantly, and reads an AI insight that feels like genuine financial advice — all within 30 seconds of landing on the app.

**Judging criteria we're targeting:**
- Strength of the problem and pain point articulation
- Creativity of the AI integration (not bolted on — structurally essential)
- Quality of the demo story and live flow

---

## The Problem We're Solving

> *Financially anxious adults have the data — their bank shows every transaction — but not the meaning. No tool translates spending patterns into a clear, trustworthy, human-toned signal that tells them what to actually do next. The result is avoidance: they don't track, don't improve, and stay anxious. Clarifin closes the gap between data and decision with AI that speaks like a mentor, not a machine.*

---

## Contributors

| Name | Role |
|------|------|
| [Your Name] | Product, AI integration |
| [Teammate 2] | Frontend (Bolt) |
| [Teammate 3] | Backend (Supabase) |
| [Teammate 4] | Design, demo |

*Built at the Accelerator Hackathon · May 2026*

---

## Licence

MIT — free to use, fork, and build on.

---

<p align="center">
  Made with focus and too much coffee ☕ · Accelerator Hackathon 2026
</p>
