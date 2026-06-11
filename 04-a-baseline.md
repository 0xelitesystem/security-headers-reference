# A baseline

A sensible baseline is: HSTS to force HTTPS, X-Content-Type-Options to stop type guessing, frame protection to prevent clickjacking, a strict referrer policy, and a Content Security Policy built up carefully. Start with the simple headers immediately and add CSP incrementally.

## Start with the easy wins

The simple headers, HSTS, content-type options, frame protection, and referrer policy, can be added right away because they rarely break anything and provide immediate protection. These are the easy wins: a few lines of server or host configuration that close off several common attack avenues at once. Deploying these first gives most of the benefit for almost none of the effort, and they form the core of a baseline any site should have.

```
Strict-Transport-Security: max-age=31536000; includeSubDomains
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: strict-origin-when-cross-origin
```

## Add CSP carefully

Content Security Policy is the high-value addition that takes more care. Add it after the simple headers, building it incrementally in report-only mode first so you can see what your site loads before you enforce restrictions. The baseline includes a CSP, but a CSP built deliberately rather than rushed, because a hasty one breaks the site and a careful one protects it. Treat CSP as the considered next step after the easy headers are in place.

A minimal starting policy for a site that serves its own assets and uses no inline scripts:

```
Content-Security-Policy: default-src 'self'; frame-ancestors 'none'; base-uri 'self'; form-action 'self'
```

Start it as `Content-Security-Policy-Report-Only` while you watch what breaks, then enforce.

## Match the baseline to the site

A baseline is a starting point, not a fixed prescription; the right headers depend on what your site does. A site that needs to be framed legitimately, or that loads content from many third parties, will adjust the baseline accordingly. The principle is to enable the protections that fit your site and tighten them as far as your site allows. Start from the baseline, then adapt it to your actual content and needs rather than applying it blindly.

## Tighten over time

Security headers reward an iterative approach: start with a safe baseline, then tighten as you confirm what your site needs. A CSP can start permissive and grow stricter; protections can be added as you verify they do not break anything. This gradual tightening reaches a strong, working configuration without the disruption of deploying an aggressive policy all at once. The baseline gets you protected quickly; ongoing tightening gets you to strong, and doing it gradually keeps the site working throughout.
