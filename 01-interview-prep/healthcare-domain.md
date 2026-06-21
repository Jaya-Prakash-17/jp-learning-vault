# Healthcare Domain

## 1. The Need (Business Purpose)
- **The Need**: The US Healthcare system is highly fragmented. Providers (Hospitals) and Payers (Insurance) use completely different software systems. Without standardized integration rules (HIPAA/CAQH), claims get lost, providers go bankrupt, and patients are denied care.

## 2. Core Concepts
- **Providers vs Payers vs Clearinghouses**: Providers give care. Payers pay for care. Clearinghouses are the middle-men that batch and scrub files between them.
- **Adjudication**: The core business rules engine at a Payer that decides whether to pay, deny, or reduce a claim.
- **CAQH CORE SLAs**: Legally mandated performance rules (e.g., a real-time eligibility check must return a response in under 20 seconds).

## 3. Basic Daily Workflows
- **Eligibility Checks**: Real-time 270/271 flows to ensure a patient is covered before surgery.
- **Claim Status**: Checking 276/277 logs to find out why a provider hasn't been paid.
- **Demographic Mapping**: Ensuring Patient DOB and Name perfectly match across all transactions to prevent "Member Not Found" rejections.

## 4. Advanced Scenarios
- **API Fallbacks**: Gracefully degrading a real-time HTTP response when the core adjudication system crashes, ensuring the provider still receives a HIPAA-compliant X12 error instead of a raw stack trace.
- **Balancing Financials**: Reconciling an 835 Remittance Advice to ensure the sum of all payments and contractual adjustments exactly matches the total amount billed on the 837.

---

## Interview Question Deep Dive

### Q: "How do you ensure CAQH CORE compliance in a real-time integration?"

**30-Second Answer**: We ensure compliance by executing SNIP 1-7 validations at the very edge of the network using pre-compiled profiles, and by utilizing synchronous HTTP routes with strict timeout thresholds to guarantee a response within the 20-second SLA.

**2-Minute Answer**: CAQH CORE compliance isn't just about data formatting; it's about latency and connectivity. To achieve this, the architecture must be completely synchronous. When an inbound 276 arrives, we immediately run it through an Edifecs profile. If it's malformed, we instantly kick back a 277CA. If it's valid, it drops into the DataFlow. We wrap all backend CORE API lookups in strict timeout exception handlers (e.g., 5 seconds max). If the backend is slow, we catch the timeout and generate an X12 STC error segment indicating "System Unavailable." 

**Deep Dive Answer**: The hardest part of CAQH compliance is thread exhaustion under load. If you get hit with 100 concurrent SOAP requests and your connection pool only has 50 threads, requests will queue. By the time the 51st request is processed, 15 seconds have passed, blowing the SLA. You must performance tune the Native Translator and the HTTP listener thread pools to match your expected peak concurrency.

**Real Example**: For Humana, I reduced the TAT from 13.5s to 2.5s. We validated the platform at 65K records/hour and 100 concurrent SOAP threads specifically to prove CAQH CORE SLA compliance under massive load.

**Follow-up Questions**:
- *Interviewer*: "What happens if the backend Facets system takes 30 seconds to respond?"
