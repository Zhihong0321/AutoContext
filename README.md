# Auto-Context v2.0 — The Org-as-Code Framework

## Overview

Auto-Context is a **shared organizational context vault** that AI agents use to understand your organization. Instead of teaching AI about your company every session, it learns once and remembers forever.

**Core Principle:** AI agents are the primary users (99.999% of the time). Humans are initiators.

---

## The Problem

| What Happens Now | What Auto-Context Solves |
|---|---|
| Every session AI starts fresh | AI knows your org context immediately |
| Same questions asked repeatedly | First answer becomes cached forever |
| No accountability for AI decisions | ADR (Agent Decision Record) logs every decision |
| Context gets stale over time | Self-correction loop keeps vault healthy |

---

## Architecture

```
┌──────────────────────────────────────────────────────────────┐
│                      AUTO-CONTEXT CLOUD                       │
│                                                               │
│   ┌────────────────────────────────────────────────────────┐  │
│   │                 MCP Server (Primary)                   │  │
│   │                                                          │  │
│   │   Tools available to AI agents:                         │  │
│   │   ├── vault.get(file)       → get vault files          │  │
│   │   ├── vault.search(query)   → search entire vault      │  │
│   │   ├── queries.lookup(q)     → fast Q&A lookup           │  │
│   │   ├── roster.find(role)     → find who to ask          │  │
│   │   ├── vault.append(file, x) → update vault             │  │
│   │   └── metrics.update(data)  → self-report metrics       │  │
│   │                                                          │  │
│   └─────────────────────────┬──────────────────────────────┘  │
│                             │                                 │
│              GitHub Sync (backup + manual edits)               │
│                             │                                 │
│   ┌─────────────────────────▼──────────────────────────────┐   │
│   │                   THE VAULT (7 Files)                 │   │
│   │                                                          │   │
│   │   ┌───────────┐ ┌───────────┐ ┌───────────┐            │   │
│   │   │  CORE     │ │  ROSTER   │ │  INDEX   │            │   │
│   │   │  .yaml    │ │  .yaml    │ │  .yaml   │            │   │
│   │   │ (org DNA) │ │ (people)  │ │ (files)  │            │   │
│   │   └───────────┘ └───────────┘ └───────────┘            │   │
│   │   ┌───────────┐ ┌───────────┐ ┌───────────┐            │   │
│   │   │  LOGIC   │ │ SCRAPBOOK │ │ QUERIES   │            │   │
│   │   │  .md     │ │   .md     │ │   .md     │            │   │
│   │   │ (decisions)│(raw notes)│(fast cache)│            │   │
│   │   └───────────┘ └───────────┘ └───────────┘            │   │
│   │   ┌───────────┐                                       │   │
│   │   │  METRICS │                                       │   │
│   │   │   .md    │                                       │   │
│   │   │ (health) │                                       │   │
│   │   └───────────┘                                       │   │
│   └──────────────────────────────────────────────────────┘   │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

---

## The 7 Files

### 1. CORE.yaml (The DNA)
Immutable organizational facts.

```yaml
identity:
  org_name: "Your Organization"
  sector: "Solar EPC"
  region: "Malaysia"
  
technology:
  core_stack:
    - "React + Next.js"
    - "Python / FastAPI"
    
context_budget:
  max_tokens_per_task: 4000
  priority_tiers:
    - "ROSTER (who to ask)"
    - "QUERIES (fast answers)"
    - "LOGIC (past decisions)"
    - "CORE (org facts)"
    - "INDEX (deep dive)"

regional_logic:
  tax_codes:
    - "SST 8%"
    - "LHDN compliance"
  energy_regulations:
    - "NEM 3.0"

authority_nodes:
  lead: "@CEO"
  architecture: "@GZ-Hong"
  finance: "@Finance_Lead"
