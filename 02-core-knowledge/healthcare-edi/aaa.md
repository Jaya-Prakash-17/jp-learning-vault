# AAA Segment (Request Validation)

**30-Second Explanation**: The segment inside a 271 Eligibility Response that explicitly states *why* an eligibility check failed.

**2-Minute Explanation**: If a provider sends a 270 Eligibility request and the Payer cannot find the patient, the Payer doesn't just drop the file. They return a 271 Response containing an AAA segment. The AAA segment provides standard codes explaining the exact error, such as "Member Not Found", "Invalid Date of Birth", or "Coverage Expired".

**Purpose**: To communicate validation errors specifically related to member eligibility and demographic mismatches.

**Who sends it**: Payers (inside 271s).

**Who receives it**: Providers.

**Input**: Demographic mismatch detected in the Payer's backend.

**Output**: E.g., `AAA*Y**71*C` (Translation: Patient Birth Date Does Not Match).

**Common Errors**: 
- Failing to return an AAA segment when a member isn't found, leaving the provider confused as to why the 271 is empty.

**Real Project Example**: Just as I used STC segments to handle errors in the Humana 277 project, AAA segments are used for the exact same purpose (error handling and graceful degradation) in 271 Eligibility DataFlows.

**Interview Questions**:
- *What segment is used to report a missing member in a 271?* (Answer: The AAA segment).
