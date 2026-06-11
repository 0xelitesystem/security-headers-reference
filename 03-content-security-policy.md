# Content Security Policy

Content Security Policy, or CSP, is the most powerful security header: it tells the browser exactly which sources content may load from, sharply limiting the damage of content-injection attacks. It is also the most involved to configure, because it must allow everything your site legitimately uses while blocking everything else.

## What CSP does

A Content Security Policy specifies the allowed sources for the various kinds of content a page loads: scripts, styles, images, fonts, and more. The browser then refuses to load anything from a source not on the list. This directly limits content-injection attacks, because injected content from an unapproved source simply does not run. CSP turns the browser into an enforcer of an allowlist you define, which is a strong defense against a serious class of attack.

## Why it is powerful

CSP is powerful because content injection, getting unauthorized scripts to run in a user's browser, is among the most damaging web attacks, and CSP can largely neutralize it. By restricting scripts to known, approved sources and disallowing the risky patterns that injection relies on, a well-built CSP removes much of the attacker's ability to execute malicious code even if they manage to inject it. No other single header addresses this class of attack as directly.

## Why it is involved

CSP is harder to deploy than the simpler headers because it must enumerate everything your site legitimately loads, from your own resources to any third-party scripts, styles, fonts, and embeds you use. Miss something and that legitimate content breaks; be too permissive and the policy provides little protection. Building a CSP means knowing exactly what your site loads and from where, then writing a policy that permits all of it and nothing more. This takes care and testing.

## Build it incrementally

The practical way to deploy CSP is incrementally: start in a report-only mode that logs what would be blocked without actually blocking it, see what your site loads, refine the policy until it covers everything legitimate, then enforce it. This avoids breaking the site while you get the policy right. Starting strict and enforcing immediately tends to break things; starting in report-only and tightening toward enforcement is the path that gets you a working, protective policy without taking the site down in the process.
