# vocabswipe.com

A redirect. Everything on `vocabswipe.com` goes to `https://vocabswiper.com`, keeping the path.

Hosted on GitHub Pages so the redirect is served over HTTPS with a real
certificate. That is not a preference for `.app` domains: the whole TLD is on
the HSTS preload list, so browsers refuse to make a plain HTTP request to one
at all, and a redirect that cannot answer on HTTPS simply fails.

`index.html` answers `/`; `404.html` is the same page, which is how every
other path gets redirected too — GitHub Pages serves it for anything it does
not recognise.

## DNS (Namecheap, Advanced DNS)

| Type | Host | Value |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | stratelabs.github.io. |

## If HTTPS is stuck

GitHub secures the apex and `www` together and the certificate request can
silently stall, which on a `.app` domain means the site is simply dead. Poke
it:

```sh
gh api -X PUT repos/stratelabs/vocabswipe-com-redirect/pages -f cname=''
gh api -X PUT repos/stratelabs/vocabswipe-com-redirect/pages -f cname='vocabswipe.com'
gh api -X PUT repos/stratelabs/vocabswipe-com-redirect/pages -F https_enforced=true
```
