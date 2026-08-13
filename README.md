# Churchill's Boxing Club

The website for Churchill's Boxing Gym — 15 Newport Street, London, SE11 6AJ. Est. 2018. *We will never surrender.*

There is no build step: open `index.html` in a browser, or serve the repo root with any static file server.

- `index.html` — review shell with three tabs: **Original** (the live site, embedded), **New Design** (the redesign), and **What Changed** (the pitch).
- `new-design.html` — the redesigned site itself, fully self-contained.
- `changes.html` — a plain-English page explaining what the redesign changes and why, ending with the offer.
- `Original` tab — embeds https://churchillsboxinggym.co.uk/ so the original is shown exactly as it stands today.
- `logo.svg` — the gym's crest as vector artwork, used across the site.
- `russianwithvladimir/` — a separate one-page site: the Russian with Vladimir
  landing page (Russian Speaking Accelerator). This folder is what the
  Cloudflare deployment publishes — see below.

## Deployment (Cloudflare)

The `russianwithvladimir/` folder is served by Cloudflare Workers as a static
site. Every push to `main` deploys it automatically: the GitHub Actions
workflow in `.github/workflows/deploy.yml` runs `wrangler deploy` against
`wrangler.jsonc`.

One-time setup, then it is hands-off:

1. In the Cloudflare dashboard, create an API token: **My Profile → API
   Tokens → Create Token**, using the **"Edit Cloudflare Workers"** template.
2. Copy your **Account ID** (shown in the right-hand sidebar of **Workers &
   Pages**, and in the dashboard URL).
3. In this GitHub repository, under **Settings → Secrets and variables →
   Actions**, add two repository secrets: `CLOUDFLARE_API_TOKEN` and
   `CLOUDFLARE_ACCOUNT_ID`.

The first deploy creates the Worker, and the site comes up at
`https://russianwithvladimir.<your-workers-subdomain>.workers.dev`. A custom
domain can be attached later under **Workers & Pages → russianwithvladimir →
Settings → Domains & Routes**.

The workflow can also be run by hand from the repository's Actions tab
(workflow_dispatch), and `npx wrangler dev` previews the site locally.

## Releases

Every push to the default branch is a release, tagged in an ascending
`vMAJOR.MINOR` sequence (v1.0, v1.1, v1.2 …). Each push increments the
minor version by one; a major bump is reserved for a ground-up overhaul.
Tags are created manually by the repo owner from the release notes
accompanying each push.
