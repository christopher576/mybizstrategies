# myBizStrategies — Deployment Guide
## From zero to live at mybizstrategies.com

---

### What's in this folder

```
mybizstrategies/
├── index.html                    ← Homepage (v5)
├── insights/
│   └── index.html                ← Insights page
├── capital-map-thank-you/
│   └── index.html                ← Thank-you page after download
├── assets/
│   └── Capital_Map_Business_Owner.pdf   ← The download
└── README.md                     ← This file
```

---

### Step 1: Set up Formspree (5 minutes)

The Capital Map form needs a Formspree endpoint to collect emails.

1. Go to **formspree.io** and create a free account
2. Click **New Form**
3. Name it "Capital Map Downloads"
4. Copy your form ID — it looks like `xrgjabc1`
5. Open `index.html` and find this line:

```
action="https://formspree.io/f/REPLACE_WITH_YOUR_FORMSPREE_ID"
```

Replace `REPLACE_WITH_YOUR_FORMSPREE_ID` with your actual form ID. Example:

```
action="https://formspree.io/f/xrgjabc1"
```

6. In Formspree settings, enable **Email Notifications** so every submission goes to your inbox
7. Upload the Capital Map PDF to Formspree's file delivery (optional — the direct download link on the thank-you page works without this)

---

### Step 2: Create a GitHub repository (3 minutes)

1. Go to **github.com** and log in
2. Click the **+** icon → **New repository**
3. Name it: `mybizstrategies`
4. Set to **Public**
5. Do NOT initialize with README (you already have one)
6. Click **Create repository**
7. Upload all files: click **uploading an existing file** → drag the entire `mybizstrategies` folder in → click **Commit changes**

---

### Step 3: Deploy on Netlify (5 minutes)

1. Go to **netlify.com** and log in
2. Click **Add new site** → **Import an existing project**
3. Select **GitHub**
4. Find and select the `mybizstrategies` repository
5. Build settings: leave everything blank (static site, no build command needed)
6. Click **Deploy site**
7. Netlify will give you a temporary URL like `random-name-123.netlify.app` — open it and confirm the site looks right

---

### Step 4: Connect your custom domain (10 minutes + 24-48 hours DNS)

**In Netlify:**
1. Go to **Site settings** → **Domain management**
2. Click **Add custom domain**
3. Enter `mybizstrategies.com`
4. Netlify will show you DNS records to add

**At your domain registrar (wherever you bought mybizstrategies.com):**
1. Log in and go to DNS settings
2. Add the records Netlify specifies — typically:
   - An **A record** pointing to Netlify's IP
   - A **CNAME record** for `www` pointing to your Netlify subdomain
3. Remove or update the existing Squarespace DNS records

**Note:** DNS changes take 24-48 hours to fully propagate. During this time the site may be intermittently accessible on both old and new servers. This is normal.

**SSL:** Netlify provisions a free SSL certificate automatically once DNS is connected.

---

### Step 5: Verify everything works

Once live, check each of these:

- [ ] Homepage loads at mybizstrategies.com
- [ ] mybizstrategies.com/insights loads correctly
- [ ] Capital Map form submits and shows success state
- [ ] Thank-you page loads at mybizstrategies.com/capital-map-thank-you
- [ ] PDF downloads correctly from the thank-you page
- [ ] You receive an email notification in Formspree when a test submission is made
- [ ] Site loads correctly on mobile

---

### Future updates

Once the GitHub repo is connected to Netlify, any changes pushed to GitHub automatically redeploy the site. To update content:

1. Edit the HTML file locally (or ask Claude to make changes and download the updated file)
2. Go to your GitHub repo → find the file → click the pencil icon to edit → paste the new content → commit
3. Netlify redeploys automatically within 30-60 seconds

---

### Email platform upgrade (when ready)

Currently the form emails you directly via Formspree. When you're ready to set up proper email nurture:

1. Create a **Kit (ConvertKit)** account at kit.com — free up to 10,000 subscribers
2. Create a form in Kit and get the form embed code
3. Replace the Formspree form in index.html with the Kit form
4. Build a 5-email sequence in Kit that delivers the Capital Map PDF automatically
5. Connect Kit to your domain for professional sending (e.g. hello@mybizstrategies.com)

---

*Built by Claude — Capital Strategy Knowledge Base — Christopher*
