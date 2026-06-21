# Payer vs. Provider

**Definition**: 
- **Payer**: The entity that finances or reimburses the cost of health services (e.g., Insurance Companies like Humana, Aetna, Medicare).
- **Provider**: The entity that delivers healthcare services to the patient (e.g., Hospitals, Clinics, Pharmacies, Individual Doctors).

**Business Purpose**: Payers collect premiums and manage financial risk. Providers deliver care and bill for services. The friction between them (getting claims approved vs. denying invalid claims) drives the entire healthcare IT integration industry (Optum, Edifecs, Gainwell).

**Real World Example**: 
- *Payer System*: Humana uses integration engines to ingest millions of incoming claims, automatically denying those where the patient wasn't covered.
- *Provider System*: Mayo Clinic uses Epic (EHR) to automatically generate and send batch files of claims every night to various payers to ensure their doctors get paid.

**Related Transactions**:
- Providers send: 270 (Check Eligibility), 837 (Submit Claim), 276 (Check Status)
- Payers send: 271 (Eligibility Answer), 835 (Payment Details), 277 (Status Answer)

**Common Interview Questions**:
- *If you are building an integration for a Payer, what is your primary concern regarding inbound 837 claims?* (Answer: Validity, fraud prevention, formatting, and member verification).
- *What is the difference between a Payer and a Clearinghouse?*
