# Healthcare EDI (X12) Cheat Sheet

### Envelope Structure
- **ISA/IEA**: Interchange (Outer shipping box. Identifies Sender/Receiver).
- **GS/GE**: Functional Group (The folder. Batches similar transactions together).
- **ST/SE**: Transaction Set (The actual letter/document data).

### SNIP Validation Levels
| Level | Focus | Failure Example |
| :--- | :--- | :--- |
| **SNIP 1** | Integrity / Syntax | Broken delimiters (`*` or `~`). Mismatched ISA/IEA. |
| **SNIP 2** | HIPAA Structure | Missing a mandatory segment (e.g., No `N4` City). |
| **SNIP 3** | Balancing | `Claim Total` does not equal `Sum of Service Lines`. |

### X12 Transaction Dictionary
| Code | Name | Direction | Sync/Async |
| :--- | :--- | :--- | :--- |
| **270** | Eligibility Inquiry | Provider ➡️ Payer | Real-Time |
| **271** | Eligibility Response | Payer ➡️ Provider | Real-Time |
| **276** | Claim Status Request | Provider ➡️ Payer | Real-Time |
| **277** | Claim Status Response| Payer ➡️ Provider | Real-Time |
| **278** | Prior Authorization | Provider ↔️ Payer | Real/Batch |
| **834** | Benefit Enrollment | Employer ➡️ Payer | Batch |
| **837(I/P/D)** | Health Care Claim | Provider ➡️ Payer | Batch |
| **835** | Remittance Advice (ERA)| Payer ➡️ Provider | Batch |
| **820** | Premium Payment | Employer ➡️ Payer | Batch |

### Acknowledgments & Errors
- **TA1**: Rejects bad ISA envelopes instantly.
- **999**: Implementation Ack. Accepts/Rejects file based on SNIP 1 & 2.
- **277CA**: Claim Ack. Business receipt (Accepts syntax, does *not* mean claim is paid).
- **STC**: Status Segment (Used inside 277s to explain *why* a claim failed).
- **AAA**: Error Segment (Used inside 271s to explain *why* a member wasn't found).

### Interview Triggers
- 🚨 **"Real-time vs Batch"** ➡️ Trigger: 27X = Inquiries (Real-time). 83X = Dumps of data (Batch).
- 🚨 **"Missing Mandatory Segment"** ➡️ Trigger: SNIP 2 Failure. Found by reading the `IK4` segment in the 999.
