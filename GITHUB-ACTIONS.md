# GitHub Actions — CI/CD Configuration

Complete GitHub Actions workflow for automatic deployment of your Hugo site to GitHub Pages.

---

## File Location

Create this file at: `.github/workflows/deploy.yml`

```bash
mkdir -p .github/workflows
```

---

## Workflow File: `deploy.yml`

```yaml
name: Deploy Hugo Site to GitHub Pages

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        with:
          fetch-depth: 0
          submodules: recursive

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v4
        with:
          hugo-version: latest
          extended: false

      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v4

      - name: Build with Hugo
        run: |
          hugo \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}"

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: ./public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```

---

## What This Does

### Trigger Events
- **On every push to `main` branch:** Builds and deploys automatically
- **On pull requests:** Builds to check for errors (but doesn't deploy)

### Build Steps
1. **Checkout code** — Gets your repo code
2. **Setup Hugo** — Installs latest Hugo version
3. **Setup Pages** — Configures GitHub Pages environment
4. **Build** — Runs `hugo --minify` to generate static files
5. **Upload artifact** — Prepares `public/` directory
6. **Deploy** — Pushes built site to GitHub Pages

### Key Configuration

```yaml
branches:
  - main
```
Deploys only when you push to the `main` branch. If you use different branch names (e.g., `master`), update this.

```yaml
extended: false
```
Uses standard Hugo (not extended). Sufficient for this site. Set to `true` if you use SCSS.

---

## Installation & Setup

### 1. Create the Workflow File

```bash
# Navigate to your project
cd /root/.openclaw/workspace/boris-website

# Create directory
mkdir -p .github/workflows

# Create the file
cat > .github/workflows/deploy.yml << 'EOF'
name: Deploy Hugo Site to GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          submodules: recursive

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v4
        with:
          hugo-version: latest

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          cname: borisrapoport.com
EOF
```

### 2. Commit and Push

```bash
git add .github/workflows/deploy.yml
git commit -m "Add GitHub Actions workflow for Hugo deployment"
git push origin main
```

### 3. Enable GitHub Actions

If this is your first time:
1. Go to your GitHub repository
2. Click **Settings** → **Actions**
3. Ensure "Actions" is enabled (should be by default)
4. Under "Workflow permissions," select:
   - ✅ "Read and write permissions"
   - ✅ "Allow GitHub Actions to create and approve pull requests"

### 4. Configure Pages

1. Go to **Settings** → **Pages**
2. Under "Build and deployment":
   - **Source:** Select "GitHub Actions"
   - This tells GitHub to use your workflow file
3. Click Save

---

## Viewing Deployment Status

### Check Workflow Runs

1. Go to your repository
2. Click **Actions** tab
3. You'll see all workflow runs (builds)
4. Each run shows:
   - Timestamp
   - Commit message
   - Status (✅ success or ❌ failed)

### View Logs

Click a run to see details:
- **Build logs** — Output from `hugo` command
- **Deploy logs** — Pages deployment confirmation
- **Artifacts** — Generated `public/` directory

### On-Demand Builds

If you need to rebuild without pushing:
1. Go to **Actions** tab
2. Select the workflow
3. Click **Run workflow** → **Run workflow** (blue button)

---

## Customization

### Change Deployment Branch

If your main branch isn't called `main`:

```yaml
on:
  push:
    branches:
      - master  # or whatever your branch is called
```

### Enable Extended Hugo

If you use SCSS/CSS processing:

```yaml
uses: peaceiris/actions-hugo@v4
with:
  hugo-version: latest
  extended: true  # Enables SCSS, PostCSS, etc.
```

### Add Custom Domain (CNAME)

Already included:
```yaml
cname: borisrapoport.com
```

Update this to your domain. Workflow will create a `CNAME` file automatically.

### Build Baseurl

The workflow dynamically sets baseurl from GitHub Pages:
```yaml
--baseURL "${{ steps.pages.outputs.base_url }}"
```

This ensures relative URLs work correctly. You can override:
```yaml
run: hugo --minify --baseURL "https://borisrapoport.com/"
```

### Environment Variables

If you need to set variables (e.g., for analytics tracking):

```yaml
env:
  ANALYTICS_ID: ""  # Add your ID if needed

- name: Build
  run: hugo --minify
  env:
    MY_VAR: "value"
```

---

## Troubleshooting

### Workflow Shows Red X (Failed)

1. Click the failed run
2. Scroll down to see error logs
3. Common issues:
   - **Hugo version:** Update to `latest`
   - **Branch name:** Check it matches your actual branch
   - **Theme files missing:** Ensure theme is in repo
   - **Invalid baseURL:** Check CNAME is correct

### Build Takes Too Long

- Expected: 30–60 seconds
- If > 5 minutes: Something's wrong
  - Check logs for errors
  - Ensure no heavy processing in content

### Deploy Step Fails

**Usually means GitHub Actions doesn't have write permissions:**
1. Go to **Settings** → **Actions** → **General**
2. Under "Workflow permissions," select "Read and write permissions"
3. Rerun the workflow

### Site Shows Old Version

**GitHub Pages cache issue:**
1. Go to **Actions** tab
2. Find the latest successful deployment
3. Check timestamp
4. If recent but site shows old content:
   - Clear browser cache (Ctrl+Shift+Delete)
   - Hard refresh (Ctrl+Shift+R)
   - Check CloudFlare cache (if using)

---

## Performance Monitoring

### Build Time Tracking

Check your Actions tab to see build trends:
- Builds should consistently take 30–60 seconds
- If increasing, check for new large assets

### Deployment Status

The workflow logs show:
- Artifacts created
- Pages deployment URL
- Build completion time

---

## Security Considerations

### Secrets & Environment Variables

This workflow uses `${{ secrets.GITHUB_TOKEN }}` which is:
- ✅ Safe — Automatically generated per workflow run
- ✅ Limited scope — Only works for this repo
- ✅ Time-limited — Expires after workflow completes

**Do NOT commit sensitive data** (API keys, passwords) to the repo. Use GitHub Secrets instead:

1. Go to **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret**
3. Add secret (e.g., `MY_API_KEY`)
4. Use in workflow: `${{ secrets.MY_API_KEY }}`

### No Credentials in Config

This site doesn't require:
- API keys
- Database passwords
- Private tokens

All third-party integrations (Formspree, CloudFlare) are configured outside the repo.

---

## Advanced: Pull Request Previews

To preview PRs before merging (optional):

```yaml
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

# In build job, add:
- name: Comment PR with preview
  if: github.event_name == 'pull_request'
  uses: actions/github-script@v7
  with:
    script: |
      github.rest.issues.createComment({
        issue_number: context.issue.number,
        owner: context.repo.owner,
        repo: context.repo.repo,
        body: '✅ Build successful! Check Actions tab for logs.'
      })
```

This leaves a comment on PRs confirming the build passed.

---

## Monitoring & Alerts

### GitHub Notifications

GitHub will email you if a workflow fails. To manage:
1. Go to **Settings** → **Notifications**
2. Choose notification preferences
3. Enable alerts for workflow failures

### CI Status Badge

Add to your README:

```markdown
![Deploy Status](https://github.com/brapoport/borisrapoport.com/workflows/Deploy%20Hugo%20Site/badge.svg)
```

---

## Summary

Your workflow:
1. ✅ Automatically builds on every push to `main`
2. ✅ Deploys to GitHub Pages
3. ✅ Sets up custom domain
4. ✅ No manual steps needed
5. ✅ Safe and secure

**That's it.** Push code → site updates automatically. 🚀
