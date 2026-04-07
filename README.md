# The Loop

Landing page for The Loop — a DJ learning community.

## Local development

Open `index.html` directly in your browser, or run a local server for reliable behavior:

```bash
npx serve .
```

Then visit `http://localhost:3000`.

## Deploying

Push to `main`. GitHub Pages serves directly from the repo root — no build step needed.

First-time setup: in the repo Settings → Pages → Source, set branch to `main`, folder to `/`.

## Switching from waitlist to Discord

When the Discord server is ready:

1. In `index.html`, find the two `<!-- WAITLIST MODE -->` blocks and remove them
2. Find the two `<!-- DISCORD MODE -->` blocks and uncomment them
3. Replace `DISCORD_INVITE_URL` with the actual Discord invite link
4. Push to `main`

## Setting up the waitlist form (Formspree)

1. Create an account at [formspree.io](https://formspree.io)
2. Create a new form — name it "The Loop Waitlist"
3. Copy the form ID (the part after `/f/` in the endpoint URL)
4. In `index.html`, replace `XXXXXXXX` in `action="https://formspree.io/f/XXXXXXXX"` with your form ID
5. Push and test with a real email submission

## Custom domain (when ready)

1. Create a `CNAME` file in the repo root with just your domain:
   ```
   theloop.community
   ```
2. Configure DNS at your registrar:
   - **Apex domain**: 4 `A` records → `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
3. In repo Settings → Pages → Custom domain, enter your domain
4. GitHub provisions HTTPS automatically (may take up to 24h)

## Brand colors

Accent color is a placeholder (`#a78bfa`). Update the `--accent` and `--accent-dim` variables in `styles.css` once brand colors are finalized.
