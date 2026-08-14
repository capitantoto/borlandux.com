# borlandux.com

Website of Borlandux LLC — ML & statistics consulting. A one-page company
site plus a tech blog, built with Jekyll (jekyll-theme-minimal), intended for
GitHub Pages.

## Local development

Requires Homebrew Ruby (the Makefile pins `/opt/homebrew/opt/ruby/bin/bundle`).

- `make` — install deps and serve at http://localhost:4000 with livereload.
- `make build` — build the static site into `_site/`.
- `make clean` — remove `_site/` and `.jekyll-cache/`.

## Custom domain

Once a domain is registered and Pages is enabled, connect it like this:

1. Add a `CNAME` file at the repo root containing the apex domain
   (e.g. `borlandux.com`).
2. Configure DNS at the registrar:
   - Apex domain: A records pointing to the GitHub Pages IPs
     `185.199.108.153`, `185.199.109.153`, `185.199.110.153`,
     `185.199.111.153` — or an ALIAS/ANAME record if the DNS provider
     supports it.
   - `www`: a CNAME record pointing to `capitantoto.github.io`.
3. In the repo: Settings → Pages → deploy from the `main` branch, and set
   the custom domain there.
4. Once the TLS certificate is issued, check "Enforce HTTPS".
