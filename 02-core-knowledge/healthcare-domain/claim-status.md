# Claim Status Inquiry (276/277)

**Definition**: A request sent by a provider to a payer to determine the current processing status of a previously submitted claim.

**Business Purpose**: Cash flow predictability. Providers need to know if a $50,000 hospital claim is going to be paid tomorrow, or if it was denied and needs to be appealed. Automating this prevents thousands of phone calls to the Payer's call center.

**Real World Example**: *(Use the Humana project context here!)* Humana was receiving hundreds of thousands of 276 requests daily. We built a real-time integration pipeline to parse the 276, ping the backend CORE APIs, and generate a 277 response within 2.5 seconds, saving millions in operational costs.

**Related Transactions**:
- 276 (Inquiry)
- 277 (Response)
- 837 (The original claim being asked about)

**Common Interview Questions**:
- *What is the difference between a 277CA and a 277?* (Answer: 277CA is an automatic "receipt" acknowledging the 837 arrived safely. A 277 Claim Status Response requires actually looking up the claim deep in the adjudication system to see if it's paid or denied).
- *How would you architect a real-time 276/277 pipeline?*
