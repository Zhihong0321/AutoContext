# Auto-Context v2.0 — The Org-as-Code Framework
## Improved White Paper — AI Research Draft

---

## PART 0: THE PAIN (Why This Exists)

### The Enterprise AI Problem

```
Current State:
LLMs have PhD-level reasoning but operate in a vacuum.
They get deployed and "misfire" because they lack the Private Context.

The result: "AI that knows everything, understands nothing about your business."

Current "Solutions":
❌ RAG → "Document Junk" — dumps PDFs, clogs context window
❌ Fine-tuning → Expensive, slow, stale quickly
❌ Manual prompting → Not scalable, human-dependent

What we actually need:
A system where AI can "learn" the organization's context
like a new employee does — systematically, persistently, actively.
```

### The Research Finding

In researching similar projects (ContextNest, ClawVault, Personal Vault, Letta, Mem0), one pattern emerged:

> **The best AI memory systems don't just store context — they structure it for retrieval, enforce governance on it, and let the AI actively grow it.**

Auto-Context v2.0 is the organizational implementation of this pattern.

---

## PART 1: THE WHY (Updated)

### The Core Problem Statement

> "An AI without organizational context is like a new employee given a degree but no onboarding — technically capable, practically lost."

### What's Different About Auto-Context v2.0

| Old Approach | Auto-Context v2.0 |
|---|---|
| Static document dump | Living context vault with active updates |
| Passive retrieval | Active self-enrichment (AI asks humans) |
| Document junk | Digest & Archive protocol — minimal active memory |
| Generic context | Org-specific logic (e.g., Malaysian NEM 3.0) |
| No feedback loop | Self-correction loop — AI reviews its own context quality |

---

## PART 2: THE ARCHITECTURE

### Overall System Design

```
┌─────────────────────────────────────────────────────────────────────┐
│                    AUTO-CONTEXT v2.0 ARCHITECTURE                   │
│                                                                     │
│  ┌──────────────────────────────────────────────────────────────┐ │
│  │                    THE VAULT (Git-Backed)                     │ │
│  │                                                               │ │
│  │   ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌────┐ │ │
│  │   │ CORE    │  │ ROSTER  │  │ INDEX   │  │ LOGIC   │  │ SCR│ │ │
│  │   │ .yaml   │  │ .yaml   │  │ .yaml   │  │ .md     │  │ .md│ │ │
│  │   │ DNA     │  │ Human   │  │ Shadow  │  │ Decision│  │ Int│ │ │
│  │   │         │  │ API     │  │ Index   │  │ Log     │  │    │ │ │
│  │   └────┬────┘  └────┬────┘  └────┬────┘  └────┬────┘  └──┬─┘ │ │
│  │        └───────────┴───────────┴───────────┴──────────┘     │ │
│  │                         │                                  │ │
│  │              ┌──────────▼──────────┐                       │ │
│  │              │   QUERIES.md        │  ← NEW: Fast Q&A cache │ │
│  │              │   METRICS.md        │  ← NEW: Context scores │ │
│  │              └─────────────────────┘                       │ │
│  └──────────────────────────────────────────────────────────────┘ │
│                              ↑                                    │
│                    AI Agent ↕ Vault Cycle                         │
│                              ↓                                    │
│  ┌──────────────────────────────────────────────────────────────┐ │
│  │               THE AI AGENT LIFECYCLE                         │ │
│  │                                                               │ │
│  │  Phase 0: Warm Up  →  Phase 1: Task  →  Phase 2: Digest      │ │
│  │     (Onboarding)      (Checkpoint)      (Maintenance)         │ │
│  │                                                               │ │
│  │  ┌─────────────────────────────────────────────────────┐    │ │
│  │  │       CONTEXT GAP PROTOCOL (Active Loop)              │    │ │
│  │  │                                                       │    │ │
│  │  │  gap detected → ROSTER lookup → ping @Owner →        │    │ │
│  │  │  reply → LOGIC update → resume task                  │    │ │
│  │  └─────────────────────────────────────────────────────┘    │ │
│  └──────────────────────────────────────────────────────────────┘ │
│                              ↑                                    │
│                    MCP Server (Model Context Protocol)             │
└─────────────────────────────────────────────────────────────────────┘
```

