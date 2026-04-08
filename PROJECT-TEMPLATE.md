# Project Template — How to Write Project Descriptions

Use this template when adding new projects to your portfolio. It includes guidance on tone, structure, and what makes a compelling project description.

---

## Quick Template

```markdown
---
title: Project Name
description: One-sentence summary of what this project does
date: 2026-04-08
status: Active
tech: ["Tech1", "Tech2", "Tech3"]
github: "https://github.com/brapoport/project-name"
live: "https://example.com/demo"  # Optional
---

## Project Name

Brief intro paragraph explaining the core idea.

### Problem Solved

What problem did you tackle? Why did it matter?

### Solution

How did you approach it? What's the architecture/approach?

### Key Features

- Feature 1 with impact
- Feature 2 with impact
- Feature 3 with impact

### Implementation Details

Technical deep-dive (optional, 1–2 paragraphs).

### Results & Impact

What was the outcome? Metrics, feedback, lessons learned.

**Status:** Active and maintained / Archived / In Progress
```

---

## Writing Guidelines

### Title
- **Clear & specific** — What's the project called?
- **Professional** — Suitable for LinkedIn/resume
- ✅ Good: "WeSuite Test Automation Framework"
- ❌ Bad: "Testing Stuff"

### Description (One Sentence)
- **Problem + solution** — What does it do?
- **Concise** — Under 100 characters
- ✅ Good: "Cypress-based end-to-end testing infrastructure for document generation"
- ❌ Bad: "A tool I built"

### Problem Solved
**Purpose:** Set context. Why should anyone care?

**Write:**
- What gap existed?
- Why was it a problem?
- Who was affected?

**Example:**
> Manual test data creation was tedious, inconsistent, and error-prone. Test engineers spent hours generating datasets by hand, and coverage was incomplete. I needed a way to generate realistic, reproducible test data in seconds.

### Solution
**Purpose:** Show your approach and thinking.

**Write:**
- How did you approach the problem?
- What tech stack did you choose and why?
- What were the trade-offs?

**Example:**
> Built a Python-based generator using the Faker library for realistic data, with SQLite for local storage and JSON export for CI/CD integration. Chose Python for rapid development and strong data manipulation libraries. Considered Go (faster) but Python's ecosystem won out.

### Key Features
**Purpose:** Highlight concrete value.

**Format:** Bullet points with impact

**Write:** Feature + benefit

**Example:**
- **Batch generation** — Create 500 test cases in seconds vs. hours manually
- **Reproducible seeds** — Same seed = identical datasets for deterministic testing
- **Custom templates** — Define your own schemas without coding

❌ Don't just list features:
- ❌ "Has templates"
- ✅ "Customizable templates for any data schema"

### Implementation Details (Optional)
**Purpose:** For technically-minded readers.

**Write:**
- Architecture overview
- Key algorithms
- Notable technical decisions

**Example:**
> Used a two-pass generation strategy: first pass populates primary records, second pass creates relationships and enforces constraints. This prevents orphaned records and ensures referential integrity across large datasets.

### Results & Impact
**Purpose:** Prove it worked.

**Write:**
- Metrics (faster, cheaper, better)
- Feedback (what did users say?)
- Lessons learned

**Example:**
> Reduced test case prep time from 3 hours to 5 minutes (97% reduction). QA team adopted it for all new feature testing. Learned that user-friendliness matters more than features—initial CLI was hard to use; added GUI wrapper, adoption tripled.

---

## Status Field

Use one of:
- **Active** — Actively maintained and in use
- **In Progress** — Under active development
- **Archived** — Old project, no longer maintained but code is available

---

## Tech Stack Examples

Be specific. List actual libraries/frameworks, not categories.

✅ Good:
```yaml
tech: ["Cypress", "JavaScript", "Docker", "GitHub Actions", "PostgreSQL"]
```

❌ Vague:
```yaml
tech: ["Testing", "Web", "Backend"]
```

---

## Links

### GitHub
- **Required** for all projects
- Full GitHub URL: `https://github.com/brapoport/project-name`
- Code should be public and well-documented

### Live Demo
- **Optional** — Include if there's something to visit
- For web apps, APIs, tools with UIs
- ✅ Good: `https://brapoport.github.io/mtg-scorekeeper/`
- ❌ Bad: Internal/private links

---

## Examples

### Example 1: Automation Tool

