# Testing and pitfalls

Test security headers with a header-checking tool to confirm they are present and correct, and watch for the common pitfalls: a too-strict CSP that breaks legitimate content, HSTS set carelessly, and headers that are configured but not actually sent. Verify before trusting that they work.

## Test that they are sent

The first check is simply confirming the headers are actually present in your responses, because a header configured but not sent protects nothing. Header-checking tools and the browser's own developer tools show which headers a page returns. Verifying that each intended header is present and has the right value catches the common situation where a configuration change did not take effect. Do not assume a configured header is a sent header; check.

## The CSP breakage pitfall

The most common pitfall is a Content Security Policy that is stricter than the site needs, blocking legitimate content and breaking functionality. This is why building CSP in report-only mode first matters: it shows what would break before it actually breaks. If a CSP breaks something after enforcement, the fix is to identify the legitimately needed source it blocked and permit it. A broken site from an over-strict CSP is the classic header mistake, and report-only mode is the classic prevention.

## The HSTS pitfall

HSTS instructs browsers to refuse insecure connections to your site for a set duration, and that instruction sticks in the browser. If you enable HSTS before your HTTPS setup is fully working, or with an overly long duration before you are confident, you can lock users into a configuration you are not ready for. The pitfall is committing to HSTS aggressively before HTTPS is solid. Confirm HTTPS works completely, then enable HSTS, increasing its duration as your confidence grows.

## Verify after every change

Because headers are configured on the server or host, changes elsewhere, a host migration, a configuration update, a new deployment, can silently drop or alter them. The pitfall is assuming headers stay in place once set. Re-checking the headers after significant changes catches a header that quietly disappeared. Periodic verification, and verification after any change to the serving setup, keeps the protections you deployed from lapsing without your noticing. Set them, then keep confirming they are still there.
