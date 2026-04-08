# CloudFlare Setup — DNS, CDN, & Security Configuration

Complete step-by-step guide for setting up CloudFlare to serve your Hugo site with DNS, CDN caching, and SSL.

---

## Table of Contents
1. [CloudFlare Basics](#cloudflare-basics)
2. [Add Your Domain](#add-your-domain)
3. [Configure Nameservers](#configure-nameservers)
4. [DNS Records](#dns-records)
5. [SSL/TLS Configuration](#ssltls-configuration)
6. [Caching & Performance](#caching--performance)
7. [Security Rules](#security-rules)
8. [Verify Setup](#verify-setup)
9. [Troubleshooting](#troubleshooting)

---

## CloudFlare Basics

**What is CloudFlare?**
- DNS provider (routes your domain to servers)
- CDN (caches & serves content faster)
- SSL/TLS provider (HTTPS security)
- Security layer (DDoS protection, firewall)

**Why use it?**
- ✅ Free tier sufficient for personal sites
- ✅ Automatic HTTPS
- ✅ Global CDN speeds up content delivery
- ✅ Built-in security (no extra setup needed)
- ✅ Easy DNS management

**Cost:** Free tier covers everything you need.

---

## Add Your Domain

### 1. Create CloudFlare Account

1. Go to https://dash.cloudflare.com/signup
2. Sign up with email
3. Verify email
4. You're in the dashboard

### 2. Add Your Domain

1. Click **+ Add a site** (big button on dashboard)
2. Enter: `borisrapoport.com`
3. Click **Add site**
4. Select plan: **Free** ($0/month)
5. Click **Continue**

CloudFlare will scan your existing DNS records (if any). This takes ~1 minute.

### 3. Review Suggested Records

CloudFlare shows DNS records it found. You'll replace these with records pointing to GitHub Pages:

- ✓ Keep existing email records (if you have any)
- ✗ Delete old nameserver records
- ✓ We'll add GitHub Pages records in the next step

---

## Configure Nameservers

### 1. Update Nameservers at Your Registrar

CloudFlare gives you two nameserver addresses. You'll update these at your domain registrar.

**CloudFlare will show you:**
```
Nameserver 1: xxx.ns.cloudflare.com
Nameserver 2: yyy.ns.cloudflare.com
```

Copy these values.

### 2. Go to Your Registrar

Where you bought `borisrapoport.com` (Namecheap, GoDaddy, Google Domains, etc.):

1. Log in
2. Find your domain
3. Go to **Manage Domain** or **DNS Settings**
4. Find **Nameservers** section
5. Change from registrar's nameservers to CloudFlare's:
   - **Nameserver 1:** xxx.ns.cloudflare.com
   - **Nameserver 2:** yyy.ns.cloudflare.com
6. Save changes

⏰ **Wait 15–60 minutes** for nameserver changes to propagate.

**To check status:** Go back to CloudFlare, it will tell you when nameservers are active.

---

## DNS Records

Once nameservers are active, you'll manage DNS in CloudFlare.

### 1. Go to DNS Records

In CloudFlare dashboard:
1. Click your domain (`borisrapoport.com`)
2. Left sidebar → **DNS** → **Records**

### 2. Add Records for GitHub Pages

You need these **A records** (pointing to GitHub Pages):

```
Type: A
Name: @
Content: 185.199.108.153
TTL: Auto
Proxy: Proxied (orange cloud)

Type: A
Name: @
Content: 185.199.109.153
TTL: Auto
Proxy: Proxied

Type: A
Name: @
Content: 185.199.110.153
TTL: Auto
Proxy: Proxied

Type: A
Name: @
Content: 185.199.111.153
TTL: Auto
Proxy: Proxied
```

**How to add:**
1. Click **+ Add record**
2. Fill in fields as above
3. Click **Save**
4. Repeat for all 4 A records

### 3. Add CNAME for www

```
Type: CNAME
Name: www
Content: brapoport.github.io
TTL: Auto
Proxy: Proxied (orange cloud)
```

### 4. Final DNS List

After setup, your records should look like:

| Type | Name | Content | Proxy |
|------|------|---------|-------|
| A | @ | 185.199.108.153 | Proxied |
| A | @ | 185.199.109.153 | Proxied |
| A | @ | 185.199.110.153 | Proxied |
| A | @ | 185.199.111.153 | Proxied |
| CNAME | www | brapoport.github.io | Proxied |

**Note:** The "Proxy: Proxied" setting (orange cloud) means CloudFlare caches and serves your content. This is what we want.

---

## SSL/TLS Configuration

### 1. Enable Automatic HTTPS

1. In CloudFlare dashboard, go to **SSL/TLS** (left sidebar)
2. Look for **Overview** tab
3. **SSL/TLS encryption mode:** Set to **Full** or **Full (strict)**
   - **Full:** CloudFlare → GitHub (encrypted one way)
   - **Full (strict):** End-to-end encrypted (recommended)
4. Click Save

### 2. Enable HTTPS Redirect

1. Still in **SSL/TLS**
2. Go to **Edge Certificates** tab
3. Turn **ON** → "Always Use HTTPS"
4. This forces all HTTP requests to HTTPS

### 3. HTTP to HTTPS Redirect (Double-Check)

In GitHub:
1. Go to repository **Settings** → **Pages**
2. ✅ Check **Enforce HTTPS** is enabled

This creates a second layer of HTTPS enforcement.

### 4. Verify Certificate

Wait 5–10 minutes for CloudFlare to issue SSL certificate.

**Check status:**
1. Go to **SSL/TLS** → **Edge Certificates**
2. You should see: "Universal SSL certificate active"

If it says "Pending," wait a bit longer.

---

## Caching & Performance

### 1. Configure Cache

1. Go to **Caching** (left sidebar)
2. **Cache Level:** Set to **Cache Everything**
3. **Browser Cache TTL:** 4 hours (or your preference)
4. Click Save

This tells CloudFlare to cache your static HTML/CSS/JS files.

### 2. Purge Cache (When Needed)

When you update your site:
1. Go to **Caching** → **Purge Cache**
2. Click **Purge Everything**
3. Wait ~30 seconds

This clears CloudFlare's cache so users see the new version immediately.

### 3. Page Rules (Advanced Caching)

Optional: Set specific caching rules for different paths:

1. Go to **Rules** → **Page Rules** (if available in your plan)
2. Create rule:
   ```
   URL: borisrapoport.com/projects/*
   Cache Level: Cache Everything
   Browser Cache TTL: 1 day
   ```

This caches project pages longer than the homepage.

---

## Security Rules

### 1. Enable Security Features (Default)

CloudFlare automatically enables:
- ✅ DDoS Protection (free)
- ✅ Bot Management (free tier)
- ✅ Firewall (free tier)

You don't need to configure anything — it's on by default.

### 2. Security Level (Optional)

1. Go to **Security** → **Settings**
2. **Security Level:** Set to **Medium** or **High**
   - **Medium:** Blocks obvious threats, allows most traffic
   - **High:** Stricter, might block some legitimate traffic
3. Click Save

### 3. Rate Limiting (Optional)

To protect contact form from spam:

1. Go to **Security** → **Rate Limiting** (if available)
2. Create rule:
   ```
   URL path: /contact/
   Requests: 10 per minute per IP
   Response: 429 Too Many Requests
   ```

This limits form submissions to 10 per minute per visitor.

---

## Content Security Policy (CSP)

CloudFlare can inject CSP headers for you (optional):

1. Go to **Security** → **HTTP Header Options** (if available)
2. Add custom headers:
   ```
   X-Frame-Options: SAMEORIGIN
   X-Content-Type-Options: nosniff
   Referrer-Policy: strict-origin-when-cross-origin
   ```

This adds security headers to every response.

---

## Verify Setup

### 1. Test HTTPS

1. Open browser to https://borisrapoport.com
2. You should see:
   - ✅ No SSL warnings
   - ✅ Lock icon in address bar
   - ✅ Site loads normally

### 2. Check DNS Propagation

Use a DNS checker:
1. Go to https://dnschecker.org
2. Enter `borisrapoport.com`
3. Should show CloudFlare IPs (e.g., `1.2.3.4`)

### 3. Verify HTTPS Redirect

Try accessing via HTTP:
1. Go to http://borisrapoport.com (no S)
2. Browser should auto-redirect to https://borisrapoport.com
3. Page loads correctly

### 4. Check CloudFlare Status

In CloudFlare dashboard:
1. Click your domain
2. Look for **Status Page** (top right)
3. Should show:
   - ✅ Nameservers active
   - ✅ SSL certificate active
   - ✅ All systems operational

### 5. Email Test (If You Added Email Records)

If you use email with your domain:
1. Send yourself a test email to hello@borisrapoport.com
2. Check it arrives in your inbox
3. CloudFlare should route it correctly

---

## Troubleshooting

### DNS Not Resolving

**Problem:** Site shows "can't reach this page"

**Solutions:**
1. **Check nameservers:** Go to dnschecker.org
   - Should show CloudFlare IPs
   - If showing old registrar IPs, wait 30–60 min
2. **Check CloudFlare status:** Dashboard should show nameservers active
3. **Try different DNS:**
   - Flush local DNS cache:
     - Windows: `ipconfig /flushdns`
     - Mac: `dscacheutil -flushcache`
4. **Wait longer:** Nameserver changes can take up to 24 hours

### HTTPS Not Working

**Problem:** Browser shows "Not Secure" or SSL errors

**Solutions:**
1. **Wait:** CloudFlare SSL certificate takes 5–10 minutes
2. **Check SSL status:** In CloudFlare, go to SSL/TLS → Edge Certificates
   - Should show "Universal SSL certificate active"
3. **Check GitHub settings:** Go to repo Settings → Pages
   - ✅ "Enforce HTTPS" should be ON
4. **Clear browser cache:** Hard refresh (Ctrl+Shift+R)

### Site Shows Old Version

**Problem:** You updated your site but old version shows

**Solutions:**
1. **Purge CloudFlare cache:**
   - CloudFlare dashboard → **Caching** → **Purge Cache** → **Purge Everything**
   - Wait ~30 seconds
2. **Clear browser cache:**
   - Hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)
3. **Check GitHub Actions:** Make sure deployment succeeded

### www Subdomain Doesn't Work

**Problem:** https://www.borisrapoport.com shows 404 but https://borisrapoport.com works

**Solutions:**
1. **Check CNAME record:**
   - Should exist: `www` → `brapoport.github.io`
   - If missing, add it (see [DNS Records](#dns-records))
2. **Check GitHub:** Repo Settings → Pages
   - Custom domain should be `borisrapoport.com`
   - GitHub automatically handles `www` subdomain
3. **Purge cache:** Purge everything in CloudFlare

### Contact Form Getting Spam

**Problem:** You're receiving spam form submissions

**Solutions:**
1. **Enable rate limiting:**
   - CloudFlare → **Security** → **Rate Limiting**
   - Limit to 10 submissions per minute per IP
2. **Use Formspree spam filter:**
   - Log in to Formspree
   - Check "Spam filter" is enabled
3. **Add reCAPTCHA** (future enhancement):
   - Add reCAPTCHA v3 to contact form
   - Prevents bot submissions

---

## CloudFlare Page Rules (Advanced)

For fine-tuned control, use Page Rules:

### Example 1: Cache Static Assets Longer

```
URL: borisrapoport.com/images/*
Cache Level: Cache Everything
Browser Cache TTL: 1 month
```

### Example 2: Don't Cache Contact Form

```
URL: borisrapoport.com/contact/*
Cache Level: Bypass
```

### Example 3: Redirect Old URLs

```
URL: borisrapoport.com/old-project/*
Forward URL: 301 Permanent to borisrapoport.com/projects/
```

---

## Performance Monitoring

### CloudFlare Analytics

1. Go to **Analytics** (left sidebar)
2. You'll see:
   - **Requests:** How many people visited
   - **Bandwidth:** How much data served
   - **Threats blocked:** Security events
3. Monitor these to understand traffic patterns

### Lighthouse Audit

Check site performance:
1. Visit https://borisrapoport.com
2. Open Chrome DevTools (F12)
3. Click **Lighthouse** tab
4. Run audit
5. Target scores:
   - Performance: 90+
   - Accessibility: 95+
   - Best Practices: 90+
   - SEO: 100

CloudFlare CDN should improve Performance score due to faster content delivery.

---

## Summary Checklist

- [ ] Created CloudFlare account
- [ ] Added domain to CloudFlare
- [ ] Updated nameservers at registrar
- [ ] Waited 15–60 minutes for propagation
- [ ] Added A records for GitHub Pages (4 total)
- [ ] Added CNAME record for www subdomain
- [ ] Enabled SSL/TLS (Full or Full Strict)
- [ ] Enabled "Always Use HTTPS"
- [ ] Set Cache Level to "Cache Everything"
- [ ] Verified HTTPS works (lock icon)
- [ ] Tested DNS resolution (dnschecker.org)
- [ ] Confirmed site loads on all URLs

**You're done!** Your site is now served through CloudFlare's global CDN with automatic HTTPS. 🚀

---

## Next Steps

1. **Monitor traffic:** Check CloudFlare analytics weekly
2. **Purge cache on updates:** When you push new code, purge cache
3. **Update documentation:** Record your CloudFlare settings
4. **Test regularly:** Verify HTTPS and DNS still work

See **[MAINTENANCE.md](MAINTENANCE.md)** for ongoing management.
