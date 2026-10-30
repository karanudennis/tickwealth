# TickWealth (revised)

Static site — no build step. Open `index.html` through any web server (GitHub Pages, Netlify, `python3 -m http.server`).
WebSockets to Deriv do not work from some `file://` setups, so use a server.

## Files
- `core.js` / `core.css` – shared engine: reconnecting sockets, live tick feed, correct last-digit maths (uses Deriv `pip_size`), paper + live trading, account modal, canvas chart.
- `digitpage.js` – builder used by Over/Under, Even/Odd and Matches/Differs.
- `index, rise-fall, over-under, even-odd, matches-differs, analyzer, bots-library, settings .html`
- `config.js` – premium / M-Pesa switches (payments are OFF by default).

## AI coach
- Floating "✦ AI coach" on every page. It reads derived numbers only (digit frequencies, session, limits — never tokens), explains them, and **cannot place trades**.
- Works out of the box with an on-device explainer. For full AI answers: run `server/ai-proxy.js` (Node 18+, no packages):
  `ANTHROPIC_API_KEY=sk-ant-... ALLOWED_ORIGIN=https://yoursite.com node server/ai-proxy.js`, then set `aiEndpoint` in `config.js`
  (or Settings → AI server URL). The key never goes in the browser. Rate-limited, size-capped, system prompt forbids predictions/profit claims.

## Deriv login
- "Log in with Deriv" uses Deriv's OAuth redirect. You must register your own app at api.deriv.com with this site's URL as the redirect, then put the app id in Settings (or `DEF.appId` in `core.js`). Multiple accounts returned by Deriv appear in an account switcher; demo is preferred on first login.
- Or paste an API token (Read + Trade only).

## Landing page
`index.html` embeds the real tools in a live preview panel (`?embed=1`, always paper mode, no AI/account UI).

## Trading modes
- **Paper (default):** live prices + real quoted payouts, virtual balance, settled on real ticks.
- **Deriv account:** paste an API token (Read + Trade scopes only; start with a Demo token). Token lives in sessionStorage unless "Remember" is ticked.
- Limits in Settings (max stake, session stop-loss, confirm) apply to manual, auto and bot trades.

## Before going public — checklist
1. Register your own Deriv app id (api.deriv.com) and put it in Settings / `DEF.appId` in `core.js`. Verify the WebSocket endpoint against Deriv's current docs.
2. Premium bots / M-Pesa: the browser can never verify a payment. To charge for bots you need a backend that:
   - `POST /stkpush {phone, amount, product}` → calls Safaricom Daraja STK push, returns `{checkoutId}`
   - `GET /status?id=<checkoutId>` → `{paid:true, unlock:"<signed token>"}` / `{failed:true,error}` after the Daraja callback
   - serves any premium-only files (e.g. XML) only to requests carrying a valid token.
   Then set `paymentsEnabled:true` and `mpesaApi` in `config.js`. Never put Daraja secrets in front-end code.
3. Keep the risk wording. Don't advertise returns ("+127%/month") — synthetic indices are random.
4. Add your own privacy policy / terms and check advertising rules for trading products in Kenya.

## Deriv login (updated for Deriv's new API)
1. Sign in at https://developers.deriv.com and register an app of type PAT. Put its App ID in Settings (or `appId` in `core.js`). Old app IDs such as 1089 do not work for login.
2. Create a Personal Access Token with the `trade` scope only and paste it in the account window.
3. Market data uses the public endpoint and needs no login.

## Advisor
`advisor.js` adds an Advisor button on every tool page: true win chance vs the payout break-even, expected value, how unusual recent ticks are, a rule alert with a 10-second countdown, and paper-trade tracking. It never predicts ticks and never places trades.

## Playbook
`playbook.html` lists 10 strategies with entry rules, true odds, a test against random entries, arm-able rule alerts with a 10-second countdown, and a Trade now button (paper by default).

## Landing page
The new `index.html` is the landing page. The previous home page is kept as `index-old.html`. All pages share the same background through `core.css`.

## Updates in this build
- **Deriv login:** the "Log in with Deriv" button now finishes linking the account after Deriv returns (token -> accounts -> one-time link). If it still fails, the toast shows the reason.
- **Digit circles:** rank colours (top 3 green, bottom 3 red/orange/amber, muted if within normal variation), 1000-tick window, and a moving cursor on the latest digit.
- **Playbook:** notes for each market type.
- **Bots (`bots-library.html`):** each bot is independent JSON with its own market, contract, entry rule, stop-loss, take-profit, max trades and optional Martingale (off by default, capped). Add, delete, export and upload bots. The previous page is kept as `bots-library-old.html`.
- **ea/** holds MetaTrader 4 and 5 source files (RiskGuard and SimpleMA). They are untested: compile in MetaEditor and test on demo only.

## Logo
`logo.svg` (full), `logo-mark.svg` and `favicon.svg`. The mark is used in the top bar and as the favicon; the full logo is on the landing page.
