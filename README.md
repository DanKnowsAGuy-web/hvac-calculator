# HVAC Calculator

A re-skinned version of the Energy Plus savings calculator. Same engine and math as the
original, new layout and storytelling (the card flow designed in the landing-page prototype).
Meant to live as its own repo and also embed as a popup on the commercial landing page.

## What this is

- `original-engine.html` — a verbatim, byte-for-byte clone of the original calculator
  (`commercial-landing/public/calculator.html`). This is the untouched engine we build on.
  Verified identical at clone time (4,803 lines).
- The re-skin changes **presentation only**: markup, CSS, the order questions are asked, and
  which on-screen element shows which result. The calculation engine (`compute()`), every
  constant, every preset, and every state table are left exactly as they are.

## The rule

Nothing that produces a number gets edited. We keep the engine and its wiring; we build a new
dashboard and body around it. Same inputs must yield the same outputs as the original.

## Plan (staged, each stage is browser-testable)

1. Clone the engine.  ✅ done (`original-engine.html`)
2. Restyle: apply the new theme/typography/spacing over the existing DOM. Lowest risk, math
   untouched. Test in a browser.
3. Reflow: regroup the existing stages into the new card sequence
   (location → facility + cost → the running-total estimate → equipment reveal → cost list → book).
   Test.
4. Re-present the results: running total, benefits row, 179D slider, the equipment-framed
   reveal + animation, the cost report, and the Cal.com notes prefill on booking. Test.
5. "Change your assumptions" accordion: surface the engine's existing depth toggles
   (lighting, motor, demand, rate negotiation, etc.) inside a collapsible panel on the results,
   framed as "this uses standard assumptions — open to adjust and see updated numbers." The
   engine already supports these; we're exposing them, not adding logic.
6. Parity check: same inputs into the original and this clone, confirm the numbers match, then
   final polish.

## Notes

- Levers not surfaced on screen run at their original preset positions (unchanged).
- To make this its own repo: move this `hvac-calculator/` folder up one level so it sits beside
  `commercial-landing/`, then `git init` and push. It's self-contained.
- Testing happens in a real browser between stages; the build environment here can't render it.
