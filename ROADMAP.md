# ROADMAP (MVP Delivery)

## Goal
A single-page web app MVP that accepts a short startup idea and returns a brutally honest, 3-point critique in the voice of a Silicon Valley investor.

## Timeline: 15 Days
- **Day 0-1:** Bootstrap + schema + system prompt
- **Day 2-4:** Backend APIs + DB + simple worker
- **Day 5-7:** Frontend + basic integration
- **Day 8:** Queue, rate limits, auth
- **Day 9-11:** Polish UI, error handling, retries
- **Day 12:** Tests & CI
- **Day 13:** Deploy + monitoring
- **Day 14:** Manual QA + documentation
- **Day 15:** Final polish + handover

## Acceptance Criteria
- [ ] User submits idea -> gets exactly 3 critique points.
- [ ] Persona covered: Market, Uniqueness, Monetization, Execution Risk.
- [ ] Accessible web app URL.
- [ ] Security, Rate Limits, and Retry on invalid schema.
