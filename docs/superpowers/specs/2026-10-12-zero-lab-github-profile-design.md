# Zero Lab GitHub Organization Profile Design

**Date:** 2026-10-12  
**Lane:** RAZOR  
**Status:** Approved in chat; awaiting written-spec review  
**Artifact:** `profile/README.md`

## Intent

Create Zero Lab's first public GitHub organization profile README. It should give security
practitioners, prospective collaborators, and buyers an immediate, credible understanding of
who Zero Lab is, what it builds, and which public repository they should inspect first.

Trail of Bits is the quality reference: concise positioning, restrained presentation, and
open-source work as proof. Zero Lab will not copy Trail of Bits' wording, layout, or identity.
The finished profile must sound and look like Zero Lab.

## Success Criteria

A first-time visitor should understand within ten seconds:

1. Zero Lab builds practical adversarial AI security tools and research.
2. The work is operator-built and grounded in real security practice.
3. The featured public repositories are useful entry points, not placeholders.
4. The organization has a clear official website and a clear way to engage.

The README should remain readable on desktop and mobile, in GitHub light and dark themes, and
without externally hosted dynamic widgets.

## Direction

Use **restrained authority**: a single strong brand anchor, compact copy, and verifiable public
work. Avoid badge walls, animated typing effects, visitor counters, generic stock imagery,
excessive emoji, and decorative sections that do not help a visitor choose what to read or use.

The voice should be direct, technical, and human. It may carry hacker character, but it must not
read like a brochure or make claims that the public evidence cannot support.

## Information Architecture

The README will use this order:

1. **Brand anchor** — existing canonical Zero Lab logo or wordmark, centered, with useful alt
   text. Prefer a repository-owned asset with transparent background and theme-safe contrast.
2. **Positioning line** — one sentence stating what Zero Lab builds and for whom.
3. **Credibility paragraph** — two or three sentences connecting adversarial AI security,
   security research, and operator-built tooling. Every factual claim must be supported by public
   material or an approved canonical Zero Lab source.
4. **Open-source work** — a compact table or short list of public, ready repositories. Each entry
   includes its name, one-sentence purpose, and direct repository link. No private, unreleased,
   placeholder, or aspirational project appears.
5. **Focus areas** — a short list covering only active public work, expected to include agentic
   system security, RAG and data-layer security, offensive AI research, and reusable security
   workflows or skills where public repositories substantiate them.
6. **Engagement links** — official website plus any verified public research/content and
   contribution or security-reporting paths that actually exist.
7. **Closing line** — a brief Zero Lab statement, not a slogan stack or sales CTA.

## Content and Evidence Rules

- Public GitHub repositories and canonical Zero Lab records are evidence sources.
- Do not publish confidential frameworks, internal infrastructure, client details, capability
  claims without public support, or unreleased product roadmaps.
- Do not expose SEED, FT09 tradecraft, private marketplace validation details, or operational
  paths from the Crypt.
- Describe projects by what they currently do, not what they are planned to become.
- If a proposed claim cannot be verified, omit it rather than soften it into vague marketing.
- Preserve product capitalization and official repository names exactly.

## Visual Treatment

- Reuse an existing canonical Zero Lab brand asset if one is suitable; do not invent a new logo.
- Keep the content width and spacing native to GitHub-flavored Markdown.
- Use standard Markdown headings and tables only where they improve scanning.
- Use at most a small, purposeful set of static badges if they communicate meaningful status;
  the default is no badges.
- Avoid raw HTML except for the centered brand image or alignment that Markdown cannot express.
- Store any copied visual asset inside this repository under `profile/assets/` with a descriptive
  filename.

## Repository Selection

Before drafting the project showcase, inspect the live `zero-lab-ai` organization and include
only repositories that are public, active enough to represent the organization, documented, and
useful to an outsider. Prefer three to six entries. The skills marketplace may lead if it is
public and release-ready; otherwise it is omitted until its visibility and readiness change.

Pinned repositories are configured separately in GitHub and are not part of this filesystem
change. The README should complement those pins rather than duplicate all their metadata.

## Files

- `profile/README.md` — public organization-profile content.
- `profile/assets/<brand-asset>` — optional, only if an existing canonical asset is selected.
- No site code, CI, dependencies, or generated output are required.

## Verification

Before completion:

1. Confirm the README is at the GitHub-required `profile/README.md` path.
2. Check every link and repository name against its live public target.
3. Confirm every represented project is public and ready to be featured.
4. Scan the rendered Markdown structure for desktop/mobile readability and light/dark contrast.
5. Scan the final diff for confidential names, internal paths, unsupported claims, and accidental
   references to the Circle's private frameworks.
6. Confirm `git diff --check` is clean.

## Out of Scope

- Creating, publishing, or changing GitHub repositories.
- Pinning repositories or changing organization settings.
- Rebranding Zero Lab or creating a new logo.
- Publishing unreleased projects or internal validation evidence.
- Adding analytics, dynamic widgets, or external tracking.
