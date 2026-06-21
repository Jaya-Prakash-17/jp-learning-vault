# Remittance Advice (835)

**Definition**: The electronic document (Electronic Remittance Advice - ERA) sent by a payer to a provider explaining exactly how a claim was processed, including payments, adjustments, and denials.

**Business Purpose**: Auto-posting. Providers use the 835 to automatically reconcile their accounting systems. Without the 835, accountants would have to manually read paper checks to figure out which patients' bills were paid.

**Real World Example**: A doctor bills $200 (via 837). The payer's contracted rate is only $150. The payer sends an 835 that says: "Billed: $200. Paid: $120. Patient Owes (Copay): $30. Contractual Adjustment (Write-off): $50."

**Related Transactions**:
- 835 (The ERA)
- 837 (The original claim)
- EFT (Electronic Funds Transfer - the actual money sent to the bank, which ties to the 835 via a trace number).

**Common Interview Questions**:
- *How does the provider link the money in their bank to the 835 file?* (Answer: Through the TRN (Trace Number) segment which is present in both the 835 and the bank's EFT payload).
- *What are Claim Adjustment Reason Codes (CARC)?* (Answer: Standardized codes in the 835 explaining *why* a claim wasn't paid in full, e.g., "CO-45: Charge exceeds fee schedule").
