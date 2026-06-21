# The Claim Lifecycle

**Definition**: The journey of a medical bill from creation at the provider's office to final payment by the insurance company.

**Business Purpose**: Tracking the financial pulse of healthcare. If claims get stuck or lost, providers go bankrupt. Companies like Zelis and Cotiviti exist to optimize, audit, and speed up this exact lifecycle.

**The Stages**:
1. **Encounter**: Patient sees a doctor. A medical coder translates the visit into ICD-10 (diagnosis) and CPT (procedure) codes.
2. **Submission (837)**: The claim is sent (usually via a Clearinghouse) to the Payer.
3. **Adjudication**: The Payer's core system (like Facets or QNXT) runs massive sets of business rules against the claim. Did the patient have insurance? Was the procedure medically necessary? (Note: Adjudication's primary purpose is often to find reasons to *deny* or *reduce* the payment based on strict policies, not just to blindly pay it).
4. **Status Check (276/277)**: Provider pings Payer to ask "Where is my money?"
5. **Payment/Denial (835)**: Payer issues the final decision and explanation of payment.

**Real World Example**: A single error in a patient's Date of Birth on an 837 claim will cause the Payer's adjudication system to instantly deny the claim (Member Not Found), forcing the provider to fix and resubmit it weeks later.

**Related Transactions**:
- 837 (Submission)
- 999 / 277CA (Acknowledgment)
- 276/277 (Status)
- 835 (Payment)

**Common Interview Questions**:
- *What is Adjudication?* (Answer: The automated process a payer uses to decide whether to pay, deny, or reduce a claim based on policies and contracts).
- *Where do clearinghouses fit into the claim lifecycle?*
