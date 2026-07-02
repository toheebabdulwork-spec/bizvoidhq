# Deploying this site (GitHub Pages)

Self-contained static one-pager. `index.html` is byte-identical to the handoff file (see `../design_handoff_bizvoid_onepage_site/README.md` for the design spec). No build step, no dependencies.

This folder is already a git repo with `index.html` committed at root. To publish:

```sh
cd site
# 1. authenticate gh once (interactive — must be run by a human):
gh auth login          # choose GitHub.com → HTTPS → auth via browser

# 2. create the repo (private) and push:
gh repo create bizvoidhq --private --source=. --remote=origin --push

# 3. enable Pages from the main branch root:
gh api -X POST repos/{owner}/bizvoidhq/pages \
  -f 'source[branch]=main' -f 'source[path]=/'
```

Note: GitHub Pages on a **private** repo requires GitHub Pro/Team/Enterprise (free plan only serves Pages from public repos). If the account is on the free plan, either make the repo public or upgrade before step 3.

Pages then serves at `https://<owner>.github.io/bizvoidhq/`.

## Custom domain (the secondary reputation domain)
```sh
# write the domain into a CNAME file at repo root, commit, push:
echo your-secondary-domain.com > CNAME
git add CNAME && git commit -m "Add custom domain" && git push
```
At your DNS provider, point the domain at Pages:
- apex domain → four A records: 185.199.108/109/110/111.153
- `www` (or a subdomain) → CNAME to `<owner>.github.io`

Then in the repo Settings → Pages, tick **Enforce HTTPS**. Keep the page at the domain root (`/`) over HTTPS.
