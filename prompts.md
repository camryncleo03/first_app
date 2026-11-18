# Prompts

- 2026-11-18: Set up the top-level single-file web app files and numbered project folders, with folder READMEs and layout guidance in `AGENTS.md`. Created the scaffold; it worked.
- 2026-11-18: Read `spec.md` and provide a few-sentence overview plus a high-level review of missing needs and section order, without section-by-section detail. Provided the requested feedback; no code or app files were built.
- 2026-11-18: Revised only the Inputs section of `spec.md` using the user's confirmed support, span, load, section, and deflection controls and limits. No code or app behavior was built.
- 2026-11-18: Reviewed the Calculations section for equations, units, undefined variables, and calculations needed by the Outputs. No spec changes or code were made.
- 2026-11-18: The user established the spec workflow: update spec.md after each section, use [NOTE lines for unresolved questions, move resolved notes to a Resolved notes section, review the whole spec, and commit only after completion. No project files were changed beyond this prompt log entry.
- 2026-11-18: Proposed a 5-stage implementation plan based on `spec.md`, with a mockup-first approach and test checks for each stage. No code or spec changes were made.
- 2026-11-18: Built Stage 1 as a static mockup in `index.html`, showing placeholder inputs, beam, plots, check cards, and responsive layout. No structural calculations were added.
- 2026-11-18: Built Stage 2 interactive controls in `index.html`: support, span, load editing and removal, add controls, material/section dropdowns, and deflection limit. Added clearly separated placeholder calculation functions and did not implement structural calculations.
- 2026-11-18: Added the waste factor to `spec.md` and changed `index.html` to provide a synchronized 0–15% slider with a 5% default and 1% step. Added an adjusted-weight display for the section recommendation.
- 2026-11-18: Implemented the calculation functions and ran hand checks for all four spec validation cases. All reactions, moments, stresses, deflections, and deflection locations matched the spec to the stated precision; project files are ready for commit.
