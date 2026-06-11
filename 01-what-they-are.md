# What they are

Security headers are HTTP response headers, sent by the server with each page, that instruct the browser to apply specific protections. Because the browser enforces them, they let a site harden itself against several common attacks by simply telling the browser how to behave.

## Headers instruct the browser

Every HTTP response carries headers alongside the content, and some of those headers are instructions to the browser about security: enforce encryption, restrict content sources, refuse to be embedded, and so on. The browser reads these and enforces them. This makes headers a powerful, low-effort tool: the protection runs in the browser, and you enable it by sending the right header. The server asks; the browser enforces.

## Why they are effective

Security headers are effective because they engage protections built into every modern browser. Rather than building defenses yourself, you switch on defenses the browser already has, targeted at common attack patterns like clickjacking, protocol downgrade, and content injection. The browser does the enforcement work; your job is to send the headers that turn it on. This is why headers offer strong protection for little effort: the heavy lifting is already in the browser.

## Defense in depth

Headers are one layer of defense, not the whole of security. They complement, rather than replace, other practices like keeping software updated, validating input, and managing access. A header that prevents one class of attack does nothing about another, so headers are part of a layered approach. Their value is that they cheaply add several layers at once, closing off common attack avenues that would otherwise be open. They are a strong layer, not a complete shield.

## Low effort, real value

Most security headers take minutes to add, often as a configuration change on the server or host, and provide real, immediate protection. This combination of low effort and genuine value is why they are among the first hardening steps worth taking. A site without them is leaving easy, free protections switched off. The following sections cover which headers matter most and how to deploy them without breaking anything.
