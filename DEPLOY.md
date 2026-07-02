# Deploying this site

Ready-to-deploy static one-pager (see `../design_handoff_bizvoid_onepage_site/README.md` for the design spec). `index.html` is byte-identical to the handoff file; `Dockerfile` + `Caddyfile` exist only so container hosts (Railway) can serve it — static hosts (Netlify, GitHub Pages) can ignore them.

## Railway (project already created: `bizvoid-onepage`)
```sh
cd site
railway up --detach     # build + deploy
railway domain          # generate a public *.up.railway.app URL
```
Then attach the real secondary domain in the Railway dashboard (Settings → Networking → Custom Domain) and add the CNAME it gives you at your DNS provider.

## GitHub Pages (alternative)
New repo → commit `index.html` at root → Settings → Pages → deploy from `main` → set custom domain + enable HTTPS.

Keep the page at the domain root (`/`) and serve over HTTPS.
