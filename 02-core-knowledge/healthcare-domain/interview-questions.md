# Domain Interview Questions

**Self-Testing Q&A (Healthcare Domain)**

**1. "Explain the flow of an 837 and an 835."**
*Answer*: A provider treats a patient and submits an 837 (Claim) to the payer. The payer adjudicates the claim through their business rules. Once finalized, the payer issues an EFT (money to the bank) and an 835 (Remittance Advice) to the provider explaining exactly how the claim was paid or why it was denied.

**2. "What happens if an 837 has a syntax error?"**
*Answer*: The clearinghouse or payer's integration engine will fail the file at SNIP Level 1 or 2. It will instantly generate a 999 or 277CA rejection back to the provider before the claim ever reaches the adjudication system.

**3. "Why is HIPAA important in your role as an integration engineer?"**
*Answer*: Because we handle PHI (Protected Health Information) in transit. Payloads (JSON/XML/X12) must be encrypted, access must be logged, and error-handling logs cannot bleed PHI into plain-text dashboards.

**4. "What is the difference between a clearinghouse and a payer?"**
*Answer*: A clearinghouse is a middleman (like Change Healthcare). They act as a post office, taking claims from thousands of providers, scrubbing them for errors, and routing them to the correct Payer. The Payer holds the actual money and assumes the financial risk.

**5. "How do you map a legacy X12 file to a modern REST API?"**
*Answer*: Use an integration engine to parse the delimited X12 file into an internal XML/JSON DOM. Then execute mapping rules to extract the necessary fields (like Member ID, DOB from the NM1/DMG segments) and bind them to the target API JSON schema.