---

## PART 3: THE 7-FILE VAULT (Updated)

### File Inventory

```
/vault/
├── CORE.yaml         DNA — Immutable organizational facts
├── ROSTER.yaml       Human API — Who's who, roles, authority
├── INDEX.yaml        Shadow Index — Metadata for big files
├── LOGIC.md          Decision Log — "Why" behind choices
├── SCRAPBOOK.md       Intake Buffer — Raw intake before digestion
├── QUERIES.md        [NEW] Fast Cache — Recurring Q&A, instant lookup
└── METRICS.md        [NEW] Context Scores — Vault health, token usage
```

### Detailed Specifications

---

#### FILE 1: CORE.yaml (The DNA)

```yaml
# Auto-Context CORE — Immutable Organizational Facts
# Version: 1.0 | Last Updated: 2026-03-30

identity:
  org_name: "Your Organization"
  sector: "Solar EPC"
  region: "Malaysia"
  fiscal_year: "Jan-Dec"

technology:
  core_stack:
    - "React + Next.js"
    - "Python / FastAPI"
    - "PostgreSQL"
  ai_platforms:
    - model: "MiniMax"
      role: "Primary reasoning agent"
    - model: "Claude"
      role: "Fallback / compliance review"

context_budget:
  max_tokens_per_task: 4000
  priority_tiers:
    - "ROSTER (who to ask)"
    - "QUERIES (fast answers)"
    - "LOGIC (past decisions)"
    - "CORE (org facts)"
    - "INDEX (deep dive only if needed)"
  compaction_trigger: 3500

regional_logic:
  tax_codes:
    - "SST 8%"
    - "LHDN compliance required"
  energy_regulations:
    - "NEM 3.0 (Net Energy Metering)"
    - "FiT rates: RM 1.42/kWh solar"

authority_nodes:
  lead: "@CEO_Name"
  architecture: "@GZ-Hong"
  finance: "@Finance_Lead"
  technical: "@Tech_Lead"

governance:
  retention_policy:
    raw_intake_days: 7
    decision_log_years: 5
  audit_level: "full"
  auto_compaction: true
```

---

#### FILE 2: ROSTER.yaml (The Human API)

```yaml
# Auto-Context ROSTER — Human Directory & Knowledge Hooks

people:
  - id: "GZ-Hong"
    name: "GZ Hong"
    role: "Lead Architect"
    authority_level: 3
    knowledge_hooks:
      - "System architecture"
      - "Technical decisions"
      - "Code review"
    communication:
      preferred: "WhatsApp"
      handle: "+60xxxxxxxxx"
    timezone: "Asia/Kuala_Lumpur"
    active: true

  - id: "Finance_Lead"
    name: "[Name]"
    role: "Finance Lead"
    authority_level: 3
    knowledge_hooks:
      - "Budget limits"
      - "Approval thresholds"
      - "Malaysian tax codes"
    communication:
      preferred: "Email"
      handle: "finance@company.com"
    timezone: "Asia/Kuala_Lumpur"
    active: true

  - id: "Legal_Lead"
    name: "[Name]"
    role: "Legal / Compliance"
    authority_level: 2
    knowledge_hooks:
      - "Contract law"
      - "LHDN compliance"
      - "NEM 3.0 regulations"
    communication:
      preferred: "Email"
      handle: "legal@company.com"
    timezone: "Asia/Kuala_Lumpur"
    active: true

communication_channels:
  whatsapp_business:
    api_endpoint: "https://api.whatsapp.example.com/send"
    enabled: true
  email:
    smtp_server: "smtp.company.com"
    enabled: true

query_protocol:
  max_length: "1 sentence"
  style: "Non-spammy, specific, actionable"
  escalation_trigger: "no response in 24h"
```

