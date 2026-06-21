# Eligibility Verification (270/271)

**Definition**: The real-time or batch process of a provider asking a payer if a patient has active insurance coverage on a specific date of service.

**Business Purpose**: Prevents uncompensated care. If a hospital performs surgery on a patient whose insurance expired yesterday, the hospital absorbs the entire cost.

**Real World Example**: You walk into a dentist's office. The receptionist asks for your insurance card. She types your ID into her system. In the background, a `270` is sent via APIs to Delta Dental. Two seconds later, a `271` returns saying "Active - $50 Copay" (OR, realistically, it returns "Inactive / Member Not Found", forcing the receptionist to ask for a different card or self-pay).

**Related Transactions**:
- 270 (Eligibility Inquiry)
- 271 (Eligibility Response)

**Common Interview Questions**:
- *Why is 270/271 usually a real-time transaction whereas 837 is usually batch?* (Answer: The provider needs to know *immediately* while the patient is standing at the front desk before providing care. Claims can be processed overnight.)
- *What kind of data must be in a 270 request?* (Answer: Member ID, Date of Birth, Provider NPI, Date of Service).
