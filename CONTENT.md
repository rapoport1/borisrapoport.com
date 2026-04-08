# Content — All Written Copy

This file contains all text content for the site, organized by page. Feel free to edit and personalize.

---

## Homepage

### Hero Section
**Title:** Boris Rapoport — Automation & QA Leadership

**Subtitle:** Lead Scrum Master @ WeSuite LLC

**Tagline:** Bridging the cosmos of automation with the precision of QA leadership

**CTA Buttons:**
1. "View Projects" → `/projects/`
2. "Get in Touch" → `/contact/`

### Quick Navigation Cards
1. **About** — "Physics, automation, and the climb"
2. **Projects** — "Automation, QA, and innovation"
3. **Contact** — "Let's build something great"

---

## About Page

Full content is in `content/about/_index.md`. Summary:

### Main Content
Three to four paragraphs covering:
1. Introduction (BS Physics, BA Astronomy, 4+ years QA/automation)
2. Connection between physics research and QA automation
3. Why both space and climbing matter (patterns, resilience, precision)
4. Current focus and call to action

### Key Points to Emphasize
- Physics → Observation and pattern-finding
- Astronomy → Understanding complexity
- QA → Verification and safety
- Climbing → Resilience and trust
- Leadership → Moving teams forward

---

## Projects

Each project has:
- **Title** — Clear, descriptive
- **Description** — One sentence problem/value
- **Status** — Active, Archived, In Progress
- **Tech Stack** — Array of technologies
- **Links** — GitHub, Live Demo (if applicable)
- **Body** — 3–5 paragraph description

### Current Projects

#### 1. WeSuite Test Automation Framework
- **Status:** Active
- **Tech:** Cypress, JavaScript, Docker, GitHub Actions
- **Description:** End-to-end testing infrastructure for document generation
- **Impact:** 80% reduction in regression testing time
- **Link:** https://github.com/brapoport/wesuite-automation

#### 2. Magic: The Gathering Scorekeeper
- **Status:** Active
- **Tech:** HTML, CSS, JavaScript, GitHub Pages
- **Description:** Responsive web app for tracking life totals during games
- **Link:** https://github.com/brapoport/mtg-scorekeeper (Code)
- **Link:** https://brapoport.github.io/mtg-scorekeeper/ (Live Demo)

#### 3. Scrum Automation Toolkit
- **Status:** Active
- **Tech:** Python, Jira API, JSON, Shell Scripts
- **Description:** Utilities for sprint planning, reporting, and velocity tracking
- **Impact:** 3+ hours saved per sprint on admin work
- **Link:** https://github.com/brapoport/scrum-automation-toolkit

#### 4. Planetary Nebulae Spectral Analysis
- **Status:** Archived
- **Tech:** Python, NumPy, Matplotlib, Spectroscopy
- **Description:** Physics research analyzing emission spectra from nebulae
- **Note:** Foundation of the Quantum Ascent design theme
- **Link:** https://github.com/brapoport/nebulae-spectral-analysis

#### 5. Smart Test Data Generator
- **Status:** Active
- **Tech:** Python, Faker, SQLite, JSON
- **Description:** Generates realistic test data for document validation
- **Impact:** Hours of prep reduced to minutes
- **Link:** https://github.com/brapoport/test-data-generator

### Coming Soon
"AI-powered tools and automation frameworks in development"

---

## Contact Page

### Intro Text
**Title:** Get in Touch

**Subtitle:** Let's discuss automation, QA, or how I can help your team

### Contact Form
Fields:
1. **Name** — Required, text input
2. **Email** — Required, email input
3. **Subject** — Optional, text input
4. **Message** — Required, textarea

### Backup Contact
"Or connect with me on [LinkedIn](https://www.linkedin.com/in/rapoporb1/)"

---

## Navigation & Footer

### Main Navigation
1. About → `/about/`
2. Projects → `/projects/`
3. Contact → `/contact/`
4. LinkedIn → https://www.linkedin.com/in/rapoporb1/

