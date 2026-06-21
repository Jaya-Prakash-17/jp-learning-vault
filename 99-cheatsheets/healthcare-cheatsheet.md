# Healthcare Domain Cheat Sheet

### Core Concepts
| Term | Definition |
| :--- | :--- |
| **Payer** | Insurance company (e.g., Aetna, Humana) that pays the claims. |
| **Provider** | Hospitals, Clinics, Physicians that render medical care. |
| **Clearinghouse** | Middleman that batches, scrubs, and routes EDI files between Providers and Payers. |
| **Adjudication** | Payer's automated rules engine determining whether to pay, deny, or reduce a claim. |
| **Prior Auth** | Provider requesting Payer's permission *before* performing expensive procedures. |
| **CAQH CORE** | Operating rules mandating real-time SLA limits (e.g., 20 seconds max for a 276/277). |
| **NPI** | National Provider Identifier (10-digit ID for doctors/hospitals). |

### Financial Terminology
- **Premium**: The monthly subscription fee paid to the Payer.
- **Copay**: A fixed dollar amount the patient pays at the door (e.g., $20 for a doctor visit).
- **Deductible**: The amount the patient must pay out-of-pocket before insurance covers *anything*.
- **Co-insurance**: The percentage split after the deductible is met (e.g., 80% Payer / 20% Patient).

### Mnemonics & Mental Models
- **PPP**: **P**atients **P**ay **P**remiums. **P**roviders **P**rovide **P**rocedures.
- **The Golden Trinity**: To get paid, a claim must perfectly match three things: **Member ID + Date of Birth + NPI**. 

### Interview Triggers
- 🚨 **"Member Not Found"** ➡️ Trigger: Check the 834 Enrollment file for demographic mismatch (DOB/Name).
- 🚨 **"API Timeout"** ➡️ Trigger: CAQH CORE SLA violation. Implement graceful degradation (STC segment).
