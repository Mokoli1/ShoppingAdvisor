# Shopping Advisor – Product Requirements Document (Merged & Final)

**Version:** 2.0  
**Date:** 13 June 2025  
**Document Owner:** Shopping Advisor Product Team  
**Status:** Draft → Ready for Cross-Functional Review

## 1. Executive Summary

Shopping Advisor is a mobile (with complementary web) application that determines the true cost of grocery shopping by combining real-time product prices with travel, time, and club-membership costs. It recommends the cheapest single-store or multi-store strategy and learns user preferences to improve over time.

**Key Proposition:** "The cheapest cart isn't always the best deal—Shopping Advisor shows the all-in cost so you never overpay."

## 2. Problem Statement

1. **Membership ROI Uncertainty** – Shoppers pay warehouse fees (e.g., Costco) without knowing if they break even.
2. **Hidden Costs Ignored** – Gas, mileage depreciation, and the value of time are rarely factored into "cheap."
3. **Multi-Store Complexity** – Manually deciding if splitting a list across stores saves money is hard.
4. **Generic Lists vs. Specific Prices** – Lists say "milk"; stores price specific SKUs.

## 3. Target Users & Personas

| Persona | Profile | Goals | Pain Points |
|---------|---------|-------|-------------|
| Budget-Conscious Family Shopper | Age 25-45, suburban, HH income $40–80k | Maximize monthly grocery savings | Unsure if membership fees pay off; complex price comparison |
| Efficient Urban Professional | Age 25-40, urban, HH income $60–120k | Minimize trips & wasted time | Limited time to scout prices; dislikes multiple stops |

## 4. Product Goals & Success Metrics

| Goal | KPI | 6mo Target | 12mo Target |
|------|-----|------------|-------------|
| Increase user savings | Avg. $ saved per active user /mo | $40 | $50 |
| Drive engagement | WAU / MAU | 60% | 65% |
| Retain users | 3mo retention | 40% | 50% |
| Monetize ethically | ARR | $100k | $500k |

## 5. Scope & Phasing

### 5.1 MVP (Priority 1 – Launch Market)

1. **Smart List Creation**
   - Text, voice, and OCR (handwritten list) input.
   - Generic-to-SKU mapping with visible default + quick refinement.

2. **Price & Store Comparison**
   - Pull daily price feeds for ≥10 local stores.
   - Return top-3 single-store options with total basket cost.

3. **True-Cost Calculator**
   - Gas (user MPG or average) + mileage wear + time value (user-set hourly rate).
   - Membership fee amortization.

4. **Multi-Store Optimizer**
   - Split across ≤3 stores only if savings ≥$10 and time increase ≤20 min.

5. **Basic Profile & Preferences**
   - Vehicle, store distance limit, memberships, dietary/brand prefs.

### 5.2 Phase 2 (Priority 2 – Months 6-12)

- Barcode & receipt scan → exact SKU & price history.
- Shared household lists & roles.
- Price-drop / deal alerts.
- Membership break-even dashboard.
- Dark-mode & full accessibility.

### 5.3 Phase 3 (Priority 3 – Year 2)

- AI meal-plan → auto-list.
- Community price reporting & gamification.
- Carbon-footprint tracking.
- Grocery-delivery & loyalty-card integrations.

## 6. Detailed Requirements (MVP)

| # | Feature | User Story | Acceptance Criteria |
|---|---------|------------|-------------------|
| 1 | Smart List | As a user I can add 10 items in <60s | 90% generic items map to correct SKU; voice works in noisy kitchen |
| 2 | Store Comparison | As a user I see ranked stores with all-in cost | Result ≤10s for 20-item list; gas calc accurate ±$0.50 |
| 3 | Multi-Store Plan | As a user I get a clear itinerary showing extra time vs. savings | Recommends split only when criteria met; includes route map |
| 4 | Membership ROI | As a member I see if I'm on-track to break even | Dashboard shows monthly savings vs. fee; renewal reminder |
| 5 | Data Privacy | My data is secure & deletable | GDPR/CCPA compliant; data encrypted in transit & at rest |

## 7. Technical Architecture (MVP)

- **Frontend:** React Native mobile (iOS 14+, Android 10+) + Next.js web dashboard.
- **Backend:** GCP – Cloud Run microservices:
  - User Service (Firebase Auth, Firestore).
  - Product Service (PostgreSQL + price cache Redis).
  - Optimization Engine (Python FastAPI) – cost model & route solver.
- **Integrations:**
  - Price APIs / respectful scraping (daily).
  - Google Maps (distance, ETA).
  - GasBuddy (fuel price).
  - Veryfi OCR (receipts).
- **ML components:**
  - OCR & SKU linking (3rd-party).
  - Collaborative filtering for "Your Usuals."
- **Performance Budgets:**
  - App launch <3s.
  - API 95th-pct latency <700ms.
  - <50 MB/mo cellular data.

## 8. Security & Privacy

- TLS 1.3 everywhere, AES-256 at rest.
- Least-privilege Firestore rules; automated security testing in CI.
- Data usage transparency modal on first launch; one-tap export & delete.

## 9. Revenue Model

1. **Freemium** – Core free, Premium $4.99/mo (multi-store optimizer, unlimited lists, analytics).
2. **Affiliate Fees** – Optional click-through to partner store apps/sites.
3. **Premium Placement** – Paid slot for partner stores (clearly labeled, no impact on ranking logic).

## 10. Go-to-Market Plan

| Phase | Geography | Key Activities |
|-------|-----------|----------------|
| Beta (Months 5-6) | Des Moines, IA | Recruit 100 families; partner 2 local chains; iterate weekly |
| Regional (6-12) | 5 Midwest metros | Social & influencer campaigns; referral program |
| National (12-24) | USA | Add major chains & delivery APIs; PR & finance-blog features |

## 11. Timeline & Milestones

| Mo | Milestone |
|----|-----------|
| 1 | Architecture complete, price-feed POC |
| 2 | Core algorithm & Firestore schema |
| 3 | Mobile alpha with list & comparison |
| 4 | Closed beta go-live |
| 6 | MVP public launch |
| 9 | Phase 2 feature set frozen |
| 12 | Multi-market expansion |

## 12. Risk & Mitigation

| Risk | Impact | Mitigation |
|------|--------|------------|
| Price data gaps | Wrong recommendations | Multi-source + user flag & reward for corrections |
| API rate limits | Service disruption | Caching, backoff, partner agreements |
| Low adoption | Miss targets | Aggressive referral, focus on clear $ savings |
| Privacy concerns | User churn, legal | Transparent policy, opt-in analytics |

## 13. Appendices

- **A.** Competitive Landscape – Flipp, Ibotta, Basket, Honey comparison.
- **B.** Detailed Cost Model Formulas – Gas, depreciation, time valuation.
- **C.** User Research Summary – 30 interviews, key insights.
- **D.** Financial Projections – 24-month ARR & CAC/LTV.

---
*End of Document* 