# GitHub Upload — Legal Pages Deploy

**Repo:** `https://github.com/SinghVISOR/singh-powerup-coach-seam-audit-landing`
**Branch:** main (auto-deploys to Vercel → theseamlinemethod.com)
**Time to ship:** ~10 minutes including verification.
**Purpose:** Publish the three legal pages Paddle (and every other payment processor) requires.

---

## What you're uploading

| File in this folder | Goes to repo path | Resulting URL |
|---|---|---|
| `terms/index.html` | `/terms/index.html` (new folder + file) | `https://theseamlinemethod.com/terms/` |
| `privacy/index.html` | `/privacy/index.html` (new folder + file) | `https://theseamlinemethod.com/privacy/` |
| `refund-policy/index.html` | `/refund-policy/index.html` (new folder + file) | `https://theseamlinemethod.com/refund-policy/` |

Three files. Three new folders. No changes to the existing root `index.html`, no changes to `/toolkit/`, no config edits, no `vercel.json` changes, no build step.

---

## Why the folder structure matters

This matches the same convention you used for `/toolkit/` — Vercel serves `/terms/index.html` at the clean URL `/terms/` automatically. Paddle accepts the trailing-slash form, and so do Lemon Squeezy, Stripe, and every other processor.

The folder structure you want in the repo after this push:

```
singh-powerup-coach-seam-audit-landing/
├── index.html                ← existing, untouched
├── SEAMline_Field_Kit_v1.pdf ← existing, untouched
├── toolkit/
│   └── index.html            ← existing, untouched
├── terms/
│   └── index.html            ← NEW
├── privacy/
│   └── index.html            ← NEW
├── refund-policy/
│   └── index.html            ← NEW
└── (other existing files)
```

---

## URLs to paste into Paddle (and any other processor) after deploy

| Paddle field | URL |
|---|---|
| Terms of service | `https://theseamlinemethod.com/terms/` |
| Privacy policy | `https://theseamlinemethod.com/privacy/` |
| Refund policy | `https://theseamlinemethod.com/refund-policy/` |

Paddle's form requires a path (won't accept the bare domain). The trailing-slash form is what works with the folder-based routing.

---

## What's in each file

All three are self-contained HTML files with inline CSS. No external dependencies. They will render in any browser the moment they hit the repo and Vercel finishes deploying.

- **`terms/index.html`** — Terms of Service. Singh PowerUp Coach LLC as merchant. FL governing law, St. Johns County venue. Cross-references the Privacy Policy and Refund Policy by their new URLs. Based on counsel-approved ToS v1.1 (LegalShield, 2026-05-21).
- **`privacy/index.html`** — Privacy Policy. GDPR/UK GDPR rights section, CCPA/CPRA rights section, processor disclosure, international transfer language. Based on counsel-approved Privacy Policy v1.1.
- **`refund-policy/index.html`** — Refund Policy v1.0. Codifies the locked 2026-05-28 all-sales-final decision. EU/UK 14-day withdrawal right expressly waived via consent-to-immediate-delivery clause. Cohort and consulting carve-outs.

All three list `contact@singhpowerupcoach.com` as the customer/legal contact.

---

## Upload — three options

### Option A — GitHub web UI (fastest, no Git needed) — recommended for this push

From `https://github.com/SinghVISOR/singh-powerup-coach-seam-audit-landing`, repeat the same three-step pattern for each of the three folders:

**1. Add `terms/index.html`:**
- From the repo root, click "Add file" → "Create new file".
- In the filename field, type `terms/index.html` (typing the `/` automatically creates the `terms` folder).
- Open `repo-upload/terms/index.html` in this folder, copy the whole file, paste it in.
- Commit message: `feat: publish Terms of Service at /terms/` → "Commit directly to the main branch" → Commit new file.

**2. Add `privacy/index.html`:**
- From the repo root, click "Add file" → "Create new file".
- In the filename field, type `privacy/index.html`.
- Open `repo-upload/privacy/index.html`, copy, paste.
- Commit message: `feat: publish Privacy Policy at /privacy/` → Commit new file.

**3. Add `refund-policy/index.html`:**
- From the repo root, click "Add file" → "Create new file".
- In the filename field, type `refund-policy/index.html`.
- Open `repo-upload/refund-policy/index.html`, copy, paste.
- Commit message: `feat: publish Refund Policy v1.0 at /refund-policy/` → Commit new file.

**4. Watch Vercel deploy:** your Vercel dashboard → the project → Deployments. Each commit triggers a build; static-only sites deploy in 30–60 seconds. After the third commit lands, all three pages will be live.

### Option B — GitHub Desktop

1. Pull latest main.
2. Drag the three folders (`terms/`, `privacy/`, `refund-policy/`) from this `repo-upload/` folder into the repo root.
3. Commit all three folders as one commit: `feat: publish Terms, Privacy, Refund Policy for processor onboarding`.
4. Push to origin.

### Option C — Git CLI

```bash
cd singh-powerup-coach-seam-audit-landing

# from this repo-upload folder, copy the three folders into the repo root
cp -r /path/to/repo-upload/terms ./terms
cp -r /path/to/repo-upload/privacy ./privacy
cp -r /path/to/repo-upload/refund-policy ./refund-policy

git add terms privacy refund-policy
git commit -m "feat: publish Terms, Privacy, Refund Policy for processor onboarding"
git push origin main
```

---

## Verification — 4 checks after Vercel finishes deploying

Open an **incognito window** so you're not seeing cached pages.

1. **`https://theseamlinemethod.com/terms/`** loads → renders cleanly → contact email shows `contact@singhpowerupcoach.com` → links to `/privacy` and `/refund-policy` are present in §14.2 and §6.
2. **`https://theseamlinemethod.com/privacy/`** loads → renders cleanly → GDPR section visible → CCPA section visible → contact email correct.
3. **`https://theseamlinemethod.com/refund-policy/`** loads → renders cleanly → summary block at top is styled (soft tan background, accent rule on left) → EU/UK §6.1 is intact.
4. **Test the mailto links** — click any `contact@singhpowerupcoach.com` link on any of the three pages → your mail client opens with that address pre-filled.

If a page returns 404: the most likely cause is the file landed at the wrong path. From the repo's Code view, navigate into the `terms/` (or `privacy/`, or `refund-policy/`) folder and confirm `index.html` is inside. If it's there but still 404, force-rebuild from the Vercel dashboard (Deployments → ⋯ → Redeploy).

---

## After it's live — paste into Paddle

Go back to your Paddle onboarding form and enter:

- Terms of service: `https://theseamlinemethod.com/terms/`
- Privacy policy: `https://theseamlinemethod.com/privacy/`
- Refund policy: `https://theseamlinemethod.com/refund-policy/`

Paddle will crawl each URL during merchant review. The pages are self-contained HTML with no JavaScript dependencies, so the crawl will succeed on the first try.

---

## What I deliberately did not change

- The root `index.html` (your Seam Audit landing page).
- The `/toolkit/` page (SKU #1 Fracture Diagnostic Toolkit).
- Any existing files in the repo.
- Your Vercel config, domain mapping, or DNS.
- Your Field Kit form, Seam Audit intake form, Calendly links, or analytics.

This push is **additive only** — three new folders, three new files, zero removals or edits.

---

## One thing to set up in parallel

Make sure `contact@singhpowerupcoach.com` is a real mailbox (or forwarder to one you check). All three legal pages route customer and counsel inquiries there. If the address bounces, you have a compliance problem regardless of whether Paddle approves you.

---

— Saved 2026-05-29
*Singh PowerUp Coach LLC*