---

#### FILE 3: INDEX.yaml (The Shadow Index)

```yaml
# Auto-Context INDEX — Metadata for Big Files (PDFs, Images)

version_control:
  enabled: true
  git_remote: "org/context-vault"
  auto_commit: true
  commit_template: "AI_context_update: {date} | {action}"

big_files:
  - id: "NEM3-Spec"
    file: "/vault/big-data/NEM3.0_Specification.pdf"
    tags:
      - "solar"
      - "NEM"
      - "energy regulation"
      - "Malaysia"
    vision_proxy: |
      "PDF describing Malaysia's Net Energy Metering 3.0 program.
      Contains: connection requirements, capacity limits (max 90kW residential),
      metering procedures, grid interconnection standards.
      Last updated: 2024."
    action_triggers:
      - "solar system design"
      - "grid connection"
      - "NEM application"
    last_verified: "2026-01-15"

  - id: "Fraud-Detection-Spec"
    file: "/vault/big-data/Fraud_Detection_Spec.pdf"
    tags:
      - "finance"
      - "claims"
      - "fraud prevention"
      - "MYR limits"
    vision_proxy: |
      "Financial fraud detection system specification.
      Contains: transaction monitoring rules, alert thresholds,
      single-claim MYR limit (RM 5,000).
      Last updated: 2025-11."
    action_triggers:
      - "claims processing"
      - "financial approval"
      - "fraud review"
    last_verified: "2026-01-15"

on_demand_pull:
  rule: "search_index_first_then_open_file"
  max_file_opens_per_task: 2
```

---

#### FILE 4: LOGIC.md (The Decision Log)

```markdown
# Auto-Context LOGIC — Decision Log
# Single-line entries: "Why" behind each decision
# Format: YYYY-MM-DD | Category | Decision | Reason

## Recent Decisions

2026-03-28 | Tech Stack | Used SQLite for Android VPS to save RAM | 
  "PostgreSQL too heavy for 512MB VPS. SQLite handles concurrent 
  reads fine for our use case. Revisit if traffic > 1000 DAU."

2026-03-15 | Solar | NEM 3.0 max system size = 90kW for residential | 
  "Based on EITDA guidelines. Above 90kW requires commercial-grade 
  metering and different approval process."

2026-03-10 | Finance | Single claim MYR limit = RM 5,000 | 
  "Finance_Lead confirmed RM 5,000 is optimal balance between 
  fraud prevention and operational friction."

2026-02-20 | Architecture | Chose Next.js over plain React | 
  "Need server-side for SEO and API routes. Next.js App Router gives 
  both with minimal overhead. GZ-Hong approved."

2026-01-15 | Compliance | LHDN e-invoice mandatory from Aug 2026 | 
  "Per LHDN Directive 2024. All billing systems must generate 
  e-invoices via myInvois portal starting Aug 1, 2026."

## Archived older decisions → /vault/HISTORY/
```

---

#### FILE 5: SCRAPBOOK.md (The Intake Buffer)

```markdown
# Auto-Context SCRAPBOOK — Raw Intake Buffer
# AI dumps raw, unprocessed information here before digestion
# Janitor process runs periodically to digest into other files
# Auto-archives after 7 days if not processed

## Recent Intake

### 2026-03-29 — From WhatsApp (GZ-Hong)
"the new server should handle 500 concurrent users easily, 
don't need to over-engineer it — keep it simple"
→ Action: Digest into TECH.md? or note under infrastructure LOGIC

### 2026-03-28 — From Email (Finance_Lead)
"RM 5,000 is the single claim limit for now, 
we can review after Q2 if fraud rate stays below 0.5%"
→ Action: Update LOGIC.md | Update QUERIES.md

### 2026-03-27 — From Meeting (CEO)
"next year we want to expand to Indonesia, 
Malaysia first though — get站稳 first"
→ Action: Note in CORE.yaml regional_expansion | Update LOGIC.md

---
## Digest Log (Janitor process records what it processed)

2026-03-29 | Processed GZ-Hong WhatsApp → TECH.md
2026-03-28 | Processed Finance_Lead email → LOGIC.md + QUERIES.md
2026-03-27 | Processed CEO meeting note → CORE.yaml (regional_logic)
2026-03-26 | Old intake from 2026-03-19 → Archived to /HISTORY/2026-03/
```

