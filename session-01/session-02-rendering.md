---
theme: seriph
colorSchema: auto
title: Frontend System Design — Rendering
info: Forge Community · Session 2 · Choose where and when UI is rendered
class: text-center
transition: slide-left
duration: 45min
---

<div class="forge-kicker">Session 02 · Rendering</div>

# Where should the page be built?

## Rendering is a product and infrastructure decision

<div class="forge-muted">CSR · SSR · Static generation · ISR · Hybrid</div>

---

# The question behind rendering

Rendering turns code and data into the interface users see.

```mermaid {scale: 0.85}
flowchart LR
  A[Route + data] --> B{Where / when is HTML produced?}
  B --> C[Browser: CSR]
  B --> D[Request time: SSR]
  B --> E[Build time: SSG]
  B --> F[Build + revalidate: ISR]
```

The choice affects first content, personalization, freshness, server work, and caching.

---

# CSR: the browser builds the page

```mermaid {scale: 0.5}
sequenceDiagram
  actor U as User
  participant B as Browser
  participant S as Web server
  participant A as API
  U->>B: Open route
  B->>S: Request document + assets
  S-->>B: HTML shell + JavaScript
  B->>B: Download / execute JS
  B->>A: Request data
  A-->>B: JSON
  B->>B: Render content
```

**Fits:** highly interactive authenticated dashboards where SEO is not the main goal.

**Costs:** large JavaScript bundles and chained requests can delay useful content, especially on low-end devices.

---

# SSR: the server renders per request

```mermaid {scale: 0.55}
sequenceDiagram
  actor U as User
  participant B as Browser
  participant S as Frontend server
  participant A as API / data layer
  U->>S: Request page
  S->>A: Read required data
  A-->>S: Data
  S-->>B: HTML with content
  B->>B: Hydrate interactive parts
```

**Fits:** personalized or frequently changing pages where server-rendered content improves the initial experience.

**Costs:** request-time compute, data latency, and hydration work. HTML can appear before every interactive feature is ready.

---

# SSG and ISR: prepare content ahead

```mermaid {scale: 0.7}
flowchart LR
  A[Content + templates] --> B[Build static HTML]
  B --> C[CDN serves page]
  C --> D{Revalidation needed?}
  D -->|No| E[Keep cached output]
  D -->|Yes| F[Regenerate output]
  F --> C
```

- **SSG:** output is generated ahead of requests.
- **ISR:** supported frameworks can regenerate static output after a configured interval or trigger.
- **Benefit:** fast delivery and efficient CDN caching.
- **Cost:** content may be stale until regeneration completes.

Framework semantics differ; verify the actual invalidation and fallback behavior.

---

# Compare the options

| Strategy | Strong fit | Main cost / risk |
|---|---|---|
| CSR | Private, highly interactive screens | JS cost; content may appear late |
| SSR | Personalized or request-fresh content | Compute and data latency per request |
| SSG | Stable public content | Rebuild or invalidation needed |
| ISR | Public content that changes periodically | Bounded staleness and revalidation complexity |

No strategy is universally fastest. Measure the full route and its data dependencies.

---

# Choose per route, not per company

<div class="forge-panel">

**News product example**

- Home page: static or revalidated feed shell
- Article body: static / revalidated when publication permits
- Breaking banner: short cache or push update
- Comments: client-fetched, with loading and failure states
- Saved articles: authenticated, user-specific data

</div>

Hybrid rendering is powerful, but it adds operational complexity and more cache rules to understand.

---

# Hydration: HTML is not the whole story

Server-rendered HTML can make content visible early. Hydration attaches client-side behavior to the rendered markup.

```mermaid {scale: 0.8}
flowchart LR
  A[HTML arrives] --> B[Content visible]
  B --> C[JavaScript downloads]
  C --> D[Hydration]
  D --> E[Interactive controls ready]
```

A page can look ready before it is fully interactive. Track both visual loading and responsiveness.

---

# Decision framework

Ask in this order:

1. Does the route need public search discovery?
2. Does its HTML vary by user or request?
3. How fresh must the content be?
4. Can it be cached safely at a CDN?
5. What does rendering and hydration cost on target devices?

Then test the chosen route under realistic network and device conditions.

---

# Production scenario: product inventory

A product page is public, but inventory changes frequently.

**Possible design:** render stable product information statically or with revalidation; fetch or refresh inventory through a suitably fresh data path.

**Trade-off:** fast product content versus the risk of displaying outdated availability. Checkout must validate stock authoritatively on the server regardless of what the page shows.

---

# Your turn: defend the decision

For each route, pick a strategy and explain the cost:

- a marketing landing page
- a private analytics dashboard
- a product detail page with changing stock
- a user-specific account page

<div class="forge-muted">Next: state ownership, request waterfalls, caching, and data freshness.</div>

---
layout: center
class: text-center
---

<div class="forge-kicker">Forge Community</div>

# Choose the rendering strategy that fits the route.
