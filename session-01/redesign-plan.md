# Forge Community — Frontend System Design Slide Redesign

## Audience and intent
Mixed beginner and intermediate developers. Preserve plain-language explanations while adding production-minded decision-making.

## Design principles
- Premium editorial hierarchy: coordinated light and dark palettes, cool blue/cyan accents, strong headings, generous whitespace.
- Visual-first teaching: architecture maps, sequence diagrams, decision matrices, failure paths, and short code examples.
- Keep Mermaid diagrams legible in both schemes using Slidev's mode-aware rendering and an opaque canvas.
- Every major concept answers: what it is, when it fits, what can fail, how to measure it, and what trade-off it introduces.
- Keep speaker notes and learner prompts so the decks remain teachable, not just readable.
- Avoid new runtime dependencies; continue using Slidev and Mermaid.

## Session_01 plan
1. Foundations: connect browser, CDN, frontend runtime, API, cache, and database; distinguish functional from non-functional requirements; teach a repeatable design method.
2. Rendering: compare CSR, SSR, SSG, and ISR by request flow, freshness, SEO, latency, and compute cost; emphasize hybrid, route-level decisions.
3. State and data: clarify state ownership, parallel requests, cache keys/invalidation, optimistic rollback, and real-time update choices.
4. Performance and reliability: teach Core Web Vitals, measure-before-optimizing, bundle/network bottlenecks, graceful degradation, capacity assumptions, and modular scaling.
5. Security and capstone: model trust boundaries, XSS/CSRF/session risks, accessibility checks, privacy, and a worked news-app design.

## Acceptance criteria
- Five separate runnable Slidev decks remain in place.
- Concepts are accurate and understandable to mixed-experience learners.
- Slides have varied visual rhythm; avoid long runs of text-only bullet slides.
- Each session includes a decision prompt or homework challenge.
- Existing Slidev dependencies and commands remain unchanged.

## Known trade-offs
- More diagrams and case studies improve comprehension but may increase presentation time. Instructors can select optional deep-dive slides.
- Rendering and caching examples are illustrative; production choices must be validated against the framework, freshness requirements, and measured traffic.

## Build
pnpm slidev build \
  session-01/session-01-intro.md \
  session-01/session-02-rendering.md \
  session-01/session-03-state-data.md \
  session-01/session-04-performance-reliability.md \
  session-01/session-05-security-capstone.md