```markdown
---
title: Scrum Automation Toolkit
description: Python scripts for sprint planning, reporting, and velocity tracking
date: 2024-06-10
status: Active
tech: ["Python", "Jira API", "JSON", "Shell Scripts"]
github: "https://github.com/brapoport/scrum-automation-toolkit"
---

## Scrum Automation Toolkit

Managing sprints involves a lot of repetitive work: generating reports, analyzing velocity, creating release notes. I built a toolkit of Python utilities to automate these tasks.

### Problem Solved

Scrum Masters spend 3+ hours per sprint on administrative work: burndown reports, velocity calculations, backlog grooming. This is time that could be spent coaching teams or solving problems. The work is also error-prone—manual data entry is tedious and mistakes happen.

### Solution

Created a modular Python library that integrates with Jira's REST API to pull sprint data, perform analysis, and generate outputs. Each utility is standalone and can run in CI/CD or locally.

### Key Features

- **Sprint Report Generator** — Pulls closed issues and creates comprehensive retrospective summaries
- **Velocity Calculator** — Analyzes 5+ sprint history to identify trends and predict capacity
- **Release Notes Generator** — Auto-formats closed issues into structured release notes
- **Bulk Operations** — Update estimation, tags, or status for dozens of stories at once

### Implementation Details

Uses Jira's REST API v3 with OAuth for authentication (no passwords in code). Each script is independent but shares a common utilities library. Configuration via JSON files, outputs as JSON/CSV/Markdown.

### Results & Impact

Reduced sprint admin time from 3+ hours to 30 minutes (90% reduction). Team can now focus on delivery instead of ceremony logistics. The velocity calculator revealed we consistently underestimate 2–3 story points per sprint—fixed our forecasting.

**Status:** Active and expanding with new utilities.
```

### Example 2: Web App / Demo Project

```markdown
---
title: MTG Scorekeeper
description: Responsive web app for tracking life totals and game state during Magic games
date: 2024-03-20
status: Active
tech: ["HTML", "CSS", "JavaScript", "GitHub Pages"]
github: "https://github.com/brapoport/mtg-scorekeeper"
live: "https://brapoport.github.io/mtg-scorekeeper/"
---

## Magic: The Gathering Scorekeeper

Keeping score during Magic games can be annoying—pen and paper is error-prone, phone calculator is clunky. I needed a clean, mobile-friendly way to track life totals, poison counters, and game history.

### Problem Solved

During casual and competitive Magic games, players need to track:
- Life totals for 2–4 players
- Poison counters (Infect mechanic)
- Undo history (mistakes happen)
- Game state (who's winning?)

Existing apps either overload with features or have clunky UIs. I wanted something minimal, fast, and beautiful.

### Solution

Built a single-page web app with zero dependencies. Pure HTML/CSS/JavaScript means it loads instantly and works offline. Used the same glass morphism design from my personal site for visual consistency.

### Key Features

- **Dual-mode tracking** — Life totals AND poison counters
- **Undo history** — Made a mistake? Go back 10 turns
- **Mobile-first design** — One-handed gameplay on phone
- **Offline capable** — Works without internet
- **No ads, no tracking** — Privacy-first approach

### Implementation

Semantic HTML for accessibility. CSS Grid + Flexbox for responsive layout. Vanilla JavaScript for interactions—no frameworks means <50KB total. Uses localStorage to persist game state.

### Results & Impact

Used it at 20+ Magic game nights. Got feedback from other players—several asked for the link. Learned that simplicity wins: players love it because it stays out of the way and just works.

**Live Demo:** https://brapoport.github.io/mtg-scorekeeper/

**Status:** Actively maintained with regular feature requests from the Magic community.
```

### Example 3: Research Project

