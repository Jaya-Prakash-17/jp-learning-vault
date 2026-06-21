# US Healthcare Overview

**Definition**: The US Healthcare system is a multi-trillion dollar network of payers (insurance companies), providers (hospitals/doctors), and members (patients), driven by complex data exchanges heavily regulated by HIPAA.

**Business Purpose**: To deliver medical care to members while ensuring providers are compensated correctly by payers based on contracted rates, medical necessity, and eligibility.

**Real World Example**: An Optum integration engineer builds a pipeline to safely route claims from thousands of independent doctors into a centralized payer system like UnitedHealthcare, ensuring data isn't lost or corrupted.

**Related Transactions**:
- 834 (Enrollment)
- 270/271 (Eligibility)
- 837 (Claim)
- 835 (Remittance)

**Common Interview Questions**:
- *How does money flow in the US Healthcare system?* (Answer: Member pays premium to Payer. Provider treats Member. Provider bills Payer. Payer pays Provider).
- *What is the role of a Clearinghouse?* (Answer: An intermediary that checks claims for errors before routing them to the correct payer).
