# Maintenance — Site Updates & Operations

How to manage your site after launch: updating content, adding projects, managing form submissions, and keeping things running smoothly.

---

## Table of Contents
1. [Adding New Projects](#adding-new-projects)
2. [Updating Existing Content](#updating-existing-content)
3. [Contact Form Management](#contact-form-management)
4. [Cache Management](#cache-management)
5. [Monitoring & Analytics](#monitoring--analytics)
6. [Troubleshooting](#troubleshooting)
7. [Regular Maintenance Schedule](#regular-maintenance-schedule)

---

## Adding New Projects

### Quick Start

1. Create a new markdown file in `content/projects/`
2. Fill in frontmatter (metadata)
3. Write project description
4. Commit and push

### Step-by-Step

#### 1. Create Project File

```bash
cd /root/.openclaw/workspace/boris-website
nano content/projects/my-new-project.md
```

#### 2. Use This Template

```markdown
---
title: Your Project Title
description: One-sentence description of what this project does
date: 2026-04-08
status: Active
tech: ["Tech1", "Tech2", "Tech3"]
github: "https://github.com/brapoport/project-name"
live: "https://demo.example.com"  # Optional, if there's a live demo
---

## Your Project Title

Write a 3–5 paragraph description.

### Problem Solved

What problem did you solve?

### Key Features

- Feature 1
- Feature 2
- Feature 3

### Implementation

How did you build it?

### Impact

What was the result? (80% faster, saved 3 hours/week, etc.)

**Status:** Active and maintained.
```

#### 3. Customize

- Change `title` to your project name
- Update `date` to today's date (YYYY-MM-DD)
- Update `status`: Active, In Progress, or Archived
- List `tech` stack
- Add GitHub link (required)
- Add `live` link if there's a demo
- Write the description (follow PROJECT-TEMPLATE.md for style)

#### 4. Commit and Push

```bash
git add content/projects/my-new-project.md
git commit -m "Add new project: My New Project"
git push origin main
```

**GitHub Actions will automatically:**
1. Build the site
2. Add your project to the grid
3. Deploy to GitHub Pages (2–5 minutes)

#### 5. Verify

1. Wait 2–5 minutes
2. Go to https://borisrapoport.com/projects/
3. Your project should appear in the grid
4. Projects are sorted by date (newest first)

---

## Updating Existing Content

### Homepage

Edit `content/_index.md`:
```bash
nano content/_index.md
```

Minimal file — mostly just frontmatter. Homepage layout is in theme.

### About Page

Edit `content/about/_index.md`:
```bash
nano content/about/_index.md
```

This is where the main "About" content lives. Update your bio as your career evolves.

### Contact Page

Edit `content/contact/_index.md`:
```bash
nano content/contact/_index.md
```

Mostly frontmatter. Contact form is in the theme template.

### Update a Project

Edit the project's markdown file:
```bash
nano content/projects/project-name.md
```

Change title, description, tech stack, or body content. Commit and push.

---

## Contact Form Management

### Using Formspree

#### 1. Check Submissions

1. Go to https://formspree.io
2. Log in
3. Click your form ("borisrapoport.com")
4. You'll see all submissions

#### 2. Reply to Messages

Formspree doesn't have built-in replies. You'll need to:
1. See the submitted email address
2. Reply directly from your email client

#### 3. Spam Management

If you're getting spam:

**In Formspree:**
- Use "Mark as Spam" on submissions
- Formspree's filter learns over time

**Add Rate Limiting (CloudFlare):**
1. Go to CloudFlare dashboard
2. **Security** → **Rate Limiting**
3. Add rule:
   ```
   URL: borisrapoport.com/contact/
   Requests: 10 per minute per IP
   Block 429
   ```

#### 4. Custom Email Filtering

If Formspree gets too spammy, you can set up a custom solution:

**Option A: Email filter (simple)**
- Set up rule in your email client to filter form submissions

**Option B: Formspree Plus (paid)**
- Upgrade Formspree for better spam filtering

**Option C: Custom Lambda (future)**
- Dave can build a custom AWS Lambda function
- Filters based on keywords, rate limits, etc.
- Routes different inquiry types to different inboxes

### Future: Custom Contact Form Backend

When you're ready, we can build:
1. Custom email filtering (spam, recruitment, project inquiries)
2. Categorization and routing
3. Auto-responses based on inquiry type
4. Database logging of submissions

Just let Dave know when you want to upgrade.

---

## Cache Management

### When You Push a Site Update

1. **GitHub Actions builds** (automatic) → 2–3 minutes
2. **CloudFlare serves cached old version** → until cache expires
3. **User browsers cache** → until browser cache expires

To force immediate updates:

#### Option A: Purge CloudFlare Cache (Recommended)

1. Go to CloudFlare dashboard
2. Click your domain
3. **Caching** → **Purge Cache**
4. Click **Purge Everything**
5. Wait ~30 seconds
6. Site shows new version

#### Option B: User Hard Refresh

Visitors can force a fresh load:
- Windows/Linux: `Ctrl+Shift+R`
- Mac: `Cmd+Shift+R`

#### Option C: Cache Duration

You can adjust how long CloudFlare caches:

In CloudFlare:
1. **Caching** → **Cache Level**
2. Currently set to **Cache Everything**
3. Browser cache TTL: 4 hours

To reduce: Set to 1 hour or 30 minutes (faster updates, slightly slower performance)

---

## Monitoring & Analytics

### CloudFlare Analytics

Understand your traffic:

1. Go to CloudFlare dashboard
2. Click your domain
3. **Analytics** (left sidebar)

You'll see:
- **Requests:** Total page views
- **Data transferred:** Bandwidth used
- **Threats blocked:** Security events (DDoS, bots, etc.)
- **Caching efficiency:** How much CloudFlare cached

### Using Analytics

**Weekly check:**
- How many people visited?
- Did caching save bandwidth?
- Were any threats blocked?

**Monthly trends:**
- Is traffic growing?
- What pages are most popular?
- Any unusual spikes?

### GitHub Actions Status

Monitor site builds:

1. Go to your GitHub repository
2. **Actions** tab
3. See deployment history

**What to look for:**
- ✅ Green checkmarks = successful deploys
- ❌ Red X = build failed (check logs)
- Deployment time (should be 30–60 seconds)

---

## SSL/TLS Certificate

### Automatic Renewal

CloudFlare automatically renews SSL certificates. You don't need to do anything.

**To verify it's active:**
1. CloudFlare → **SSL/TLS** → **Edge Certificates**
2. Should show "Universal SSL certificate active"

### Force HTTPS

Already enabled. All HTTP requests redirect to HTTPS.

**To verify:**
1. Try visiting http://borisrapoport.com
2. Browser auto-redirects to https://borisrapoport.com

---

## Domain Management

### Renew Your Domain

Your domain expires after 1 year. Set a reminder to renew:

1. Check expiration date in registrar (Namecheap, GoDaddy, etc.)
2. Renew 30 days before expiration
3. Cost: ~$12/year

CloudFlare won't renew it — only your registrar will.

### Change Registrar

If you want to move to a different registrar:

1. Unlock domain at current registrar
2. Request authorization code
3. Transfer to new registrar
4. Update nameservers to CloudFlare's (same process as initial setup)

CloudFlare works with any registrar.

---

## Troubleshooting

### Site Is Down

**Check in this order:**

1. **CloudFlare status:** Is it up?
   - Go to https://status.cloudflare.com
2. **GitHub status:** Did deployment fail?
   - Go to repo → **Actions** tab
   - Look for red X
   - Click to see error logs
3. **DNS resolution:** Is domain still pointing to CloudFlare?
   - Use https://dnschecker.org
   - Should show CloudFlare IPs
4. **Browser cache:** Is your browser showing old cached version?
   - Hard refresh: Ctrl+Shift+R

### Contact Form Not Working

**Check:**

1. **Is CloudFlare blocking it?**
   - CloudFlare → **Security** → **WAF rules**
   - Check if /contact/ is blocked

2. **Is Formspree up?**
   - Go to https://status.formspree.io

3. **Did you configure Form ID?**
   - Check `themes/quantum-ascent/layouts/section/contact.html`
   - Make sure action attribute has correct Formspree ID

4. **Test directly:**
   ```bash
   curl -X POST https://formspree.io/f/YOUR_FORM_ID \
     -H "Content-Type: application/json" \
     -d '{"name":"Test","email":"test@example.com","message":"test"}'
   ```

### Slow Site Performance

**Check:**

1. **Is CloudFlare caching working?**
   - CloudFlare → **Caching** → **Cache Level**
   - Should be "Cache Everything"

2. **Are images optimized?**
   - Compress images before adding to repo
   - Use https://tinypng.com or https://imageoptim.com

3. **Check Lighthouse score:**
   - Open site → F12 → Lighthouse tab
   - Run audit
   - Target: Performance 90+

4. **CloudFlare analytics:**
   - Check cache hit rate (should be > 80%)
   - If low, increase cache TTL

### HTTPS Certificate Issues

**Problem:** Browser shows SSL warning

**Check:**

1. **Is certificate active?**
   - CloudFlare → **SSL/TLS** → **Edge Certificates**
   - Should show "active"

2. **Hard refresh:**
   - Ctrl+Shift+R (or Cmd+Shift+R on Mac)

3. **Clear browser cache:**
   - Settings → Clear browsing data → Cached images/files

4. **Wait:**
   - Certificate issuance takes 5–10 minutes
   - Check back later

---

## Regular Maintenance Schedule

### Daily
- Nothing needed (automatic)

### Weekly
- Check CloudFlare analytics
- Verify site still loads
- Spot-check projects grid

### Monthly
- Review contact form submissions
- Check Analytics trends
- Update About page if career changes
- Purge CloudFlare cache if you pushed updates

### Quarterly
- Review GitHub Actions deployment history
- Check Lighthouse scores
- Test contact form submission
- Review security settings

### Annually
- Renew domain (~$12)
- Review SSL certificate (automatic, but verify)
- Update projects (add new, remove old)
- Refresh About page

---

## Making Updates: Workflow

### Update 1: Add New Project

```bash
# 1. Create file
nano content/projects/new-thing.md

# 2. Add content using template
# ... write project description ...

# 3. Save and push
git add content/projects/new-thing.md
git commit -m "Add project: New Thing"
git push origin main

# 4. Wait 2–5 minutes for GitHub Actions
# 5. Purge CloudFlare cache
# 6. Verify at borisrapoport.com/projects/
```

### Update 2: Fix a Typo

```bash
# 1. Find and edit
nano content/about/_index.md
# ... fix typo ...

# 2. Commit and push
git add content/about/_index.md
git commit -m "Fix typo on About page"
git push origin main

# 3. Wait for deployment (2–5 min)
# 4. Hard refresh in browser (Ctrl+Shift+R)
```

### Update 3: Modify Design

```bash
# 1. Edit CSS
nano themes/quantum-ascent/static/css/quantum-ascent.css
# ... change colors, spacing, etc ...

# 2. Test locally
hugo server
# Check http://localhost:1313

# 3. Commit and push
git add themes/quantum-ascent/static/css/quantum-ascent.css
git commit -m "Update hero section spacing"
git push origin main

# 4. Purge CloudFlare cache to force immediate update
```

---

## Files You'll Edit Most Often

| File | Purpose | How Often |
|------|---------|-----------|
| `content/projects/*.md` | Add/update projects | Monthly |
| `content/about/_index.md` | Update bio | Quarterly |
| `content/contact/_index.md` | Update contact info | Rarely |
| `config.toml` | Site settings | Rarely |
| `themes/quantum-ascent/static/css/*.css` | Styling | As needed |

---

## Common Commands

```bash
# Clone repo (first time)
git clone https://github.com/brapoport/borisrapoport.com.git

# See what changed
git status

# Commit changes
git add .
git commit -m "Your message"

# Push to GitHub (triggers deployment)
git push origin main

# Check build status
# Go to: https://github.com/brapoport/borisrapoport.com/actions

# Test locally
hugo server

# Build for production
hugo --minify
```

---

## Getting Help

If something breaks:

1. Check **Troubleshooting** section above
2. Check **WEBSITE-SETUP.md** for deployment issues
3. Check **GITHUB-ACTIONS.md** for build errors
4. Check **CLOUDFLARE-SETUP.md** for DNS/SSL issues
5. Contact Dave if it's really stuck

---

## Summary

Your site is built to be low-maintenance:

- ✅ Automatic deployments on every push
- ✅ Automatic HTTPS and SSL renewal
- ✅ Global CDN for fast content delivery
- ✅ Built-in security and DDoS protection
- ✅ No server to manage
- ✅ No database to maintain

**Main task:** Update your content. Everything else is automatic. 🚀