---

#### FILE 6: QUERIES.md (NEW — Fast Cache)

```markdown
# Auto-Context QUERIES — Fast Answer Cache
# Recurring questions and confirmed answers
# AI reads this first before asking humans

## Finance & Approvals

Q: What is the single-claim MYR limit?
A: RM 5,000
Source: Finance_Lead (2026-03-28)
Verified: 2026-03-30

Q: Who approves claims above RM 5,000?
A: Finance_Lead (authority_level: 3)
Source: ROSTER.yaml
Verified: 2026-03-30

Q: What's the budget for solar installation per kW?
A: RM 5,000 - RM 7,000 depending on system size
Source: Finance_Lead meeting 2026-02
Verified: 2026-03-15

## Technical

Q: What's the max NEM 3.0 system size for residential?
A: 90kW (requires single-phase or three-phase connection)
Source: NEM 3.0 Spec (INDEX.yaml)
Verified: 2026-01-15

Q: What's the current server capacity?
A: Handles 500 concurrent users comfortably
Source: GZ-Hong (WhatsApp 2026-03-29)
Verified: 2026-03-30

## Compliance

Q: When does LHDN e-invoice become mandatory?
A: August 1, 2026
Source: Legal_Lead email 2026-02-20
Verified: 2026-03-01

Q: What's the data retention requirement?
A: 7 years for customer records (LHDN requirement)
Source: Compliance briefing 2025-10
Verified: 2026-01-01

## People

Q: Who is the technical lead?
A: GZ-Hong (architecture decisions)
Source: ROSTER.yaml
Verified: 2026-01-01

Q: Who handles NEM 3.0 applications?
A: Technical team (GZ-Hong) + Finance (budget approval)
Source: Org meeting 2026-01
Verified: 2026-03-01
```

---

#### FILE 7: METRICS.md (NEW — Context Health)

```markdown
# Auto-Context METRICS — Vault Health & Context Efficiency

## Context Performance

last_updated: 2026-03-30

token_efficiency:
  avg_tokens_per_task: 2850
  budget_ceiling: 4000
  utilization: "71%"
  compaction_count: 1
  compaction_trigger: 3500

vault_growth:
  total_files: 7
  entries_added_this_week: 12
  queries_served_from_cache: 34
  human_queries_avoided: 28

context_quality:
  accuracy_score: "92%"
  staleness_check: "OK"
  gaps_detected: 2
  gaps_resolved: 2

onboarding_status:
  ai_onboarded: true
  warm_up_completed: "2026-03-28"
  baseline_questions_answered: 3/3
  communication_vibes_mapped: "OK"

## Digest & Archive Stats

scrapbook_items_processed: 8
scrapbook_items_archived: 3
old_entries_moved_to_history: 12
vacuum_run: "2026-03-29"

## Alert Flags

⚠️ staleness: LOGIC.md entry from 2025-10 — needs verification
✅ all_clear: CORE.yaml verified 2026-03
```

---

## PART 4: THE AI LIFECYCLE (Updated)

### Phase 0: The Warm Up (Mandatory Onboarding)

