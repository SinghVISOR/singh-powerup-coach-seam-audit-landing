# GitHub Upload — Toolkit Page Deploy

**Repo:** `https://github.com/SinghVISOR/singh-powerup-coach-seam-audit-landing`
**Branch:** main (auto-deploys to Vercel → theseamlinemethod.com)
**Time to ship:** ~10 minutes including verification.

---

## What you're uploading

| File in this folder | Goes to repo path | Resulting URL |
|---|---|---|
| `index.html` | `/index.html` (overwrites existing root) | `https://theseamlinemethod.com/` |
| `toolkit/index.html` | `/toolkit/index.html` (new folder + file) | `https://theseamlinemethod.com/toolkit/` |

That's it. Two files. No config changes, no `vercel.json` edits, no build step.

---

## Why the folder path matters

Vercel serves `/toolkit/index.html` at the URL `/toolkit/` automatically — that's the convention for static sites. **Do not** rename it to `toolkit.html` at the repo root; that would serve at `/toolkit.html` (uglier, breaks the nav link I wrote, and gives you a worse URL for sharing in email).

The folder structure you want in the repo after this push:

```
singh-powerup-coach-seam-audit-landing/
├── index.html                ← root landing (updated)
├── SEAMline_Field_Kit_v1.pdf ← existing, untouched
├── toolkit/
│   └── index.html            ← NEW
└── (other existing files)
```

---

## What changed in the root `index.html`

Three surgical edits — nothing else moved. If you want to diff against the existing version: only these blocks are different.

1. **Nav (in `<header class="site">`):** added `<a href="/toolkit/">The toolkit</a>` between "The audit" and "Pricing".
2. **Gate strip section:** added a second `<aside class="fieldkit-gate">` right after the existing Field Kit gate strip. Same component, white background (`var(--paper)`) instead of bone-deep, parallel framing — "Past the Field Kit but $15K isn't this quarter?" → toolkit CTA.
3. **Pricing closing copy:** added a second line referencing the toolkit as a lateral step.

No CSS changes. No script changes. The Field Kit form, the Seam Audit intake, the analytics, and all the legal links are untouched.

---

## What's in the new `toolkit/index.html`

- Full standalone product page styled to match the root site (same brand tokens, same fonts, same header/footer grammar).
- **Live $349 buy button wired** to your Lemon Squeezy checkout: `https://fabricpress.lemonsqueezy.com/checkout/buy/d101bc49-0dce-4d5f-a27a-b6853413242f?embed=1&media=0`
- Single-tier pricing for v1 (per SKU1 launch doc §4.2 — defer the multi-org and firm tiers until single-org has shipped 20+ units). Multi-org and firm pricing footnote routes to `mailto:info@singhpowerupcoach.com`.
- Lemon Squeezy overlay script in `<head>` (`https://app.lemonsqueezy.com/js/lemon.js`).
- Buttons use `class="lemonsqueezy-button"` which is the hook LS's script looks for. The `?embed=1&media=0` URL params trigger overlay mode.

---

## Upload — three options

### Option A — GitHub web UI (fastest, no Git needed) — recommended for this push

1. Go to `https://github.com/SinghVISOR/singh-powerup-coach-seam-audit-landing`.
2. **Replace root `index.html`:**
   - Click `index.html` in the file list → click the pencil icon (top right) → delete all content → paste content from `repo-upload/index.html` in this folder → scroll down → commit message: `feat: add toolkit page link to nav + gate strip + pricing closing` → "Commit directly to the main branch" → Commit changes.
3. **Add the new `toolkit/index.html`:**
   - From the repo root, click "Add file" → "Create new file".
   - In the filename field, type `toolkit/index.html` (typing the `/` automatically creates the `toolkit` folder).
   - Paste content from `repo-upload/toolkit/index.html` in this folder.
   - Commit message: `feat: ship Fracture Diagnostic Toolkit product page (SKU #1)` → "Commit directly to the main branch" → Commit new file.
4. Watch Vercel deploy: go to your Vercel dashboard → the project → Deployments. You'll see a build start within ~10 seconds of the second commit. Static-only sites deploy in 30–60 seconds.

### Option B — GitHub Desktop

1. Pull latest main.
2. Drag `index.html` (this folder's version) into the repo root, overwriting the existing.
3. Drag the entire `toolkit/` folder (with `index.html` inside) into the repo root.
4. Commit both as one commit: `feat: ship SKU #1 toolkit page + nav/gate updates on root`.
5. Push to origin.

### Option C — Git CLI

```bash
cd singh-powerup-coach-seam-audit-landing
# from this Commerce folder, copy both files into the repo
cp /path/to/repo-upload/index.html ./index.html
mkdir -p ./toolkit
cp /path/to/repo-upload/toolkit/index.html ./toolkit/index.html

git add index.html toolkit/index.html
git commit -m "feat: ship SKU #1 toolkit page + nav/gate updates on root"
git push origin main
```

---

## Verification — 5 checks after Vercel finishes deploying

Open an **incognito window** so you're not seeing cached pages.

1. **`https://theseamlinemethod.com/`** loads → nav now shows "The toolkit" → both gate strips appear after the hero → pricing closing has the new toolkit line.
2. **Click "The toolkit" in the nav** → routes to `/toolkit/` cleanly.
3. **`https://theseamlinemethod.com/toolkit/`** loads with the full toolkit page → hero shows $349 → ladder strip shows "You are here" on the middle rung.
4. **Click the big "Buy the toolkit — $349" button** → Lemon Squeezy overlay opens with your product. **Do not** complete the purchase (use a 100%-off test discount in LS if you want to verify the full flow — see Step 8 of the LS setup checklist).
5. **Back button works** from the overlay → returns you to the page in the same scroll position.

If the LS overlay doesn't appear and instead redirects to a full LS-hosted page: that's still functional, just not the polished UX. The `class="lemonsqueezy-button"` + the `lemon.js` script in `<head>` should trigger overlay. If it doesn't, the most likely cause is the URL format. To switch to true overlay, in LS go to Product → Share → **Overlay** tab (not Direct checkout) → copy that URL — it'll look like `https://fabricpress.lemonsqueezy.com/buy/[uuid]?embed=1` instead of `/checkout/buy/[uuid]`. Swap the two `href`s in `toolkit/index.html` (hero button + pricing button) and re-push.

---

## What I deliberately did not change

- Your Field Kit form and its mailto flow.
- Your Seam Audit intake form.
- The pricing module's 3 tiers ($7,500 / $15,000 / $25,000). Toolkit lives on its own page, not in this module.
- The capacity strip, About strip, contact section, footer.
- Any legal links or copyright text.
- Any of your existing JavaScript.

The root page is **additive only** — three small additions, zero removals.

---

## After it's live

1. Test purchase using a 100%-off discount code (LS Dashboard → Discounts → New).
2. Confirm the post-purchase email arrives with all 4 download links + license key.
3. Mark the test order as `Test` in LS so it doesn't pollute revenue reports.
4. Soft launch via warm channel (don't announce publicly yet) — add the P.S. to your existing warm templates pointing at `theseamlinemethod.com/toolkit`.
5. Watch for 48 hours, then announce in Issue 0 of The Seam newsletter.

---

— Saved 2026-05-28
