# Website Setup — Complete Deployment Guide

This guide walks you through deploying your Hugo site to GitHub Pages with CloudFlare CDN and a custom domain.

---

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Local Setup](#local-setup)
3. [GitHub Repository](#github-repository)
4. [GitHub Pages Configuration](#github-pages-configuration)
5. [Custom Domain Setup](#custom-domain-setup)
6. [CloudFlare Configuration](#cloudflare-configuration)
7. [Automated Deployment](#automated-deployment)
8. [Testing & Verification](#testing--verification)
9. [Troubleshooting](#troubleshooting)

---

## Prerequisites

### Software
- **Git** (https://git-scm.com/downloads)
- **Hugo** (https://gohugo.io/installation/)
  - Version: 0.100.0 or newer
  - Verify: `hugo version`

### Accounts
- **GitHub** (https://github.com/signup) — Free account is fine
- **CloudFlare** (https://dash.cloudflare.com/signup) — Free plan sufficient
- **Domain registrar** — For borisrapoport.com (if you don't own it yet)
- **Email service** — For contact form (Formspree is easiest)

### Domain
If you don't own `borisrapoport.com` yet:
1. Go to a registrar (Namecheap, GoDaddy, Google Domains, etc.)
2. Buy `borisrapoport.com` for ~$12/year
3. Once purchased, you'll configure nameservers in the next steps

---

## Local Setup

### 1. Clone This Repository (If Starting Fresh)

If you have the Hugo project in `/root/.openclaw/workspace/boris-website`:

```bash
cd /root/.openclaw/workspace/boris-website
git init
git add .
git commit -m "Initial Hugo project setup"
```

Or, if cloning from GitHub:
```bash
git clone https://github.com/brapoport/borisrapoport.com.git
cd borisrapoport.com
```

### 2. Install Dependencies

No npm or external dependencies needed — this is a pure Hugo + CSS project.

### 3. Test Locally

Run the Hugo development server:

```bash
hugo server
```

You should see:
```
Web Server is available at http://localhost:1313/
Press Ctrl+C to stop
```

Visit http://localhost:1313 in your browser. Everything should work:
- ✅ Homepage renders
- ✅ Navigation works
- ✅ Projects grid displays
- ✅ Contact form loads

### 4. Build Static Files

Generate production-ready HTML:

```bash
hugo --minify
```

This creates the `public/` directory with all static assets. This is what gets deployed to GitHub Pages.

---

## GitHub Repository

### 1. Create New Repository

1. Log in to GitHub
2. Click **+** → **New repository**
3. **Repository name:** `borisrapoport.com` (or your preference)
4. **Description:** "Personal brand website — QA automation + physics"
5. **Visibility:** Public (required for free GitHub Pages)
6. ✅ **Initialize with README** (optional)
7. Click **Create repository**

### 2. Add Remote & Push

In your local project:

```bash
# Add GitHub as remote
git remote add origin https://github.com/brapoport/borisrapoport.com.git

# Rename branch to main (if needed)
git branch -M main

# Push code
git push -u origin main
```

### 3. Verify on GitHub

Go to https://github.com/brapoport/borisrapoport.com — you should see your code.

---

## GitHub Pages Configuration

### 1. Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** → **Pages** (left sidebar)
3. Under "Build and deployment":
   - **Source:** "GitHub Actions" (recommended for Hugo)
   - Click **Configure**

### 2. Add GitHub Actions Workflow

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy Hugo Site

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: recursive

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v4
        with:
          hugo-version: 'latest'
          extended: false

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          cname: borisrapoport.com
```

**Push this file to your repo:**

```bash
mkdir -p .github/workflows
# Create the file above or copy from GITHUB-ACTIONS.md
git add .github/workflows/deploy.yml
git commit -m "Add GitHub Actions deployment"
git push
```

### 3. Verify Deployment

1. Go to your repository
2. Click **Actions** tab
3. You should see a workflow run starting
4. Wait for it to complete (green checkmark = success)
5. Your site is now published to `https://brapoport.github.io/borisrapoport.com/`

---

## Custom Domain Setup

### 1. Point Your Domain to GitHub Pages

You have two options:

#### Option A: CloudFlare Nameservers (Recommended)
You'll do this in the next step. For now, continue.

#### Option B: Direct DNS Records (Without CloudFlare)
If you're not using CloudFlare:

1. Log in to your domain registrar (Namecheap, GoDaddy, etc.)
2. Find DNS settings
3. Add these **A records:**
   ```
   Type: A
   Name: @
   Value: 185.199.108.153
   
   Type: A
   Name: @
   Value: 185.199.109.153
   
   Type: A
   Name: @
   Value: 185.199.110.153
   
   Type: A
   Name: @
   Value: 185.199.111.153
   ```
4. Add **CNAME record:**
   ```
   Type: CNAME
   Name: www
   Value: brapoport.github.io
   ```
5. Wait 15–60 minutes for DNS to propagate
6. Jump to [Verify Custom Domain](#verify-custom-domain)

### 2. CloudFlare Setup (Recommended Path)

See **[CLOUDFLARE-SETUP.md](CLOUDFLARE-SETUP.md)** for detailed instructions. In summary:

1. Add domain to CloudFlare
2. Update nameservers at your registrar
3. Create DNS records pointing to GitHub Pages
4. Enable SSL/TLS and caching

### 3. Verify Custom Domain

In your GitHub repository:

1. Go to **Settings** → **Pages**
2. Under "Custom domain," enter `borisrapoport.com`
3. Click **Save**
4. GitHub creates a `CNAME` file in your repo

**Test in browser:**
- http://borisrapoport.com (should redirect to HTTPS)
- https://borisrapoport.com (should work)
- https://www.borisrapoport.com (should work)

If you get connection errors, DNS hasn't propagated yet. Wait 15–60 minutes and try again.

---

## Automated Deployment

Your GitHub Actions workflow is already set up. Every time you push to `main`:

1. **GitHub detects push**
2. **Actions workflow runs:**
   - Checks out code
   - Installs Hugo
   - Builds site (`hugo --minify`)
   - Deploys to GitHub Pages
3. **Site updates live** (usually within 2–5 minutes)

**To deploy a change:**

```bash
# Edit a file (e.g., about page)
nano content/about/_index.md

# Commit and push
git add content/about/_index.md
git commit -m "Update about page"
git push origin main
```

Check **Actions** tab to see the deployment progress.

---

## Contact Form Setup

### Using Formspree (Recommended)

1. Go to https://formspree.io
2. Sign up with your email
3. Create a new form:
   - Name: "borisrapoport.com"
   - Email: your email address
4. Copy the **Form ID** (e.g., `myzjwkxk`)
5. Edit `themes/quantum-ascent/layouts/section/contact.html`:
   ```html
   <form action="https://formspree.io/f/myzjwkxk" method="POST">
   ```
6. Replace `myzjwkxk` with your Form ID
7. Push changes:
   ```bash
   git add themes/quantum-ascent/layouts/section/contact.html
   git commit -m "Configure Formspree contact form"
   git push
   ```

**Test form:**
1. Visit https://borisrapoport.com/contact/
2. Fill in and submit
3. You should receive an email
4. Click the link in the email to confirm

---

## Testing & Verification

### Pre-Launch Checklist

- [ ] Local `hugo server` works without errors
- [ ] All pages render correctly
- [ ] Links (internal and external) work
- [ ] Projects grid displays all 5 projects
- [ ] Contact form submits and you receive email
- [ ] Navigation is responsive on mobile
- [ ] GitHub Pages deployment succeeds (Actions tab green)
- [ ] Custom domain resolves to your site
- [ ] HTTPS works (lock icon in browser)
- [ ] No 404 errors in browser console

### Performance Testing

**Lighthouse Audit (Chrome DevTools):**
1. Visit https://borisrapoport.com
2. Open DevTools (F12)
3. Click **Lighthouse**
4. Run audit
5. Target scores: Performance 90+, Accessibility 95+, Best Practices 90+, SEO 100

**Mobile Testing:**
1. Open site on your phone
2. Check layout (should stack vertically)
3. Check buttons (should be tappable)
4. Check scrolling (should be smooth)

### URL Verification

All these should work:
- https://borisrapoport.com/
- https://www.borisrapoport.com/
- https://borisrapoport.com/about/
- https://borisrapoport.com/projects/
- https://borisrapoport.com/contact/

---

## Troubleshooting

### "Site not found" or 404 errors

**Problem:** Custom domain shows 404

**Solutions:**
1. **Check DNS propagation:** https://dnschecker.org
   - Enter `borisrapoport.com`
   - Should show CloudFlare IPs
2. **Verify CNAME file:** In repo, check for `CNAME` file in root
   - Should contain: `borisrapoport.com`
3. **Wait:** DNS can take 15–60 minutes to propagate

### GitHub Actions deployment fails

**Problem:** Red X in Actions tab

**Solutions:**
1. Click the failed workflow to see logs
2. Common issues:
   - Hugo version mismatch: Update to `latest` in workflow
   - Theme not initialized: Ensure theme files are in repo
   - Branch name: Check workflow targets correct branch (`main`)
3. Re-run workflow after fixing

### Contact form not receiving emails

**Problem:** Form submits but no email arrives

**Solutions:**
1. **Check spam/junk folder**
2. **Verify Form ID:** Paste correct Formspree ID in contact.html
3. **Test Formspree:** Go to https://formspree.io, log in, check submissions
4. **Confirm email:** Formspree sends confirmation email; click it

### HTTPS not working

**Problem:** Browser shows "Not Secure" or HTTPS errors

**Solutions:**
1. **Wait:** CloudFlare SSL can take 5–10 minutes
2. **Verify:** In CloudFlare dashboard, check SSL/TLS status
3. **Force HTTPS:** In CloudFlare, set "Always Use HTTPS" to ON

### Styles not loading

**Problem:** Site renders but looks unstyled (no colors, no spacing)

**Solutions:**
1. **Check CSS files:** Verify `themes/quantum-ascent/static/css/` exists in repo
2. **Clear cache:** Hard refresh (Ctrl+Shift+R or Cmd+Shift+R)
3. **Check CloudFlare caching:** Purge cache in CloudFlare dashboard
4. **Hugo build:** Rebuild locally: `hugo --minify`

### Site looks broken on mobile

**Problem:** Layout is jumbled, text overlaps, buttons aren't clickable

**Solutions:**
1. **Check viewport meta tag:** Should be in baseof.html
   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   ```
2. **Check responsive CSS:** Verify `responsive.css` loads
3. **Test in browser DevTools:**
   - Press F12 → Click phone icon (device emulation)
   - Test on iPhone 12, Pixel 5
4. **Check for JavaScript errors:** DevTools Console tab

---

## Next Steps

### After Launch

1. **Share your site:** LinkedIn, email, resume
2. **Monitor:** Check Analytics (no Google Analytics due to privacy-first approach)
3. **Update projects:** Add new projects as you build them
4. **Update about:** Keep professional story current

### Maintenance

See **[MAINTENANCE.md](MAINTENANCE.md)** for:
- How to add new projects
- How to update existing content
- How to configure contact form filtering
- How to manage custom domain

---

## Support

If you run into issues:
1. Check **Troubleshooting** section above
2. See **[MAINTENANCE.md](MAINTENANCE.md)** for common updates
3. GitHub Pages docs: https://docs.github.com/en/pages
4. Hugo docs: https://gohugo.io/documentation/
5. CloudFlare docs: https://developers.cloudflare.com/

---

**Your site is production-ready. Push to GitHub and it's live.** 🚀