```
┌─────────────────────────────────────────────────────────────┐
│              PHASE 0: WARM UP — CHECKLIST                   │
│         AI cannot execute tasks until all ✓ complete        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  □ Step 0.1: Self-Introduction                             │
│     → Send brief greeting to key ROSTER people             │
│     → Format: "Hi @Name, I'm [AI Name], I'll be helping  │
│        with [role]. I'll ask questions when I need context."│
│                                                             │
│  □ Step 0.2: Baseline Alignment (exactly 3 questions)      │
│     → Ask Lead: "What are the top 3 things I should know   │
│        about [org] that aren't in the vault?"              │
│                                                             │
│  □ Step 0.3: Silent Observation (24h minimum)              │
│     → Map communication style and terminology              │
│     → Note in SCRAPBOOK: "vibes observed"                  │
│                                                             │
│  ⏱️ Gate: Phase 1 only unlocks after all 3 complete        │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Phase 1: The Cognitive Checkpoint (Every Task)

```
┌─────────────────────────────────────────────────────────────┐
│           PHASE 1: COGNITIVE CHECKPOINT — PRE-FLIGHT        │
│                                                             │
│  Every task runs this before execution:                    │
│                                                             │
│  1. SCAN: Read vault for constraints                        │
│     → CORE.yaml (facts, rules)                             │
│     → QUERIES.md (fast answers)                            │
│                                                             │
│  2. ASSESS: "What info do I lack?"                          │
│     → Check LOGIC.md for past decisions                    │
│     → If still missing → ROSTER lookup for @Owner           │
│                                                             │
│  3. THE CONTEXT GAP PROTOCOL (if gap found):                │
│     ┌─────────────────────────────────────────────────┐   │
│     │  gap detected → check ROSTER → ping @Owner      │   │
│     │  "Hi @Owner, quick question: [1 sentence]"      │   │
│     │  wait → reply → update QUERIES.md + LOGIC.md    │   │
│     │  resume task                                   │   │
│     └─────────────────────────────────────────────────┘   │
│                                                             │
│  4. EXECUTE: Run task with full context                     │
│                                                             │
│  5. REPORT: Write metrics to METRICS.md                     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Phase 2: The Digestion (Weekly Maintenance)

```
┌─────────────────────────────────────────────────────────────┐
│              PHASE 2: DIGESTION — JANITOR PROTOCOL           │
│                      Runs weekly (auto)                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. EXTRACT: SCRAPBOOK.md → process raw notes              │
│     → Key-value rules → inject into QUERIES.md             │
│     → Decisions → inject into LOGIC.md                    │
│     → New org facts → inject into CORE.yaml               │
│                                                             │
│  2. VERIFY: Check METRICS.md alert flags                    │
│     → Any files not verified in 90 days? → flag           │
│     → Stale entries → ping @Owner for re-verification      │
│                                                             │
│  3. ARCHIVE: Move old SCRAPBOOK to /HISTORY/                │
│     → Delete SCRAPBOOK entries older than 7 days          │
│                                                             │
│  4. VACUUM: Clean up /HISTORY/ (keep last 90 days only)   │
│                                                             │
│  5. SELF-REVIEW: AI reviews own context quality            │
│     → "What did I get wrong this week?" → update LOGIC    │
│     → "What should I have known?" → create new QUERIES     │
│     → "What's changing in the org?" → check with ROSTER   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## PART 5: THE CONTEXT GAP PROTOCOL (Core Differentiator)

This is what makes Auto-Context "active" vs passive RAG:

```
┌─────────────────────────────────────────────────────────────────┐
│              THE CONTEXT GAP PROTOCOL — ACTIVE LOOP              │
│                                                                 │
│   ┌───────────┐                                                 │
│   │ Task given │                                                │
│   └─────┬─────┘                                                 │
│         ↓                                                       │
│   ┌─────────────────────────────────────────┐                  │
│   │ Step 1: SCAN vault                       │                  │
│   └─────┬───────────────────────────────────┘                  │
│         ↓                                                       │
│   ┌─────────────────────────────────────────┐                  │
│   │ Step 2: ASSESS — "Do I know this?"        │                  │
│   │                                                         │  │
│   │   IF know enough → proceed to execute     │                  │
│   │   IF gap found → go to Step 3             │                  │
│   └─────┬───────────────────────────────────┘                  │
│         ↓                                                       │
│   ┌─────────────────────────────────────────┐                  │
│   │ Step 3: ROUTE to human                   │                  │
│   │                                                         │  │
│   │   - Check ROSTER.yaml for @Owner        │                  │
│   │   - Format: 1-sentence question          │                  │
│   │   - Use preferred channel (WhatsApp)    │                  │
│   └─────┬───────────────────────────────────┘                  │
│         ↓                                                       │
│   ┌─────────────────────────────────────────┐                  │
│   │ Step 4: UPDATE vault                     │                  │
│   │                                                         │  │
│   │   Human replies → AI captures answer    │                  │
│   │   → Update QUERIES.md (fast cache)       │                  │
│   │   → Update LOGIC.md (decision log)       │                  │
│   │   → Update METRICS.md (gap resolved)     │                  │
│   └─────┬───────────────────────────────────┘                  │
│         ↓                                                       │
│   ┌─────────────────────────────────────────┐                  │
│   │ Step 5: RESUME task                      │                  │
│   │                                                         │  │
│   │   Now with full context → execute         │                  │
│   │   AND: now AI knows this for ALL future   │                  │
│   └─────────────────────────────────────────┘                  │
│                                                                 │
│   KEY RULE: Never guess. Always ask. Document the answer.       │
└─────────────────────────────────────────────────────────────────┘
```

---

## PART 6: TOKEN BUDGET SYSTEM

### Inspired by Anthropic's Context Engineering

```yaml
# AUTO-CONTEXT TOKEN BUDGET

