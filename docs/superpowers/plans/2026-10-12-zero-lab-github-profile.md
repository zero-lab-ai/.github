# Zero Lab GitHub Organization Profile Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish a concise, polished Zero Lab organization profile README that establishes the brand, states the lab's public focus, and routes visitors to verified public work.

**Architecture:** The deliverable is a static GitHub-flavored Markdown profile at `profile/README.md`, supported by a small shell verification script. The README uses a typographic wordmark rather than introducing a new or unverified image asset, and every featured project and external claim is tied to a live public source.

**Tech Stack:** GitHub Flavored Markdown, HTML alignment supported by GitHub, POSIX shell, `curl`, `git`

**Spec:** `docs/superpowers/specs/2026-10-12-zero-lab-github-profile-design.md`

## Global Constraints

- Use restrained authority: one brand anchor, compact copy, and verifiable public work.
- Do not use badge walls, animated typing effects, visitor counters, stock imagery, excessive emoji, or decorative sections without navigational value.
- Do not publish confidential frameworks, internal infrastructure, client details, unsupported capability claims, or unreleased roadmaps.
- Do not expose SEED, FT09 tradecraft, private marketplace validation details, or operational paths from the Crypt.
- Do not describe projects beyond their current public behavior.
- The public profile must live at `profile/README.md`.
- Do not add dependencies, generated output, analytics, dynamic widgets, or external tracking.

## Review Focus

- **Private-language leakage:** Internal names or filesystem paths must fail verification; Task 1 tests representative sealed terms and `/Users/` paths.
- **Broken public routes:** The official site and both featured repository URLs must return success; Task 3 checks each target live.
- **Unsupported expansion:** The copy must describe only claims already present on the official site or featured repository READMEs; Task 2 performs a line-by-line provenance review.
- **GitHub profile placement:** A root-level README would not render as the organization profile; Task 1 requires `profile/README.md` exactly.
- **Theme and viewport resilience:** No fixed-width image, color-dependent graphic, or wide feature matrix may be introduced; Task 3 inspects the rendered structure and source constraints.

---

### Task 1: Add the README Verification Gate

**Files:**
- Create: `scripts/check_profile_readme.sh`
- Test: `scripts/check_profile_readme.sh`

**Interfaces:**
- Consumes: the future `profile/README.md` file.
- Produces: `scripts/check_profile_readme.sh`, returning `0` only when the profile path, required public links, required headings, and sealed-content checks pass.

- [ ] **Step 1: Write the failing verification script**

```sh
#!/bin/sh
set -eu

readme="profile/README.md"

if [ ! -f "$readme" ]; then
  echo "FAIL: missing $readme" >&2
  exit 1
fi

require() {
  pattern="$1"
  message="$2"
  if ! grep -Fq "$pattern" "$readme"; then
    echo "FAIL: $message" >&2
    exit 1
  fi
}

require '<h1 align="center">ZERO LAB</h1>' "missing brand anchor"
require '## Open-source work' "missing project showcase"
require '## What we work on' "missing focus areas"
require 'https://zero-lab.ai/' "missing official site"
require 'https://github.com/zero-lab-ai/PatternForge' "missing PatternForge"
require 'https://github.com/itsbroken-ai/RAGdrag' "missing RAGdrag"

if grep -Eiq 'SEED|FT09|Cipher Circle Crypt|NEURF|/Users/|TODO|TBD' "$readme"; then
  echo "FAIL: sealed or placeholder content found" >&2
  exit 1
fi

echo "PASS: profile README structure and sealed-content checks"
```

- [ ] **Step 2: Make the verifier executable**

Run: `chmod +x scripts/check_profile_readme.sh`

- [ ] **Step 3: Run the verifier to confirm the missing artifact fails**

Run: `./scripts/check_profile_readme.sh`

Expected: exit `1` with `FAIL: missing profile/README.md`.

- [ ] **Step 4: Commit the failing verification gate**

```bash
git add scripts/check_profile_readme.sh
git commit -m "test: add organization profile verification"
```

---

### Task 2: Build the Public Organization Profile

**Files:**
- Create: `profile/README.md`
- Test: `scripts/check_profile_readme.sh`

**Interfaces:**
- Consumes: official positioning from `https://zero-lab.ai/`, public project descriptions from the PatternForge and RAGdrag repositories, and Task 1's verification contract.
- Produces: the public GitHub organization profile at `profile/README.md`.

