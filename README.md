# Health Quick Check — Telegram Mini App Starter

## What's here
- `index.html` — the Mini App frontend (Telegram Web App SDK wired in, plus a Stars payment button)
- `bot.js` — bot backend (Telegraf): `/start` command, menu button, Stars invoice creation, payment handling
- `package.json` — backend dependencies

## Setup

1. **Host the frontend**
   - Deploy `index.html` to any HTTPS host (Vercel, Netlify, GitHub Pages, Cloudflare Pages).
   - Note the resulting URL, e.g. `https://healthquickcheck.vercel.app`.

2. **Configure the backend**
   ```
   npm install
   ```
   Create a `.env` file:
   ```
   BOT_TOKEN=<your token from BotFather>
   MINI_APP_URL=https://healthquickcheck.vercel.app
   PORT=3000
   ```
   Deploy `bot.js` somewhere it can run persistently (Railway, Render, Fly.io, a VPS).
   Update the `fetch` URL in `index.html` (`your-backend.example.com`) to your deployed backend URL.

3. **Register the Mini App with BotFather**
   - `/mybots` → select your bot → **Bot Settings** → **Mini App** → set the same HTTPS URL.
   - Optionally `/setmenubutton` to make it launch from the chat's menu button (also handled automatically by `bot.js`).

4. **Run the bot**
   ```
   npm start
   ```

5. **Test**
   - Open your bot in Telegram, tap **Open App** or send `/start`.
   - Tap "Unlock Premium" to test the Stars payment flow (works in real chats; Stars are Telegram's built-in currency, no bank setup needed).

## Monetization notes
- `XTR` currency = Telegram Stars, no payment provider needed — Telegram handles it.
- For real-currency payments instead, get a `provider_token` from a payment provider via BotFather (`/mybots` → Payments) and swap `provider_token: ''` for that value.
- Always verify `initData` server-side (done in `verifyInitData`) before trusting any user info sent from the frontend.

## Next steps
- Replace the placeholder cards in `index.html` with your actual health check-in UI.
- Add a database (e.g. Postgres/SQLite) to store check-ins and unlock status per user.
- Add `bot.telegram.setWebhook(...)` and switch from polling to webhooks for production.