```

---

### 2. ROSTER.yaml (The Human API)
Who the AI can ask when it has gaps.

```yaml
people:
  - id: "GZ-Hong"
    name: "GZ Hong"
    role: "Lead Architect"
    authority_level: 3
    knowledge_hooks:
      - "System architecture"
      - "Technical decisions"
    communication:
      preferred: "WhatsApp"
      handle: "+60xxxxxxxxx"
      
  - id: "Finance_Lead"
    name: "[Name]"
    role: "Finance Lead"
    authority_level: 3
    knowledge_hooks:
      - "Budget limits"
      - "Approval thresholds"
      - "Malaysian tax codes"

query_protocol:
  max_length: "1 sentence"
  style: "Non-spammy, specific"
```

---

### 3. INDEX.yaml (The Shadow Index)
Metadata for big files (PDFs, images) — AI reads this first, not the files.

```yaml
big_files:
  - id: "NEM3-Spec"
    file: "/vault/big-data/NEM3.0_Specification.pdf"
    tags:
      - "solar"
      - "NEM"
      - "Malaysia"
    vision_proxy: |
      "PDF describing Malaysia's Net Energy Metering 3.0.
      Contains: connection requirements, capacity limits
      (max 90kW residential), metering procedures."
    action_triggers:
      - "solar system design"
      - "grid connection"
```

---

### 4. LOGIC.md (The Decision Log)
Single-line entries: "Why" behind each decision.

```markdown
2026-03-28 | Tech Stack | Used SQLite for Android VPS to save RAM | 
  "PostgreSQL too heavy for 512MB VPS. Revisit if traffic > 1000 DAU."

2026-03-15 | Solar | NEM 3.0 max system size = 90kW for residential | 
  "Based on EITDA guidelines. Above 90kW requires commercial metering."

2026-03-10 | Finance | Single claim MYR limit = RM 5,000 | 
  "Finance_Lead confirmed optimal balance between fraud prevention 
  and operational friction."
```

---

### 5. SCRAPBOOK.md (The Intake Buffer)
Raw, unprocessed notes before digestion.

```markdown
### 2026-03-29 — From WhatsApp (GZ-Hong)
"the new server should handle 500 concurrent users easily"
→ Action: Digest into LOGIC.md

### 2026-03-28 — From Email (Finance_Lead)
"RM 5,000 is the single claim limit for now"
→ Action: Update LOGIC.md + QUERIES.md
```

---

### 6. QUERIES.md (Fast Cache)
Recurring Q&A — AI reads this first.

```markdown
Q: What is the single-claim MYR limit?
A: RM 5,000
Source: Finance_Lead (2026-03-28)
Verified: 2026-03-30

Q: What's the max NEM 3.0 system size for residential?
A: 90kW
Source: NEM 3.0 Spec (INDEX.yaml)
Verified: 2026-01-15

Q: Who handles NEM 3.0 applications?
A: Technical team (GZ-Hong) + Finance (budget approval)
Source: ROSTER.yaml
Verified: 2026-03-01
```

---

### 7. METRICS.md (Context Health)
Self-reported vault metrics.

```markdown
token_efficiency:
  avg_tokens_per_task: 2850
  budget_ceiling: 4000
  utilization: "71%"
  
vault_growth:
  queries_served_from_cache: 34
  human_queries_avoided: 28

context_quality:
  accuracy_score: "92%"
  gaps_detected: 2
  gaps_resolved: 2
```

---

## MCP Tools (The AI Interface)

| Tool | Input | Output | Purpose |
|------|-------|--------|---------|
| `vault_get` | `file: "CORE"` | CORE.yaml content | Get org facts |
| `vault_get` | `file: "ROSTER"` | ROSTER.yaml content | Get human directory |
| `vault_get` | `file: "LOGIC"` | LOGIC.md content | Get past decisions |
| `queries_lookup` | `q: "budget limit"` | Filtered Q&A | Fast answer lookup |
| `roster_find` | `role: "finance"` | Person object | Find who to ask |
| `vault_search` | `query: "NEM Malaysia"` | All matching entries | Full vault search |
| `vault_append` | `file: "QUERIES", content: "..."` | Confirmation | Update vault |
| `metrics_update` | `data: {...}` | Confirmation | Self-report |

---

## The AI Lifecycle (Protocols)

### Phase 0: Warm Up (One-Time Onboarding)

AI cannot execute tasks until:
- [ ] Send self-introduction to key ROSTER people
- [ ] Ask Lead 3 baseline questions
- [ ] Map communication "vibes" (24h)

### Phase 1: Cognitive Checkpoint (Every Task)

```
Task given
     │
     ▼
