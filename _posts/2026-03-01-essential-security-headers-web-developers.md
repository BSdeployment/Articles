---
title: "Essential Security Headers Every Web Developer Should Implement"
date: 2026-03-01
categories: [cybersecurity]
tags: [security, web-development, headers, best-practices]
author: "Bs DotNet"
reading_time: 5
description: "A practical guide to HTTP security headers that protect your web applications from common attacks."
---

Security headers are one of the simplest yet most overlooked defenses in web application security. A few lines of configuration can protect your users from XSS, clickjacking, MIME-type attacks, and more.

Let's walk through the headers every web application should have.

## Content-Security-Policy (CSP)

CSP is your strongest defense against XSS attacks. It tells the browser exactly which sources of content are allowed:

```
Content-Security-Policy: default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' data: https:; font-src 'self'
```

### Implementation in ASP.NET Core

```csharp
app.Use(async (context, next) =>
{
    context.Response.Headers.Append(
        "Content-Security-Policy",
        "default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'"
    );
    await next();
});
```

> **Start strict, then relax.** Begin with `default-src 'none'` and add sources as needed. This is far safer than starting permissive.

## Strict-Transport-Security (HSTS)

Forces browsers to use HTTPS for all future requests:

```
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
```

## X-Content-Type-Options

Prevents browsers from MIME-type sniffing:

```
X-Content-Type-Options: nosniff
```

## Referrer-Policy

Controls how much referrer information is sent with requests:

```
Referrer-Policy: strict-origin-when-cross-origin
```

## Permissions-Policy

Restricts which browser features your site can use:

```
Permissions-Policy: camera=(), microphone=(), geolocation=(), payment=()
```

## Testing Your Headers

Use these tools to audit your security headers:

1. **[securityheaders.com](https://securityheaders.com)** — Free scanner with grading
2. **Browser DevTools** — Network tab → Response Headers
3. **curl** — `curl -I https://yoursite.com`

---

Security headers are a low-effort, high-impact security measure. Implement them today, and you'll have eliminated several entire classes of attacks with minimal code changes.

*Next article: Deep dive into Content Security Policy — reporting, nonces, and handling third-party scripts.*
