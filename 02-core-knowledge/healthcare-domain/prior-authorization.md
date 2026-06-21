# Prior Authorization (278)

**Definition**: The process where a provider must obtain advance approval from the payer before delivering a specific medical service or medication.

**Business Purpose**: Cost control for the Payer. It prevents unnecessary expensive procedures (like MRIs or experimental drugs). For companies like Cognizant and Optum, automating this process using AI and APIs is a massive business opportunity.

**Real World Example**: A doctor wants to prescribe a $5,000/month specialty drug. Before the pharmacy can dispense it, they send a `278` request with the patient's diagnosis. The Payer reviews it (often manually by a nurse) to ensure a cheaper generic drug shouldn't be tried first.

**Related Transactions**:
- 278 Request
- 278 Response
- 275 (Attachments - sending medical records to justify the 278)

**Common Interview Questions**:
- *What is the biggest pain point in the Prior Authorization workflow?* (Answer: It is heavily manual, often requiring faxes and PDF medical records, delaying critical patient care).
- *What is the difference between Eligibility (270) and Prior Auth (278)?* (Answer: 270 asks "Does this person have insurance?". 278 asks "Will you pay for this *specific, expensive procedure*?").
