---
name: lean-website-kickoff
description: Token-efficient version of the professional website kickoff workflow (brief, research, design plan, build, verify). Use when starting any website project with that master prompt.
---

# Lean Website Kickoff

Same phases and quality bar as the full master prompt, with far less token use. Most of the cost in that workflow comes from a few habits: a context that grows across every phase, screenshots, re-reading repos on every project, and running many reviewers. This skill changes those habits and keeps the rest.

## Token rules (apply in every phase)
1. **Files hold the state, not the chat.** Each phase writes one file (`concepts_brief.md`, `research/DESIGN_RESEARCH.md`, `design_draft.md`). At each check-in, tell the user they can start a fresh chat for the next phase and attach only those files. This is the biggest saving.
2. **Text before images.** Read pages as text (page-text / fetch tools). Take a screenshot only when the visual itself is what you're judging: one hero and one ~390px mobile shot per site at most. Never take full-scroll screenshot series.
3. **Read only part of a file when part will do.** Search, or read with offset and limit, instead of reading whole files. Edit with targeted replacements, never full rewrites.
4. **Load a skill only when its phase starts.** Don't read every SKILL.md up front.
5. **Short updates.** One line per completed step. No recaps of earlier phases. Don't restate files back to the user. Point to the file.
6. **Delegate heavy reading.** When a subagent tool exists, let a subagent read repos or sites and return only a 10–15 line summary of rules. Its raw tool output then never enters the main context.

## Free resources only
Same rule as the master prompt: open source or free tiers with no card, and no trials or premium tiers. Ask before anything paid. Fonts: Google Fonts / Fontshare. Icons: Lucide / Phosphor / Tabler. Media: Unsplash / Pexels / Wikimedia, with credit. 3D: Three.js / R3F with CC0 models. Hosting: free tiers.

## Phase 0 — Tools (ask, don't auto-install)
- Check what's already available: browser tools, subagents, installed design skills. Use the built-in `frontend-design` skill if it's present.
- List any missing tool the user's prompt names (Ego Browser, EGM, Hallmark, etc.) and ask once for permission to install the ones that are actually needed. Don't download or run installers without that permission. If a tool is unavailable, say so and use what exists. Don't fall back to memory silently.

## Phase 1 — Brief (one message, then stop)
Ask these in one numbered message: 1) what the site is (type, name, purpose); 2) users, and what they should feel and do; 3) primary action; 4) pages; 5) 3D/motion level (none/subtle/medium/heavy); 6) existing assets; 7) sites they love or hate; 8) mood words; 9) tech preference; 10) constraints (deadline, hosting, CMS, languages, a11y, performance).
Allow at most one follow-up round. Then run **one** fresh-context reviewer (a subagent given only the draft brief) to find gaps and conflicts. Bring back its top 3–5 questions only. Save `concepts_brief.md` and get confirmation. Suggest a fresh chat for Phase 2.

## Phase 2 — Design knowledge (cache it once, reuse it)
- If `research/DESIGN_RULES.md` already exists from a past project, reuse it and only add to it. Don't re-read the repos.
- Otherwise, read only the README/SKILL.md of: Hallmark (anti-slop gates), Impeccable (critique/detect), Emil Kowalski's skill (motion), and taste-skill. Run one GitHub search for newer repos and pick the top 2. Write the concrete rules (numbers, dos and don'ts) to `research/DESIGN_RULES.md`, about 150 lines max. Record the name, URL and last update for each repo.
- 21st.dev and MotionSites: browse only the categories the brief needs (for example, hero and nav). Note 3–5 candidate components. Free components only. Never use generate tools or premium prompts.

## Phase 3 — Live research (6 sites, not 10+)
Choose 2 sites for layout/typography, 2 for motion, 1 for 3D/WebGL, and 1 wildcard, plus any sites the user named. None may be from the user's industry. Vary the picks every project. For each site, read the page text and the computed styles (fonts, sizes, spacing, colors) with a short JS snippet where possible. That costs far fewer tokens than eyeballing screenshots. Add at most two screenshots per site. Note the craft in up to 8 bullets: grid, spacing, type, color, components and their states, motion (ms/easing), 3D, accessibility, and the wow moment.

## Phase 4 — Plan (before any code)
Write `research/DESIGN_RESEARCH.md` with: universal principles (15–25 rules), 2–3 concepts with a recommendation, a design system (tokens, type scale, spacing, grid, radius, shadow, component states, motion tokens, 3D budget), a sitemap with wireframes, and a Do/Don't list.
Write `design_draft.md` from the brief and the research, all at once. Don't pause after every section. Run **one** fresh-context reviewer on it, then go through its findings with the user. Wait for approval. Suggest a fresh chat for the build, attaching the brief and the draft.

## Phase 5 — Build
Build the hero alone first, render it, and check it against Hallmark's Floor. Then build tokens, components with all their states, then pages. Adapt 21st.dev components to the project's tokens. Use motion with intent and respect `prefers-reduced-motion`. For 3D: lazy-load, a poster fallback, compressed assets, pause when off-screen. Use real copy only and never invent facts, numbers, logos or testimonials. Aim for semantic HTML, WCAG AA and Lighthouse ≥ 90. The README maps each section to the rule it follows.

## Phase 6 — Verify
Run the site locally. Take one desktop and one mobile screenshot of each page. Run `/hallmark audit` and `npx impeccable detect` if they're installed. Report only the failures, then fix them. Nothing ships with a Floor failure: contrast, focus, reduced motion, invented facts, broken phone layout. The final report covers what was built, how to run it, the screenshots, and known limits, in under 15 lines.

## Never
- Avoid AI-slop tells: an eyebrow label over every heading, tracked-caps labels, one colored word in a headline, a centered hero with 3 cards, an email signup at the end of every page, fake success messages.
- Don't copy competitors. Take principles, not assets.
- Don't skip the check-ins after Phases 1, 4 and 6.