- [ ] **Step 1: Create the profile README with the approved hierarchy and copy**

```markdown
<h1 align="center">ZERO LAB</h1>

<p align="center">
  <strong>Adversarial AI security, built by operators.</strong>
</p>

<p align="center">
  We test the models, applications, and agent systems organizations depend on—and build
  practical tools that help security teams understand the new attack surface.
</p>

<p align="center">
  <a href="https://zero-lab.ai/">Website</a>
  ·
  <a href="https://zero-lab.ai/#contact">Work with us</a>
</p>

---

## Open-source work

| Project | What it does |
| --- | --- |
| [PatternForge](https://github.com/zero-lab-ai/PatternForge) | Pattern-aware password analysis and candidate generation for authorized security testing. |
| [RAGdrag](https://github.com/itsbroken-ai/RAGdrag) | Security assessment tooling for retrieval, generation, and ingestion boundaries in RAG pipelines. |

## What we work on

- **AI red teaming** — adversarial testing of models, applications, and agent systems.
- **Agent and tool security** — trust boundaries, tool abuse, authorization, and failure paths.
- **RAG and data-layer security** — retrieval, ingestion, poisoning, and exposure testing.
- **Security capability development** — practical tools, workflows, and hands-on training.

## Our approach

We came from the offensive side first. We combine real-world security operations with
purpose-built AI tooling, then turn what we learn into clear findings, useful software, and
capability that teams can keep.

---

<p align="center">
  <strong>Build what comes next. Secure it before someone else breaks it.</strong>
</p>
```

- [ ] **Step 2: Run the structural and sealed-content verification**

Run: `./scripts/check_profile_readme.sh`

Expected: exit `0` with `PASS: profile README structure and sealed-content checks`.

- [ ] **Step 3: Perform the provenance review**

Compare the positioning and service language to `https://zero-lab.ai/`, PatternForge's public
README, and RAGdrag's public README. Confirm that:

```text
"models, applications, and agent systems" -> zero-lab.ai AI Security section
"came from the offensive side first" -> zero-lab.ai AI Security section
PatternForge description -> zero-lab-ai/PatternForge public README
RAGdrag description -> itsbroken-ai/RAGdrag public README
```

Expected: each factual statement has a public source; no private validation counts, internal
framework names, customer claims, or future capabilities appear.

- [ ] **Step 4: Commit the profile**

```bash
git add profile/README.md
git commit -m "feat: add Zero Lab organization profile"
```

---

### Task 3: Validate Public Targets and Final Presentation

**Files:**
- Modify: `profile/README.md` only if verification reveals a concrete defect.
- Test: `scripts/check_profile_readme.sh`

**Interfaces:**
- Consumes: Task 2's complete profile and all public URLs embedded in it.
- Produces: a final clean profile diff with verified live links and a recorded validation result.

- [ ] **Step 1: Re-run the local profile gate**

Run: `./scripts/check_profile_readme.sh`

Expected: exit `0`.

- [ ] **Step 2: Verify every public destination**

```bash
curl -L --fail --silent --show-error --output /dev/null https://zero-lab.ai/
curl -L --fail --silent --show-error --output /dev/null https://zero-lab.ai/#contact
curl -L --fail --silent --show-error --output /dev/null https://github.com/zero-lab-ai/PatternForge
curl -L --fail --silent --show-error --output /dev/null https://github.com/itsbroken-ai/RAGdrag
```

Expected: all four commands exit `0`.

- [ ] **Step 3: Inspect layout constraints in source**

Run:

```bash
grep -nE '<img|<picture|width=|shields\.io|visitor|github-readme-stats' profile/README.md
```

Expected: no output. This confirms that no fixed-width visual, theme-sensitive image, badge wall,
visitor counter, or dynamic widget entered the implementation.

- [ ] **Step 4: Run repository-level whitespace and state checks**

Run:

```bash
git diff --check HEAD~1..HEAD
git status --short
```

Expected: `git diff --check` exits `0`; `git status --short` is empty.

- [ ] **Step 5: Record the final verification commit only if Task 3 required a correction**

```bash
git add profile/README.md scripts/check_profile_readme.sh
git commit -m "fix: correct organization profile verification"
```

If Task 3 required no correction, do not create an empty commit.
