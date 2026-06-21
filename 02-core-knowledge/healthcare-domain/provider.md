# The Provider & NPI

**Definition**: The individual or organization delivering medical care. Every provider in the US is identified universally by a 10-digit National Provider Identifier (NPI).

**Business Purpose**: Routing, billing, and fraud prevention. Payers maintain massive "Provider Directories". If an out-of-network provider submits a claim, the Payer will pay significantly less. Companies like Zelis specialize in managing these complex provider network databases.

**Real World Example**: Dr. Smith (Individual NPI) works at General Hospital (Organizational NPI). When a claim is submitted, it must include both: Dr. Smith as the "Rendering Provider" and General Hospital as the "Billing Provider".

**Related Transactions**:
- Provider data is present on literally every healthcare transaction (837, 270, 276, 278, 835).

**Common Interview Questions**:
- *What is an NPI?* (Answer: A unique 10-digit identification number issued to health care providers in the US by CMS).
- *What is the difference between a Billing Provider and a Rendering Provider?* (Answer: Rendering actually performed the surgery. Billing is the corporate hospital entity that collects the money).