### Footer
**Left Section:**
- Name: Boris Rapoport
- Title: Lead Scrum Master @ WeSuite LLC
- Location: Brooklyn, NY

**Middle Section:**
- **Connect**
  - LinkedIn
  - GitHub
  - Contact

**Right Section:**
- **Site Info**
  - Privacy Policy
  - "Built with Hugo + ❤️"
  - "Theme: Quantum Ascent"

**Bottom:**
- Copyright: "© 2026 Boris Rapoport. All rights reserved."
- Privacy Note: "No tracking. No analytics. Privacy first."

---

## SEO & Meta

### Site Title
"Boris Rapoport — Automation & QA Leadership"

### Site Description
"Lead Scrum Master at WeSuite LLC. Physics + Astronomy background. Automation, QA, and leadership."

### Social Tags
- Author: Boris Rapoport
- Type: Personal website / Portfolio
- Theme colors: Nebula purples, deep navy, climbing oranges

---

## Email Configuration

### Contact Form Setup
The form uses **Formspree** (recommended for simplicity):

1. Visit https://formspree.io
2. Create a new form
3. Replace `YOUR_FORM_ID` in `themes/quantum-ascent/layouts/section/contact.html` with your form ID
4. All messages go to your configured email

### Alternative: Custom Email Forwarding
For future custom filtering:
- Contact emails received at: `contact@borisrapoport.com`
- Can be filtered/forwarded to: `rapoport1@gmail.com` (private)
- Template-based routing: newsletter, project inquiries, employment, spam

---

## Tone & Voice Guidelines

### Writing Style
- **Clear & Concise** — No corporate jargon
- **Technical but Accessible** — Explain tech choices without being arrogant
- **Authentic** — Your real voice, not marketing speak
- **Confident** — Proud of your work, but humble
- **Action-Oriented** — Results matter; show impact

### Do's
- Use active voice
- Show impact (80% reduction, 3+ hours saved)
- Link to proof (GitHub repos, live demos)
- Personal touches (physics background, climbing interests)

### Don'ts
- Don't oversell
- Don't hide behind buzzwords
- Don't make claims you can't back up
- Don't forget the human element

### Examples

❌ "Utilized advanced testing methodologies to optimize quality assurance processes"

✅ "Built a test automation framework that reduced regression testing time from 20 minutes to 5 minutes"

---

## Content Updates

When adding new projects:
1. Create `content/projects/project-name.md`
2. Include frontmatter: title, description, date, status, tech, github/live
3. Write 3–5 paragraphs with context, solution, and impact
4. Projects automatically appear in the grid (sorted by date)

When updating About/Contact:
1. Edit the respective `_index.md` files
2. Rebuild with `hugo` (automatic in CI/CD)
3. Commit and push; GitHub Actions handles deployment

---

## Asset Paths

- **Images:** `static/images/` (referenced as `/images/filename`)
- **Social links:** Use full URLs (https://linkedin.com/...)
- **Internal links:** Use relative paths (`/projects/`, `/about/`)
- **GitHub repos:** Use full GitHub URLs (https://github.com/brapoport/...)

---

## Contact Form Backend Setup

After Hugo site is deployed:

### Option 1: Formspree (Recommended)
1. Go to https://formspree.io
2. Sign up / log in
3. Create new form → get Form ID
4. Update contact.html with Form ID
5. Test form submission
6. All emails route to your configured address

### Option 2: Netlify Forms
If hosting on Netlify instead of GitHub Pages, add to Hugo template:
```html
<form name="contact" method="POST" netlify>
  <!-- form fields -->
</form>
```

### Option 3: Custom Lambda (Future)
For advanced filtering and routing:
- AWS Lambda function receives form submission
- Filters based on type (recruitment, project inquiry, spam)
- Routes to appropriate email address
- Future enhancement (Dave can build this)

---

That's all the content! Personalize as needed, and remember: authenticity > polish.