SCAN: Read vault (QUERIES → ROSTER → LOGIC)
     │
     ▼
ASSESS: "What do I lack?"
     │
     ▼ (if gap found)
CONTEXT GAP PROTOCOL:
  1. Check ROSTER for @Owner
  2. Send 1-sentence question
  3. Wait for reply
  4. Update QUERIES.md (so never ask again)
  5. Update LOGIC.md (decision logged)
     │
     ▼
EXECUTE: Run task with full context
     │
     ▼
REPORT: Write to METRICS.md
```

### Phase 2: Digestion (Weekly)

- Process SCRAPBOOK → inject into QUERIES/LOGIC/CORE
- Verify stale entries in METRICS.md
- Archive old SCRAPBOOK entries
- Self-review: "What did I get wrong?"

---

## Token Budget (Context Engineering)

Inspired by Anthropic's context engineering:

```yaml
budget:
  per_task_limit: 4000 tokens
  compaction_trigger: 3500 tokens

priority_order:
  1_tier:
    - ROSTER (always load - tiny)
    - QUERIES (always load - tiny)
  2_tier:
    - LOGIC (load if task-related)
    - CORE (load if sector relevant)
  3_tier:
    - INDEX (only if 1+2 failed)
    - big files (last resort)
```

---

## Governance & Audit

### Agent Decision Records (ADR)

Every significant AI action gets logged:

```markdown
### ADR-2026-03-30-001
- Task: "Design solar claim system for Malaysia NEM 3.0"
- Context used: [CORE, LOGIC, QUERIES, NEM3-Spec]
- Gap detected: "What is the single-claim MYR limit?"
- Gap resolved via: Finance_Lead (WhatsApp)
- Answer: "RM 5,000"
- Decision: "Set limit = RM 5,000 in design"
- Confidence: 95%
- Token spent: 2340/4000
```

### File Permissions

| File | Who Can Edit |
|------|--------------|
| CORE.yaml | Admin only |
| ROSTER.yaml | Admin only |
| INDEX.yaml | AI propose, human approve |
| LOGIC.md | AI append, human review monthly |
| QUERIES.md | AI write (from gap resolutions) |
| SCRAPBOOK.md | AI write, Janitor processes |
| METRICS.md | AI self-report |

---

## Deployment

### Platform
- **Host:** Railway (or any Node.js host)
- **Database:** PostgreSQL (via Railway)
- **Backup:** GitHub (sync)

### No Auth Required (Phase 1)
- Single user (you)
- No access management needed yet
- API key optional for future multi-user

---

## Comparison to Other Solutions

| Solution | Approach | vs Auto-Context |
|----------|----------|-----------------|
| ContextNest | Git for AI context | No active loop |
| ClawVault | Markdown memory | No human-in-loop |
| Letta/Mem0 | AI agent memory | No org context |
| Traditional RAG | Document retrieval | Passive (not active) |
| **Auto-Context** | **Org-as-Code + Active Loop** | **Human-in-loop, self-improving** |

---

## Roadmap

### Phase 1: MVP (Now)
- [ ] MCP Server with 7 tools
- [ ] Skill.md for AI behavior
- [ ] Deploy to Railway
- [ ] Manual vault population

### Phase 2: Polish
- [ ] Cache layer (QUERIES hot in memory)
- [ ] ADR logging
- [ ] Self-correction cron job
- [ ] Web UI for vault management

### Phase 3: Scale
- [ ] Multi-user auth (when ready)
- [ ] WhatsApp/Email integration
- [ ] GitHub sync automation

---

## Contributing

This is your personal organizational context system. Customize the vault files for your organization's specific needs.

---

*Auto-Context v2.0 — Built for AI agents, by AI agents*
*GitHub: https://github.com/Zhihong0321/AutoContext*