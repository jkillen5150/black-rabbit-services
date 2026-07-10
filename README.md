# Black Rabbit Services

Local services marketplace + Grok assistant for [blackrabbitlawn.com](https://blackrabbitlawn.com).

## Relationship to the marketing site

| Repo | Role |
|------|------|
| **BlackRabbitApp2026** | Marketing site HTML at blackrabbitlawn.com (keep as-is) |
| **black-rabbit-services** | This product: Expo app + FastAPI + Grok chat |
| **BlackRabbitLandscapingApp** | Dev / staging clone of the app |

**You do not rebuild the whole website.** Point a few links (or an iframe) from the existing HTML to this app once it is hosted.

## Website integration (copy-paste)

In `BlackRabbitApp2026/index.html`, set one base URL and use buttons or an iframe:

```html
<script>
  // After you deploy the app, put that public URL here:
  window.BR_APP_URL = 'https://app.blackrabbitlawn.com';
</script>

<!-- Quick links (simplest, recommended first) -->
<section class="marketplace-cta">
  <a class="cta" href="https://app.blackrabbitlawn.com/">Post a free job</a>
  <a class="cta" href="https://app.blackrabbitlawn.com/pros">Find a pro</a>
  <a class="cta" href="https://app.blackrabbitlawn.com/chat">Ask Grok</a>
</section>

<!-- Optional full embed -->
<iframe
  id="br-app"
  title="Black Rabbit Services"
  src="https://app.blackrabbitlawn.com/"
  style="width:100%;min-height:720px;border:0;border-radius:16px;"
  loading="lazy"
  allow="clipboard-write"
></iframe>
```

See `website-embed/snippet.html` for a drop-in block styled like the marketing site.

## Recommended DNS layout

| Host | Points to |
|------|-----------|
| `blackrabbitlawn.com` | Existing GitHub Pages site (BlackRabbitApp2026) |
| `app.blackrabbitlawn.com` | This marketplace frontend (Railway / Render / Fly / Vercel) |
| `api.blackrabbitlawn.com` | FastAPI backend |

Frontend env:

```bash
EXPO_PUBLIC_API_URL=https://api.blackrabbitlawn.com
```

## Run locally

```bash
# API
cd backend && pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000

# Web app
cd frontend && npm install && npm run web
# http://localhost:8081
```

## Source of truth

If this repo is empty or behind, pull from:

https://github.com/jkillen5150/BlackRabbitLandscapingApp

```bash
git clone https://github.com/jkillen5150/BlackRabbitLandscapingApp.git
cd BlackRabbitLandscapingApp
git remote add services https://github.com/jkillen5150/black-rabbit-services.git
git push services main
```