budget_rules:
  per_task_limit: 4000 tokens
  compaction_threshold: 3500 tokens

priority_order:
  1_tier:
    - ROSTER (who to ask)          # Always load — tiny file
    - QUERIES (fast answers)        # Always load — tiny file
  2_tier:
    - LOGIC (decisions)            # Load if task-related
    - CORE (org facts)              # Load if sector/region relevant
  3_tier:
    - INDEX (deep dive)             # Only if 1+2 failed to answer
    - big files (PDFs, images)      # LAST resort — expensive

compaction_strategy:
  method: "summarize_and_restart"
  trigger_tokens: 3500

efficiency_targets:
  avg_utilization: "< 75%"
  cache_hit_rate: "> 60%"
  human_query_rate: "< 10%"
```

---

## PART 7: GOVERNANCE & AUDIT

### Decision Traces & Agent Decision Records (ADR)

```markdown
### ADR-2026-03-30-001
- Timestamp: 2026-03-30 14:05
- Task: "Design solar claim system for Malaysia NEM 3.0"
- Context used: [CORE.yaml, LOGIC.md, QUERIES.md, NEM3-Spec (INDEX)]
- Gap detected: "What is the single-claim MYR limit?"
- Gap resolved via: Finance_Lead (WhatsApp)
- Answer: "RM 5,000"
- Decision made: "Set single-claim limit = RM 5,000 in design"
- Confidence: 95%
- Token spent: 2340 / 4000 budget

### ADR-2026-03-30-002
- Timestamp: 2026-03-30 14:22
- Task: "Verify NEM 3.0 residential capacity"
- Context used: [CORE.yaml, INDEX.yaml (NEM3-Spec)]
- Gap detected: None — found answer in INDEX
- Decision made: "Max residential = 90kW"
- Confidence: 98%
- Token spent: 1890 / 4000 budget
```

### Governance Rules

```yaml
governance:
  file_permissions:
    CORE.yaml: "Admin only (senior human)"
    ROSTER.yaml: "Admin only (HR/IT)"
    INDEX.yaml: "AI can propose, human approves"
    LOGIC.md: "AI can append, human reviews monthly"
    SCRAPBOOK.md: "AI writes, Janitor processes"
    QUERIES.md: "AI writes (from gap resolutions)"
    METRICS.md: "AI writes (self-reported)"

  audit:
    enabled: true
    retention_years: 5
    trace_format: "ADR (Agent Decision Record)"
    
  compliance:
    ai_actions_logged: true
    human_approval_required_above: "authority_level_2"
    data_retention_days: 2555    # ~7 years
