Listo, corregido. Aquí tienes la versión actualizada:
Markdown# 🌿 GreenShort

**Self-hosted URL shortener that runs entirely on Cloudflare.**  
No servers • No external databases • No dependencies  

Everything lives inside your Cloudflare account using **Pages**, **D1**, **Workers AI** and **Analytics Engine**.

<p align="center">
  <a href="https://github.com/GS-URL/GreenShort">
    <img src="https://img.shields.io/badge/GitHub-Repo-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub">
  </a>
  &nbsp;
  <a href="https://greenshort.pages.dev">
    <img src="https://img.shields.io/badge/Presentation-00C853?style=for-the-badge&logo=cloudflare&logoColor=white" alt="Presentation">
  </a>
  &nbsp;
  <a href="https://github.com/GS-URL/GreenShort/fork">
    <img src="https://img.shields.io/badge/Fork-FF6D00?style=for-the-badge&logo=github&logoColor=white" alt="Fork">
  </a>
</p>

---

## What is GreenShort?

GreenShort is a URL shortener with an admin dashboard, designed to be deployed in minutes and operated with zero maintenance.

It generates short links, builds link-in-bio style hubs, tracks clicks with analytics, and offers password and captcha protection.  
The frontend, backend, and database all run inside Cloudflare.

Built for people who want their own shortener without relying on third-party services, without paying subscriptions, and without worrying about servers.

You only need a Cloudflare account, a domain (or the free Pages subdomain), and to follow the setup steps.

---

## Features

| Feature | Description |
|---------|-------------|
| **Short links** | Custom or random slug. Supports nested routes like `my_brand/promo/summer` |
| **Link hubs** | Link-in-bio style pages with multiple buttons, title, bio and color palette |
| **AI-generated slugs** | Analyzes page content and suggests short, descriptive slugs (Workers AI) |
| **Built-in captcha** | Custom visual challenge, no Google reCAPTCHA or external services |
| **Password protection** | Protect any link or hub with a password |
| **Link expiration** | Minutes, hours, days or never |
| **Splat subroutes** | Capture everything after the slug and forward it |
| **Click analytics** | Country, user agent, referrer, IP and timestamp |
| **Storage indicator** | Real-time D1 usage with selectable units |
| **Multi-language** | Spanish, English, Russian, Simplified & Traditional Chinese |
| **Dark theme** | Minimal dark design with green accents |
| **QR Generation** | Generate QR codes easily in a few clicks |

---

## How it works

GreenShort runs as a single Cloudflare Pages project with a catch-all Worker.

1. Visitor hits a URL → Worker checks if the slug exists  
2. Applies rules (password, captcha, expiration, splat)  
3. Redirects to the destination  

All data lives in **D1**. Clicks go to **Analytics Engine**.  
Admin dashboard authenticates with a single `SITE_TOKEN`.

---

## Requirements

- Cloudflare account (free plan is enough)
- Cloudflare Pages project
- D1 database bound as `DB`
- Workers AI binding as `AI`
- Analytics Engine dataset (optional but recommended) bound as `ANALYTICS`

**Environment variables:**

| Variable | Required | Description |
|----------|----------|-------------|
| `SITE_TOKEN` | Yes | Admin password (min. 8 characters) |
| `CF_ACCOUNT_ID` | Yes | Your Cloudflare Account ID |
| `CF_D1_ID` | Yes | D1 database ID |
| `CF_API_TOKEN` | Yes | Token with D1 + Analytics Engine permissions |
| `MAX_SLUG_LENGTH` | No | Default: `20` |
| `MAX_EXPIRATION_DAYS` | No | Default: `365` |
| `AI_MODEL` | No | Recommended: `@cf/moonshot-ai/kimi-k2.5` |

---

## Recommended AI model
@cf/moonshot-ai/kimi-k2.5

Clean, short and contextually accurate slugs. Works great within the free Workers AI quota.

---

## Deployment summary

1. Fork or clone the repository  
2. Create a Cloudflare Pages project linked to the repo  
3. Create a D1 database → bind as `DB`  
4. Create Analytics Engine dataset named `greenshort` → bind as `ANALYTICS`  
5. Add Workers AI binding as `AI`  
6. Set the environment variables  
7. Deploy (migrations run automatically on first request)  
8. Visit `/gs/dashboard` and log in with your `SITE_TOKEN`

**That’s it.** No build step, no external services, no maintenance.

---

## Reserved routes

These cannot be used as slugs:

- `favicon.ico` / `favicon.svg`
- `robots.txt` / `sitemap.xml`
- `gs` / `gs-files` / `api`
- Any slug starting with `_`

---

## Security

- Single admin token stored only in localStorage after login  
- All API endpoints require Bearer token  
- Captchas signed with HMAC + secure cookies (HttpOnly, Secure, SameSite=Strict)  
- Passwords compared server-side  
- Reserved routes validated on both frontend and backend  

**Never expose your `SITE_TOKEN`.** Treat it like a password.

---

## License

Open source. Check the repository for the exact license terms.  
*Currently only supports deployment to Cloudflare Pages.*

<br>

<p align="center">
  <a href="https://github.com/quasvx">
    <img src="https://img.shields.io/badge/GitHub-quasvx-181717?style=for-the-badge&logo=github&logoColor=white" alt="github.com/quasvx">
  </a>
  &nbsp;&nbsp;
  <a href="https://greenshort.pages.dev">
    <img src="https://img.shields.io/badge/Presentation-greenshort.pages.dev-00C853?style=for-the-badge&logo=cloudflare&logoColor=white" alt="greenshort.pages.dev">
  </a>
</p>

<p align="center">
  <b>Made with 💚 by <a href="https://github.com/quasvx">quasvx</a></b>
</p>
