# myBizStrategies.com

Static marketing + lead-generation site for business-owner financial planning, live at **mybizstrategies.com**.

Flat static HTML (no build step). Hosted on **Netlify**, which auto-deploys on every push to the `main` branch of this repo.

---

## Folder structure

```
mybizstrategies/
├── index.html                  Homepage (Six Domains, Capital Map form, newsletter)
├── capital-map-landing.html    "Three Buckets" landing page (Capital Map form)
├── capital-map-diagnostic.html Printable Socratic diagnostic worksheet (the lead magnet)
├── insights/
│   ├── index.html              Insights hub (article cards + newsletter)
│   └── <article-slug>/         10 article pages
└── README.md                   This file
```

---

## Lead capture (Netlify Forms)

Submissions are collected with **Netlify Forms** - no third-party form service. Two forms exist, each consolidated into a single Netlify bucket regardless of which page it is submitted from:

| Form name (bucket)        | Where it appears                         | Fields                                   |
|---------------------------|------------------------------------------|------------------------------------------|
| `capital-map-diagnostic`  | Homepage `#capital-map`, landing page    | First name, last name, email, situation  |
| `newsletter-subscribe`    | Homepage + Insights hub newsletter box   | Email                                    |

How each form works:
- Marked up with `data-netlify="true"` and a hidden `form-name` input so Netlify detects and stores it at deploy time.
- A hidden `bot-field` honeypot filters spam.
- JavaScript intercepts submit and `fetch()`-posts to `/` (URL-encoded), so there is no page reload - the form swaps to an inline success message on success.

Where leads land:
- Netlify dashboard -> **Forms** -> the bucket name above.
- A notification email is sent to **contact@mybizstrategies.com** on any new submission.

Notes / gotchas for forms:
- Form detection must be enabled once in Netlify (**Project configuration -> Forms**).
- After enabling (or after adding a brand-new form name), a fresh deploy is required before Netlify actually starts persisting submissions. The confirmation email firing is **not** proof the submission was saved - check the Forms dashboard directly.

---

## Editing / updating the site

1. Edit the HTML file directly in GitHub (open the file, click the pencil / use find-and-replace) and commit to `main`. No local setup needed.
2. Netlify redeploys automatically, usually within 30-60 seconds.

**Important deploy gotcha:** the Netlify team ("Advisory OS") can run out of operational credits, which **silently skips production deploys** - the commit succeeds in GitHub, but the live site does not update. If a change does not appear live after a normal wait, open Netlify's **Deploys** tab and look for a banner reading *"Advisory OS is now running on operational credits"* and a deploy marked *"Skipped due to account credit usage exceeded."* Fix: upgrade the team plan or wait for the billing cycle to reset, then manually trigger **Deploy project without cache**.

---

## Domain & SSL

`mybizstrategies.com` is connected to Netlify (custom domain in **Site settings -> Domain management**). Netlify provisions and renews the SSL certificate automatically - no manual steps.

---

## Future: email nurture (when ready)

Netlify Forms only collects and notifies. To add an automated email sequence later, connect a dedicated email platform (e.g. Kit / ConvertKit): create a form there, swap its embed in for the Netlify form, and build a nurture sequence that delivers content automatically. Until then, follow-up is manual from the Netlify Forms inbox.
