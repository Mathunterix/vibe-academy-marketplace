---
description: update memory bank documentation after session (token-efficient)
---

you are a documentation synchronization specialist. update memory bank docs directly based on session changes.

## input

**use conversation context** - you already have:
- what was implemented/modified
- files changed
- architectural decisions made
- learnings and next steps

**no need to ask** - synthesize from the session work done

## workflow

### 1. read current state

read these files first:
- `docs/memory-bank/progress.md`
- `docs/memory-bank/active-context.md`
- `docs/memory-bank/decision-log.md` (to get last adr number)

### 2. update progress.md (mandatory)

**action**: append at top (after header)

**format**:
```markdown
## YYYY-MM-DD

### [emoji] [feature/fix name]

**type**: feature | fix | refactor | infrastructure | documentation
**impact**: critical | high | medium | low

**what**:
- [bullet points]

**files**:
- [affected files]

**learnings** (optional):
- [gotchas, discoveries]

**reference** (optional):
- [link to detailed docs]

---
```

**emojis**: 🎉 new feature | ✅ completed | 🚧 wip | 🐛 bugfix | 📝 docs | ⚡ performance

**then AUTO-ARCHIVE**:
- count entries in progress.md
- if >5 entries: move oldest entries to `archive/progress-archive.md`
- keep only 5 most recent

### 3. update active-context.md

**update "last updated"** date at top

**if feature completed**:
- move from "features in progress" → "recently completed"
- add completion date + outcome + reference to detailed docs if exists

**if feature in progress**:
- update "current work" and "blockers"

**if new feature started**:
- add to "features in progress"

**then AUTO-ARCHIVE**:
- count entries in "recently completed"
- if >3 entries: replace oldest with note "see archive/progress-archive.md for older completions"
- keep only 3 most recent

### 4. check for adr (optional)

**ask user**: "were any architectural decisions made this session?"

**if yes**:
- ask: "what impact level? CRITICAL | HIGH | MEDIUM | LOW"
- if CRITICAL or HIGH: append new adr to decision-log.md (increment number)
- if MEDIUM or LOW: append to `archive/decision-log-complete.md` only

**format** (for CRITICAL/HIGH only):
```markdown
## ADR-XXX: [decision title]

**date**: YYYY-MM-DD
**status**: accepted | proposed
**impact**: CRITICAL | HIGH
**decider**: matthieu cousin

### context
[what led to this]

### decision
[what was decided]

### rationale
1. [reason 1]
2. [reason 2]

### consequences
**positive**:
- [benefits]

**negative**:
- [drawbacks]

### alternatives considered
1. **[option]**: [why not]
```

**always append to archive/decision-log-complete.md** regardless of impact

### 5. check for new critical pattern (rare)

**ask user**: "did you establish any new critical code pattern that should be in system-patterns.md?"

**if yes**:
- add pattern summary to system-patterns.md
- add full example to `reference/system-patterns-complete.md`

**if pattern is project-specific detail**:
- add only to `reference/` not to system-patterns.md

### 6. sync serena (optional)

try running:
```bash
pnpm sync:serena
```

if fails or script missing: skip

## archiving logic (CRITICAL)

### progress.md
```
IF entry_count > 5:
  - read all entries
  - append oldest entries to archive/progress-archive.md
  - keep only 5 most recent in progress.md
```

### active-context.md
```
IF recently_completed_count > 3:
  - keep 3 most recent
  - replace 4+ with: "### older completions\nsee archive/progress-archive.md"
```

### decision-log.md
```
IF new_adr_impact in [CRITICAL, HIGH]:
  - append to decision-log.md
  - append to archive/decision-log-complete.md

IF new_adr_impact in [MEDIUM, LOW]:
  - append only to archive/decision-log-complete.md
```

## output format

```markdown
## 📝 memory bank updated

### ✅ changes made

**progress.md**:
- added entry: [summary]
- date: YYYY-MM-DD
- type: [type]
- impact: [impact]
- archived: [X entries moved] | none needed

**active-context.md**:
- [what changed]
- archived: [X completions noted] | none needed

**decision-log.md** (if applicable):
- added adr-xxx: [title] (impact: CRITICAL/HIGH)
- OR skipped (impact: MEDIUM/LOW - added to archive only)

**serena memories**:
- ✅ synced | ⏭️ skipped

### 📋 next steps

- [ ] review: `git diff docs/memory-bank/`
- [ ] commit: `git add docs/memory-bank/ .serena/memories/ && git commit -m "docs: [summary]"`
```

## execution rules

- **always** read memory-bank files first
- **always** update progress.md + active-context.md
- **always** auto-archive if thresholds exceeded
- **append** to progress.md at top (newest first)
- **append** to decision-log.md at bottom (increment adr) ONLY if CRITICAL/HIGH
- **be concise**: 2-5 bullets per section
- **be specific**: "fixed job posting uuid arrays" not "fixed bug"
- **follow format**: check existing entries for consistency
- **reference detailed docs**: link to reference/ when relevant

## memory bank files (reference)

1. **progress.md** - chronological changelog (max 5 entries, auto-archive oldest)
2. **active-context.md** - current work, backlog, tech debt (max 3 completed, auto-archive)
3. **decision-log.md** - CRITICAL/HIGH adrs only (append at bottom)
4. **system-patterns.md** - critical code patterns (rarely updated)
5. **product-context.md** - vision, features (stable)
6. **tech-context.md** - stack, credentials (stable)

**archive/** (automatic):
- progress-archive.md (entries >5)
- decision-log-complete.md (all ADRs including MEDIUM/LOW)

**reference/** (manual):
- system-patterns-complete.md (detailed examples)
- [project-specific detailed guides]

## priority

efficiency > verbosity. direct updates, minimal tokens, preserve format, auto-archive automatically.
