[![TrackIQ MCP — connect your AI assistant to Amazon data. 16 tools, full MCP access, $69/mo. Works with Claude, ChatGPT and Cursor.](.github/trackiq-mcp-banner.png)](https://trackiq.com/mcp)

# TrackIQ: Amazon Weekly Executive Report

The Monday client send. A week-over-week Amazon recap that someone who
didn't watch the account all week can read in five minutes and come away
knowing what happened and what happens next.

Built as an [Agent Skill](https://code.claude.com/docs/en/skills). Runs in
Claude Code, Claude web, Claude desktop and ChatGPT from the same folder.

---


---

## Powered by the TrackIQ MCP

These skills read your live Amazon account through the
**[TrackIQ MCP](https://trackiq.com/mcp)** — 16 tools connecting your AI
assistant to Amazon data:

Sales & Traffic · Orders · Inventory · Returns · Sponsored Products · Sponsored
Brands · Sponsored Display · Amazon DSP · AMC Cloud · Keywords · Search Terms ·
Targeting · Search Query Performance · Organic Rank · Best Seller Rank · Buy Box
History · Brand Analytics · Export


Works with Claude, ChatGPT and Cursor. **[Get access →](https://trackiq.com/mcp)**

---

## What you get

One self-contained `.html` email, table-based and inline-styled, that
renders in Outlook and Apple Mail without a build step.

| Section | What it does |
|---|---|
| **Cover strip** | Week range vs. prior week, three KPI tiles: retail, all-in ad spend, all-in TACoS |
| **Executive summary** | A takeaway headline, three numbered lever cards, one decision panel |
| **The scorecard** | Full WoW table, then the channel table — SP/SB/SBV/SD/DSP with share of spend |
| **Pacing** | This week against the brand's own trailing four-week average |
| **Where the money went** | Retail earned per incremental ad dollar, per line, then the full ranked table |
| **Amazon DSP** | One row per programmatic bucket. Self-hides when DSP carries no spend |
| **Demand & search share** | Purchase share vs. impression share, with the search week stated explicitly |
| **Keyword economics** | Brand vs. non-brand, match-type table, proven terms running under potential |
| **Inventory watch** | Days of cover against the account's own thresholds, banded |
| **Actions & closing** | This week's decisions: channel, move, and the one-sentence reason |

Sections with nothing behind them **self-hide** — no placeholder, no "N/A"
table, no apology paragraph. A report that always shows every section
teaches the reader to stop checking whether the data is real.

## Requirements

- The **TrackIQ MCP**, for account overview, product/line performance, ad
  and DSP performance, inventory, keyword and search-query tools
- Nothing else. No filesystem, no shell, no internet.

**Without the MCP connected** the skill asks you to paste this week's and
last week's figures and builds from those. A section whose figures weren't
provided is omitted rather than estimated.

---

## Install

### Claude Code — one command, updates itself

```
/plugin marketplace add TrackIQ-HQ/amazon-seller-skills
/plugin install trackiq-amazon-weekly-executive-report@trackiq
```

### Claude web, desktop, mobile

1. Download the `.zip` from the
   [latest release](https://github.com/TrackIQ-HQ/trackiq-amazon-weekly-executive-report/releases)
2. **Settings → Capabilities → Skills** (code execution must be on)
3. **Create skill → Upload a skill**, choose the `.zip`
4. Toggle it on

### ChatGPT

Same zip. **Plugins → Skills → Create → Upload from your computer.**
Skills are a Business / Enterprise / Edu feature — personal plans can't
upload them yet.

---

## Setup

The skill interviews you once and never asks again.

1. **Brand name** for the eyebrow, and the account line for the footer
2. **Marketplace** — US, UK, DE
3. **Week anchor** — most accounts are Sunday-Saturday
4. **Product lines** — how your ASINs roll up
5. **Inventory bands** — the account's own days-of-cover cutoffs
6. **Delivery** — in-chat, file, Slack, n8n or email

Answers live in `account.md`, copied from
[`assets/account.example.md`](skills/trackiq-amazon-weekly-executive-report/assets/account.example.md).

**Every TrackIQ skill reads the same `account.md`.** If you've already set
up [the daily Snacks email](https://github.com/TrackIQ-HQ/trackiq-amazon-daily-snacks-email),
add the week anchor and inventory bands and you're done.

Point 5 matters more than it looks. Days-of-cover cutoffs are per-account —
a 14-day critical band is right for one brand and badly wrong for another,
and the skill will never assume 21/42 for you.

## Delivery

Where the finished report goes is asked once at setup and stored in
`account.md`. The report is always produced in the chat first; delivery is
the last step.

| Method | What happens | Needs |
|---|---|---|
| **In-chat** | The HTML comes back in the conversation. Default. | nothing |
| **File** | Saved beside the skill, dated. | a filesystem |
| **Slack** | Headline and decisions posted as text, HTML attached as a file. | a connected Slack tool |
| **n8n** | POSTed to your webhook as `text/html`, status reported back. | network access |
| **Email** | Handed to your connected mail tool. | a connected mail tool |

Slack, n8n and email publish outside the chat, so the skill shows you the
channel or recipient and waits for a yes before the first send of a
session. If the configured method isn't available in whatever runtime
you're in, you get the report in-chat with a note saying what was skipped —
it never silently switches to a different outward channel.

## Customizing

| To change | Edit |
|---|---|
| Brand, ASINs, product lines, bands, week anchor | `account.md` — no skill edits |
| Tone and register | `assets/voice.md` |
| Section order, or drop a section | `assets/structure.md` |
| Colors, type scale, geometry | `assets/tokens.md` |
| The methodology and every formula | `assets/build.md` |
| The email shell itself | `assets/template.html` |

Three rules are load-bearing and worth leaving alone.

**Pull both weeks on the same day.** Attribution matures for days after a
week closes, so a prior week pulled last Monday against a current week
pulled today is not a like-for-like comparison.

**Pick sponsored-only or all-in for the headline, once.** A sponsored-only
headline sitting above a channel table that includes DSP contradicts
itself, and a "full-funnel" total that adds DSP on top of an already-all-in
headline double-counts it.

**Marginal return only where spend actually increased.** A line that cut
spend and grew retail has no position on that axis, and a ratio built on a
$50 change is noise wearing a decimal point.

---

## Contributing

```bash
python scripts/validate.py    # must exit 0 before any commit
python scripts/build.py       # writes dist/ zips + registry.json
```

Read [AUTHORING.md](https://github.com/TrackIQ-HQ/amazon-seller-skills/blob/main/AUTHORING.md)
before proposing changes.

## License

MIT. See [LICENSE](LICENSE).