```markdown
---
title: Planetary Nebulae Spectral Analysis
description: Physics research analyzing emission line spectra to determine physical properties of nebulae
date: 2020-05-30
status: Archived
tech: ["Python", "NumPy", "Matplotlib", "Spectroscopy"]
github: "https://github.com/brapoport/nebulae-spectral-analysis"
---

## Planetary Nebulae Spectral Analysis

This is where my journey started. An undergraduate research project analyzing emission spectra from planetary nebulae, which led to my fascination with precision measurement, pattern-finding, and verification—skills that became the foundation of my QA automation practice.

### Problem Solved

Understanding physical properties of astronomical objects requires measuring and interpreting their light. Planetary nebulae emit light at specific wavelengths (emission lines) that encode information about temperature, density, and composition. The challenge was extracting these measurements from noisy spectroscopic data.

### Solution

Used Hubble Space Telescope spectroscopic data as input. Developed Python pipeline for:
1. Image calibration and preprocessing
2. Spectral line identification and fitting
3. Physical modeling to extract temperature and density
4. Error analysis and uncertainty quantification

### Key Features

- **Automated line fitting** — Gaussian deconvolution to measure line centers and widths
- **Physical modeling** — Photoionization equilibrium calculations
- **Uncertainty propagation** — Statistical analysis of measurement errors
- **Visualization** — Interactive plots of spectra and derived properties

### Results & Impact

Successfully measured electron temperature and density from forbidden line ratios. Calculated elemental abundances and compared to solar values. The research contributed to understanding the lifecycle of planetary nebulae.

More importantly: this project taught me that **precision measurement, pattern-finding, and verification** are universal skills. The tools changed (from spectroscopy to Cypress), but the mindset remained: ask the right questions, measure carefully, verify assumptions.

**Status:** Archived, but the code and analysis are preserved as a reminder of where this started. The nebula imagery in my Quantum Ascent design theme is a direct reference to these celestial objects.
```

---

## Length Guidelines

- **Short:** 3–4 paragraphs (total ~300 words)
  - Good for: Simple tools, demo projects
- **Medium:** 5–6 paragraphs (total ~500 words)
  - Good for: Full applications, frameworks
- **Long:** 7+ paragraphs (total ~800+ words)
  - Good for: Complex systems, research, deep dives

The MTG example above is ~350 words (short–medium). That's plenty.

---

## Tone & Voice

### Do
- ✅ Be proud of your work
- ✅ Use "I" — personal projects are personal
- ✅ Show impact with metrics
- ✅ Explain why you chose certain approaches
- ✅ Be honest about limitations

### Don't
- ❌ Oversell ("revolutionary," "disrupted the industry")
- ❌ Use buzzwords without substance
- ❌ Hide behind vague language ("leveraged synergies")
- ❌ Write about projects you didn't lead
- ❌ Make claims you can't back up

### Examples

❌ "Utilized advanced testing methodologies to optimize QA processes"
✅ "Built a Cypress framework that reduced regression testing time from 20 minutes to 5 minutes"

❌ "Developed an innovative solution"
✅ "Created a Python script that automated sprint report generation, saving 3+ hours per sprint"

---

## SEO & Discoverability

When you write projects, think about how people might search for them:

- Include **technology names** (Cypress, Python, React, etc.)
- Include **problem domain** (automation, testing, QA, etc.)
- Include **outcome metrics** (faster, cheaper, more reliable)

This helps when:
- Recruiters search for "Cypress automation expert"
- Other engineers search for "Python testing tool"
- You need to explain your work in interviews

---

## Updating Old Projects

When you update a project:

**Change date?**
- Only if it's a major rewrite
- Use original date for archive projects

**Edit description?**
- Yes, keep it current
- Update status if project evolved

**Add features?**
- Update the "Key Features" section
- Update "Results & Impact"

**Example:**
```markdown
---
title: WeSuite Test Automation
date: 2025-01-15  # Original date
status: Active
---

## Recent Updates (as of April 2026)

Added Playwright support alongside Cypress. Parallelization now runs 8 browsers simultaneously, cutting execution time in half. Framework runs in 150+ GitHub Actions workflows and catches ~40 bugs per month in staging.
```

---

## Final Checklist

Before publishing a project, check:

- [ ] Title is clear and specific
- [ ] Description is one sentence
- [ ] Frontmatter (date, status, tech, github) is complete
- [ ] Problem section explains the gap
- [ ] Solution explains your approach
- [ ] Features have benefits, not just features
- [ ] Results have metrics or concrete impact
- [ ] Tech stack is specific (not vague categories)
- [ ] GitHub link is correct and public
- [ ] Live link works (if included)
- [ ] No typos or grammar errors
- [ ] Tone is authentic and confident

---

## Adding It to Your Site

```bash
# 1. Create file
nano content/projects/project-name.md

# 2. Copy template and customize
# ... write your project description ...

# 3. Save and commit
git add content/projects/project-name.md
git commit -m "Add project: Project Name"
git push origin main

# 4. Wait 2–5 minutes for deployment
# 5. Check https://borisrapoport.com/projects/
```

---

## Questions?

Use the existing projects as examples:
- See `content/projects/wesuite-automation.md` for a professional tool
- See `content/projects/mtg-scorekeeper.md` for a personal project
- See `content/projects/planetary-nebulae-analysis.md` for research

Copy the structure, personalize the content, and you're good to go.

**Your projects tell your story. Make them count.** 🚀