```

---

## PART 8: MCP INTEGRATION

### How Auto-Context connects to AI via MCP

```
┌─────────────────────────────────────────────────────────────┐
│              MCP INTEGRATION — HOW AI ACCESSES VAULT         │
│                                                             │
│   AI Agent                                                  │
│      │                                                       │
│      │ MCP Client (inside AI)                               │
│      ↓                                                       │
│   ┌─────────────────────────────────────────────────────┐  │
│   │              MCP Server (Auto-Context)                │  │
│   │                                                       │  │
│   │  Tools available:                                     │  │
│   │  vault_status()     → Returns vault health metrics    │  │
│   │  vault_get(file)    → Returns file content            │  │
│   │  vault_list()       → Lists all vault files           │  │
│   │  vault_append(file, content) → Appends to file         │  │
│   │  vault_search(query)→ Searches all files              │  │
│   │  roster_find(role)  → Finds person by role             │  │
│   │  queries_lookup(q)  → Fast Q&A lookup                  │  │
│   │  metrics_update(data) → Updates METRICS.md            │  │
│   └─────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

---

## PART 9: THE SELF-CORRECTION LOOP

```
┌─────────────────────────────────────────────────────────────┐
│              THE SELF-CORRECTION LOOP                        │
│         AI reviews its own context quality weekly            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Every Friday (auto-triggered):                            │
│                                                             │
│  1. GAPS REVIEW: "Which gaps did I hit this week?"          │
│     → Were they in QUERIES? No → add them                   │
│     → Were answers wrong? Yes → correct them                │
│                                                             │
│  2. STALENESS CHECK: "Which files haven't been verified?"   │
│     → Flag entries older than 90 days                       │
│     → Send reminder to @Owner for re-verification           │
│                                                             │
│  3. EFFICIENCY REVIEW: "Was my token usage optimal?"         │
│     → Did I open big files when INDEX was enough?           │
│     → Note in METRICS.md for next week                      │
│                                                             │
│  4. NEW KNOWLEDGE: "What did I learn not in vault?"        │
│     → Append to SCRAPBOOK for janitor to process            │
│                                                             │
│  5. SELF-GRADE: "Did I follow the rules?"                   │
│     → Did I ask before guessing?                           │
│     → Did I update QUERIES after asking?                   │
│     → Did I log ADRs for major decisions?                   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## PART 10: COMPARISON TO EXISTING SOLUTIONS

| Framework | What It Is | vs Auto-Context |
|---|---|---|
| **ContextNest** | Git for AI context | Similar vision, but no active loop |
| **ClawVault** | Markdown memory for AI | Similar file approach, no human-in-loop |
| **Personal Vault** | Encrypted personal context | Encryption focus, single-user |
| **Letta/Mem0** | AI agent memory systems | No human-in-loop, no org context |
| **Traditional RAG** | Document retrieval | Passive, no active enrichment |
| **Auto-Context** | Org-as-Code with active loop | Human-in-loop, active self-enrichment, governance |

---

## THE GOLDEN RULES

1. **Few Lines, More Clarity** — If it can be a tag, don't make it a sentence
2. **Context is Earned** — Never guess. If a gap exists, use ROSTER and ask
3. **Protect the Window** — Search QUERIES first, read INDEX next, open big files last
4. **Self-Manage** — You are the janitor of your own intelligence. Keep the vault clean
5. **Document Everything** — Every answer to a gap becomes a future QUERIES entry
6. **Audit Your Actions** — ADR every significant decision for compliance
7. **Self-Correct Weekly** — The vault degrades without active maintenance

---

*Auto-Context v2.0 — Built on the Karpathy Loop principle applied to organizational knowledge*
*Git-backed, MCP-powered, Human-in-the-loop, Governance-ready*
*Research completed: 2026-03-30 | AI: MiniMax*