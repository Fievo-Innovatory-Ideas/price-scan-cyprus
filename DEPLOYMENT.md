# Deploying the portfolio site — step by step (Windows CMD)

Goal: the site live at **https://pricescan.fievo.com** via Vercel.
A **separate repo** — never mix the portfolio into `price-comparison-app`.

## Step 0 — preview locally (no tools needed)

Open the `portfolio-site` folder in Explorer and double-click `index.html`.
The whole site works from disk. Check all three pages before publishing.

## Step 1 — copy the site out of the Claude project folder

Open Command Prompt and run:

```
xcopy "C:\Users\mpapa\Documents\Claude\Projects\Price Comparison Tool\portfolio-site" C:\Users\mpapa\portfolio-site\ /E /I
```

then

```
cd C:\Users\mpapa\portfolio-site
```

Optional: delete `images\logo-source.png` from the copy (4.6 MB master file, not needed online).

## Step 2 — create the GitHub repo

1. Go to https://github.com/new
2. Repository name: `portfolio-site`
3. Set it to **Public**
4. Do NOT tick "Add a README" (we have one)
5. Click **Create repository**

## Step 3 — push the code

One line at a time (replace `YOUR-GITHUB-USERNAME` in the fifth command):

```
git init
```

```
git add .
```

```
git commit -m "PriceScan Cyprus portfolio site"
```

```
git branch -M main
```

```
git remote add origin https://github.com/YOUR-GITHUB-USERNAME/portfolio-site.git
```

```
git push -u origin main
```

Pause here and confirm the files appear on the GitHub page.

## Step 4 — connect Vercel

1. Go to https://vercel.com and log in (same account as the app)
2. **Add New… → Project** → pick `portfolio-site` → **Import**
3. Framework Preset shows "Other" — correct, leave everything default
4. Click **Deploy**

You get a URL like `portfolio-site-xxxx.vercel.app`. Check all three pages.
From now on, every `git push` redeploys automatically.

## Step 5 — add the subdomain in Vercel

1. In the Vercel project: **Settings → Domains**
2. Type `pricescan.fievo.com` → **Add**
3. Vercel shows the DNS record it needs — typically a **CNAME** for `pricescan`
   pointing to `cname.vercel-dns.com`. Keep this tab open.

## Step 6 — add the DNS record in cPanel

1. Log in to the cPanel for fievo.com
2. Find **Zone Editor** (sometimes "Advanced DNS Zone Editor")
3. Click **+ CNAME Record** and enter:
   - **Name:** `pricescan` (cPanel may auto-complete it to `pricescan.fievo.com.`)
   - **Record / target:** exactly what Vercel showed (e.g. `cname.vercel-dns.com`)
4. Save. Do NOT touch any other records — the existing site and email depend on them.
5. Back in the Vercel Domains tab, wait for the check to turn green
   (minutes to a few hours). SSL is provisioned automatically.

## Step 7 — final checks

- [ ] https://pricescan.fievo.com loads, all three pages, on your phone too
- [ ] `https://` padlock shows
- [ ] CV downloads from the contact section (and you're OK with the phone number in it being public)
- [ ] Add the URL to your CV, LinkedIn profile, and email signature

## Updating the site later

Edit files in `C:\Users\mpapa\portfolio-site`, then:

```
cd C:\Users\mpapa\portfolio-site
```

```
git add .
```

```
git commit -m "Update portfolio"
```

```
git push
```

Live in ~30 seconds.
