# Prompt Library

## Context Management

Prompts for preserving or transferring conversation state.

### Compact — preserve decisions & changes

`/compact` — Preserve all decisions, changes, and additions made this session. Prioritize: (1) explicit decisions/confirmations, (2) file changes and additions, (3) rationale behind them. Compress general discussion/exploration first.

### Handoff summary — resume in new chat

Act as an expert technical archivist. Generate a comprehensive handoff summary of our entire conversation so far. Format it so I can paste it directly into a brand-new chat to resume work seamlessly without losing context. Include: (1) Core project goals and overall objective, (2) Key decisions made and constraints established, (3) Current technical stack, file structures, or core components discussed, (4) Exact state of what we just finished, and (5) The immediate next steps or open tasks we need to tackle. Be dense with technical specifics, code snippets or logic paths if applicable, but concise enough to fit efficiently into a new context window.

## UI/UX Animation & Transitions

Prompts for auditing and upgrading motion design in a frontend codebase.

### Motion audit & upgrade — principles + reusable patterns

Act as a senior motion/interaction designer doing a paid audit of this codebase's animations and transitions. First, inventory every place motion currently exists (CSS transitions/keyframes, animation libraries like Framer Motion, custom hooks that gate animation lifecycle, autoplay/carousel logic) and every place it's conspicuously absent on interactive elements (buttons, cards, modals, menus, toggles, form validation, loading/empty states). Score what exists against Disney's 12 principles adapted for web (timing under 300ms for user-initiated motion, ease-out entrances / ease-in exits, spring physics for overshoot, one focal point at a time, staggered enters ≤50ms/item, dimmed modal backgrounds) and against interface-polish fundamentals (interruptible CSS-transition state changes vs. one-shot keyframes, split+staggered enter animations with subtler exits, scale-on-press at exactly 0.96, contextual icon cross-fades, no `transition: all`, `will-change` reserved for transform/opacity/filter only, `prefers-reduced-motion` handled with an intentional reduced alternative rather than a blanket kill). Flag every violation with file:line and a one-line fix. Then, for gaps where a well-tested, accessible pattern already exists rather than a bespoke one — dropdowns, modals, panel reveals, notification badges, success confirmations, input-shake on validation error, page transitions, icon swaps, number pop-ins — pull the matching transition from transitions.dev (https://transitions.dev, `npx transitions-pro`, or its agent skill) instead of hand-rolling it; its `t-*` snippets already ship with `@media (prefers-reduced-motion: reduce)` guards and semantic custom properties, so adapt them to this project's existing motion tokens/hooks rather than importing a second animation system. Respect whatever animation lifecycle/gating hooks the project already has (e.g. an intro-motion hook that plays once, stops on interaction, and pauses off-screen) — extend that pattern to new motion instead of introducing a competing one. Deliver: (1) the audit table of violations, (2) a prioritized list of missing-motion opportunities with the exact transitions.dev pattern or hand-written values to use for each, (3) the diffs applied, grouped by principle, as before/after tables — nothing that changes behavior or copy outside of motion/timing/easing.
