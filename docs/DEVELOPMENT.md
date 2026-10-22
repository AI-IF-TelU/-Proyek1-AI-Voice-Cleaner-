# Development plan & gates

## Stage 1 (current)
- [x] Provisional problem and user.
- [x] Architecture choice: Next.js, FastAPI, PostgreSQL.
- [x] Proposed A/B demo.
- [ ] Obtain official rubric, event duration, team composition.
- [ ] Check Generative AI requirement and model suitability.
- [ ] Competitor + same-domain winner research (if applicable).
- [ ] Validate real noisy audio and model resource budget.
- [ ] Explicit GO approval.

## Stage 2 — only after GO
1. AMATI: 5–8 design references; comparison matrix.
2. TIRU: extract 2–3 design patterns, not pixel-copy.
3. MODIFIKASI: final UI and user journey.
4. Scaffold monorepo, env templates, CI, PostgreSQL and migrations.
5. Implement upload + secure job lifecycle + inference.
6. Implement synchronized before/after, download and accessible states.
7. Evaluate on held-out clips and record limitations.
8. Deploy, test end-to-end, capture demo video/screenshots.

## Suggested task ownership
FE/UI, BE/API+DB, ML/evaluation, integration/QA/docs. Roles may overlap depending on team size.

## Definition of done
No broken demo path; no fabricated results; valid error states; tests passing; secrets not committed; cleanup verified; documented model license and deployment constraints.
