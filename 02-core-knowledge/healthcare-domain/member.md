# The Member (Subscriber vs. Dependent)

**Definition**: The patient or individual covered by the health insurance plan. 

**Business Purpose**: Data integrity. Almost all EDI transaction failures (like the DOB-mismatches handled in the Humana project) stem from bad member demographic data. Integrations must perfectly map and validate member data.

**Real World Example**: 
- **Subscriber**: The mother who gets insurance through her employer.
- **Dependent**: The child who is covered under the mother's plan.
When the child goes to the doctor, the 837 claim must clearly distinguish that the *Patient* is the child, but the *Subscriber* holds the policy.

**Related Transactions**:
- 834 (Used by HR/Employers to enroll the Member into the Payer's system)
- 270 (Uses Member ID to check eligibility)

**Common Interview Questions**:
- *What is the difference between a Subscriber and a Patient?* (Answer: Subscriber owns the policy. Patient is the one receiving care. They can be the same person, or different).
- *If an 837 claim fails with "Member Not Found", what usually went wrong?* (Answer: The name, DOB, or Member ID submitted by the provider didn't perfectly match what the Payer has on file from the 834 enrollment).
