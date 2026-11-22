# Lookalike: deploy your own copy

Upload a photo, get similar items. The page runs on its own; Claude's API does the image analysis from a server function, so your key stays private.

## Files
- `public/index.html`: the website. Edit the `AFFILIATE` block at the top of the script to add your Amazon tag.
- `api/analyze.js`: the server function that calls the AI.
- `.env.example`: the settings the server needs.

## Deploy (about 20 minutes, free tier)
1. **Get an API key:** create an account at console.anthropic.com, add a small amount of credit, create a key. In Billing, set a monthly spend limit (for example $10) so a surprise can never cost more.
2. **Put the code on GitHub:** create a free GitHub account, make a new repository, upload everything in this folder.
3. **Deploy on Vercel:** sign up at vercel.com with your GitHub account, click "Add New Project", pick the repository, leave the defaults, and before deploying open "Environment Variables" and add:
   - `ANTHROPIC_API_KEY` = your key
   - `MODEL` = `claude-haiku-5-5`
   - `DAILY_LIMIT` = `10`
4. Click Deploy. You get a public address like `yourproject.vercel.app`.
5. **Custom domain:** buy one (Namecheap, Cloudflare...) and connect it in Vercel > Settings > Domains.

## Earning
- **Affiliate:** join Amazon Associates (and others like Etsy or AliExpress affiliate programs), put your tag in `AFFILIATE.amazonTag`. The disclosure sentence is already on the page; keep it. Check each program's rules and whether you can be paid from Burundi before relying on it.
- **Paid plan (later):** add logins and a payment provider. Check which providers support you in Burundi first (merchant-of-record services such as Lemon Squeezy or Paddle, PayPal, or mobile money for local users).

## Important limits
- `DAILY_LIMIT` is a best-effort counter that resets when the server restarts. For strict limits, add Upstash Redis (free tier) and store counts there.
- Add a short privacy policy page: photos are sent to an AI provider for analysis and are not stored by your site.
