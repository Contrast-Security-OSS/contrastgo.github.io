# Using Github pages to serve Go vanity URLs

To setup `vangen` vanity site generator for `go` imports to use Github pages
follow these steps.

**To make this easy I've set this respoitory as a template which you can fork
to your own repo.**

## 1. Create `gh-pages` branch

```bash
git checkout --orphan gh-pages
git reset --hard && git clean -fd
touch README.md
git add .
git commit -m "Initial commit"
git push -u origin gh-pages
```

## 2. Add workflow from `.github/workflows/` to build and deploy

```yaml
name: Build and Deploy
on: [push]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout 🛎️
        uses: actions/checkout@v2.3.1

      - name: Install and Build
        run: |
          curl -sSL https://github.com/leighmcculloch/vangen/releases/download/v1.1.3/vangen_1.1.3_linux_amd64.tar.gz | tar xz -C /usr/local/bin vangen
          vangen -out build

      - name: Deploy 🚀
        uses: JamesIves/github-pages-deploy-action@4.1.7
        with:
          branch: gh-pages
          folder: build
```

## 3. Update your Pages site to point at the `gh-pages` branch

From the repository settings click `Settings` and then `Pages`.

In the branch dropdown under Source select `gh-pages` and click `Save`.

## Using a Custom Domain

Update the `Custom domain` section with the domain you wish to use.

i.e. `go.benjiv.com`

Click `Save` to update the pages.

Update your DNS settings to point the domain you wish to use at the domain
Github suggests. Generally this follows the pattern `<username>.github.io.`.

**NOTE**: The `.` at the end of the address is required.

Once you have updated your DNS settings, you can test your site by visiting
`https://go.benjiv.com`. This should show your readme.

**NOTE**: DNS entries can take up to 24 hours to propagate.

After Github has verified your CNAME points to your domain, you can publish
your site with HTTPS by checking the `Enforce HTTPS` checkbox.
