# EDI Technical Interview Questions

**Self-Testing Q&A (X12 & EDI)**

**1. "What is the difference between a 276/277 and a 270/271?"**
*Answer*: 270/271 is for Eligibility (checking if a patient has insurance *before* care is given). 276/277 is for Claim Status (checking if a claim will be paid *after* care is given and billed). Both are usually real-time.

**2. "Explain SNIP Levels 1 and 2."**
*Answer*: SNIP 1 is EDI syntax—checking basic X12 delimiters and envelope structure (ISA/GS). SNIP 2 is structural HIPAA compliance—checking for mandatory segments, correct code sets, and maximum element lengths.

**3. "How does a provider know if their 837 batch was accepted?"**
*Answer*: The payer's gateway will instantly return a 999 (validating X12 structure) and a 277CA (Claim Acknowledgment validating front-door business rules).

**4. "What happens if you submit an 837 without a prior authorization for a mandatory procedure?"**
*Answer*: The adjudication system will deny the claim. The denial will be communicated back to the provider weeks later on an 835 Remittance Advice using a specific CARC code.

**5. "How do you handle a scenario where an external API times out during a real-time EDI transaction?"**
*Answer*: In systems like Edifecs, I wrap the API call in an exception handler. If it times out, I catch it and map a standardized X12 STC segment (for 277s) or AAA segment (for 271s) indicating a system timeout, ensuring the provider receives a valid EDI response rather than a broken socket.
