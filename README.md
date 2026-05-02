# ResumeAI PWA — Deployment Guide

## 📁 Files in this package

```
pwa/
├── index.html      ← Main app (everything lives here)
├── manifest.json   ← PWA config (name, icons, colors)
├── sw.js           ← Service worker (offline support)
├── icons/          ← App icons (you need to add these)
│   ├── icon-192.png
│   └── icon-512.png
└── README.md
```

---

## 🎨 Step 1: Create App Icons (Free)

Go to https://favicon.io or https://realfavicongenerator.net
- Upload any image or use text "R" with green (#00FF94) background
- Download and place icon-192.png and icon-512.png in an `/icons/` folder

---

## 🚀 Step 2: Deploy to Vercel (Free, ~2 minutes)

1. Create a free account at https://github.com and https://vercel.com
2. Create a new GitHub repo (e.g. `resumeai`)
3. Upload all 3 files: index.html, manifest.json, sw.js + icons/ folder
4. Go to vercel.com → "Add New Project" → import your GitHub repo
5. Click Deploy — your app goes live at `your-app.vercel.app`

That's it! Free forever on Vercel's hobby plan.

---

## 📱 Step 3: Install on Phone

**Android (Chrome):**
- Visit your Vercel URL in Chrome
- Tap the 3-dot menu → "Add to Home screen"
- OR tap the install banner that appears automatically

**iPhone (Safari):**
- Visit your Vercel URL in Safari
- Tap the Share button (box with arrow)
- Scroll down → "Add to Home Screen"
- Tap Add

The app now appears on the home screen like a native app! ✅

---

## 💰 Step 4: Add Monetization

### Option A — Lemon Squeezy (easiest, handles taxes)
1. Create account at https://lemonsqueezy.com
2. Create a product "$7/month - ResumeAI Pro"
3. Add their payment link to index.html

### Option B — Gumroad
1. Create account at https://gumroad.com
2. Create a digital product
3. Embed their buy button in index.html

### Option C — Stripe (most powerful)
1. Create account at https://stripe.com
2. Use Stripe Checkout links (no backend needed!)
3. Add a "Go Pro" button that opens Stripe checkout

---

## 🔑 Important: API Key

The app currently calls the Anthropic API directly from the browser.
For production, you should:
1. Create a small backend (free on Vercel serverless functions)
2. Store your API key there securely
3. This prevents users from stealing your API key

Backend template (Vercel function — save as `/api/analyze.js`):
```js
export default async function handler(req, res) {
  const response = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'x-api-key': process.env.ANTHROPIC_API_KEY,
      'anthropic-version': '2023-06-01'
    },
    body: JSON.stringify(req.body)
  });
  const data = await response.json();
  res.json(data);
}
```
Then in index.html, change the fetch URL to `/api/analyze` instead of the Anthropic URL directly.

---

## 📣 Step 5: Get First Users (Free)

1. Post on r/resumes, r/jobs, r/cscareerquestions
2. Share on LinkedIn: "I built an AI resume analyzer"
3. Launch on ProductHunt (free)
4. DM people who post "resume help" on Twitter/X

---

## 💡 Pricing Suggestion

- **Free**: 3 analyses per day
- **Pro $7/month**: unlimited analyses + PDF export + cover letter generator

Even 50 paying users = $350/month 🎉
