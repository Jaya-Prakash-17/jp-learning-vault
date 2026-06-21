# The Story of a Healthcare Transaction

**Definition**: The end-to-end lifecycle of a patient interacting with the healthcare system, mapped directly to EDI X12 transactions.

**The Story**:
1. **Enrollment (834)**: A patient (the Subscriber) purchases an exclusive health insurance policy directly from a Payer (the Insurance Company). The Payer processes an `834 Benefit Enrollment` transaction to register the patient as an active Member in their core adjudication system.
2. **Eligibility (270/271)**: The patient falls ill and visits a local Hospital (the Provider). At the front desk, the receptionist needs to verify coverage. The hospital's system sends a `270 Eligibility Request` to the Payer. Within seconds, the Payer returns a `271 Eligibility Response` confirming the patient's active coverage (OR returning an error if the policy is inactive or the member is not found, forcing the patient to self-pay).
3. **Prior Authorization (278)**: The physician examines the patient and determines an expensive MRI is necessary. To ensure the Payer will cover the cost, the hospital submits a `278 Prior Authorization Request` before performing the scan. The Payer reviews the medical necessity and sends back a `278 Response` granting approval for the procedure (OR denying it if deemed not medically necessary, halting the procedure).
4. **The Claim (837)**: Following the approved MRI, the patient is discharged. The hospital's billing department generates an `837 Health Care Claim`, detailing the exact diagnosis and procedure codes, and transmits it to the Payer for reimbursement.
5. **Claim Acknowledgment (277CA)**: The Payer's integration gateway receives the file and immediately replies with a `277CA Claim Acknowledgment`, indicating that the file passed initial HIPAA syntax checks and is accepted for processing (OR rejecting the entire file instantly if the X12 syntax is malformed).
6. **Claim Status (276/277)**: After a week with no payment, the hospital's billing software automatically fires a `276 Claim Status Request` to the Payer. The Payer's system responds instantly with a `277 Claim Status Response`, noting that the claim is currently "pending final review."
7. **Payment & Remittance (835)**: Once the Payer fully adjudicates the claim, they either approve it (transferring funds via EFT) OR deny it completely. Simultaneously, the Payer sends an `835 Electronic Remittance Advice (ERA)` to the hospital, explaining the exact payment amount, contractual write-offs, or the specific business reason for the denial.

**Business Purpose**: Understanding this flow is mandatory for companies like Cotiviti, Optum, or Cognizant, as they build systems that intercept, audit, and route these exact transactions between Payers and Providers.

**Common Interview Questions**:
- *Walk me through the lifecycle of a claim from the patient's perspective to final payment.*
