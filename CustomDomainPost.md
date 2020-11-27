# Blog Post Hosting Custom Domain

Hosting a personal website on Github Pages with a custom domain.

First, purchase a domain name.

I purchesed mine on [Google Domains](https://domains.google.com). They seemed to have the best selection and lowest prices for most options.
Google recently launched a few of their own top level domains. `.page`, `.dev`, `.studio`, `.tech`, and `.design`.

I felt that `.dev` fit my web presence as a developer the best.

`.dev` is always served over `.https` (secured by Google).

Github will host a "root" GitHub Pages site for your repo <user>.github.io. This repo will be served by default at `https://<user>.github.io`. Applying a custom domain to this repo will naturally apply to all other repos hosted on Github Pages

`https://<user>.github.io/<repo>` => `https://mycustom.domain/<repo>`

Second step is to configure your DNS to redirect your custom domain to GitHub. Any DNS service will work similarly, but I used Google Domains.

First apply a apex domain Alias `A` rule directly to the IP Addresses of GitHub servers.

https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site

Then apply a CNAME Rule for the `www` subdomain to point to `<user>.github.io`.

Note that all these modifications may take up to 48 hours to apply and propogate across DNS servers.

Once the DNS records are in place, you must enable `Enforce HTTPS` in the GitHub UI. GitHub will automatically sign and distribute a `letsencrypt` Certificate for your site. This may take up to 15 min to complete.

<!-- Image of TLS progress -->

--

Once you have your root GitHub pages repo setup, you can host other repositories on subdomains if you prefer.

`https://mycustom.domain/<repo>` => `https://<repo>.mycustom.domain/`

Back in the DNS config, add a second CNAME record for your desired subdomain.

`<domain>` CNAME => `<user>.github.io`.

Note that you do not need to add the path to the repo, simply redirect to `github.io`. We will configure the repo itself with a CNAME record to instruct GitHub where to redirect the request.

Once the CNAME record is in place, go to the repo you wish to host.

Add a CNAME file to the repo root with the url including the subdomain. `<domain>.mycustom.domain`. This may take 15min - 60min to apply. Once it applies, be sure to enable `Enforce HTTPS`. This will again take 15 min to deploy a new certificate.

At this point, your repo's GitHug Pages will be available at `https://<domain>.mycustom.domain`.


<!-- Previous notes -->
# Custom Domain

I have purchased a custom domain name for hosting this blog: [brisberg.dev](https://brisberg.dev)

Purchased from [Google Domains](https://domains.google/).

After some playing around, I followed [GitHub's Guide](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/configuring-a-custom-domain-for-your-github-pages-site) for setting up a custom domain for GitHub Pages.

The built in Google Domain forward rules didn't work. It directs to `ghs.googlehosted.com` instead of `brisberg.github.io`. Also I had to add `ALIAS` (`A`) rules towards the 4 IPs provided by Github.

I needed to wait nearly 30 min for Github to provision new TLS Certificates but it now works over `https`.
