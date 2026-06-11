# The essential headers

The essential security headers are HSTS, which forces encrypted connections; X-Content-Type-Options, which stops content-type guessing; a frame-protection header, which prevents your page from being embedded by others; and a referrer-policy header, which controls what referrer information is shared. Each addresses a specific, common risk.

## HSTS: force HTTPS

The HTTP Strict Transport Security header tells the browser to only ever connect to your site over encrypted HTTPS, even if a user types or follows an insecure link. This closes the window where a connection could be downgraded to unencrypted and intercepted. Once set, the browser refuses insecure connections to your site for the specified duration. HSTS is a core header for any site served over HTTPS, which today should be every site.

```
Strict-Transport-Security: max-age=31536000; includeSubDomains
```

That is one year, applied to subdomains too. Only add `preload` after verifying every subdomain serves HTTPS, because preload is hard to undo.

## X-Content-Type-Options: stop MIME sniffing

This header tells the browser not to guess the type of a file but to trust the declared type. Without it, a browser might interpret a file as a different, more dangerous type than intended, which attackers can exploit. Setting it disables this guessing, ensuring files are treated as what they are declared to be. It is a simple header with one job, and it closes a real avenue for content-based attacks.

```
X-Content-Type-Options: nosniff
```

`nosniff` is the only value. There is no reason not to set it on every response.

## Frame protection: prevent clickjacking

A frame-protection header, historically X-Frame-Options and now also expressible through Content Security Policy, controls whether your page can be embedded in a frame on another site. Preventing unwanted framing stops clickjacking, where an attacker embeds your page invisibly and tricks users into interacting with it. Unless you have a reason to allow framing, telling the browser to refuse it protects your users from this manipulation. It is a key header for any page where user actions matter.

```
X-Frame-Options: DENY
```

The modern CSP equivalent, which takes precedence where both are present, is `frame-ancestors 'none'` inside Content-Security-Policy. Use `SAMEORIGIN` (or `frame-ancestors 'self'`) only if your own pages frame each other.

## Referrer policy: control leakage

The referrer-policy header controls how much information about the originating page is sent when a user navigates away or loads a resource. By default, browsers may send the full originating URL, which can leak information through the referrer. Setting a stricter referrer policy limits what is shared, reducing inadvertent leakage of URLs that might contain sensitive context. It is a privacy-protecting header that costs nothing and prevents quiet information disclosure.

```
Referrer-Policy: strict-origin-when-cross-origin
```

This sends the full URL within your own site, only the origin to other HTTPS sites, and nothing to insecure destinations. It is the sensible default for most sites.
