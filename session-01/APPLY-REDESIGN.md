# Apply the Forge Community slide redesign

<!-- This bundle contains the redesigned five-session Slidev decks, shared theme CSS, and the focused redesign plan. -->

## Files
- session-01-intro.md
- session-02-rendering.md
- session-03-state-data.md
- session-04-performance-reliability.md
- session-05-security-capstone.md
<!-- - `style.css`
- `redesign-plan.md` -->


## Validate locally
```bash
pnpm install --frozen-lockfile
pnpm exec slidev session-01-intro.md
pnpm exec slidev session-02-rendering.md
pnpm exec slidev session-03-state-data.md
pnpm exec slidev session-04-performance-reliability.md
pnpm exec slidev session-05-security-capstone.md
```

Build/export commands depend on the project's existing scripts. Check each deck in the browser and export before presenting.

## Design and content notes
- The shared CSS uses a restrained dark ink palette with cyan/blue accents.
- Mermaid diagrams are used for architecture and request flows.
- The technical examples are illustrative. Validate framework-specific behavior and production targets against your actual stack and measured workloads.
- Core Web Vitals thresholds shown in Session 4 are the standard “good” thresholds at the 75th percentile; re-check current web.dev guidance when updating the course.
