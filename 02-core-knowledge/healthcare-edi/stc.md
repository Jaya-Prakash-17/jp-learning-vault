# STC Segment (Status Information)

**30-Second Explanation**: The segment inside a 277 response that explicitly states the status of a claim or the specific error that occurred.

**2-Minute Explanation**: When you send a 277 back to a provider, you can't just type free-text saying "We denied this because the DOB is wrong." You must use standardized STC codes. The STC segment combines a Category Code, a Status Code, and an Entity Code to create a highly specific, machine-readable message.

**Purpose**: To provide standardized, HIPAA-compliant status updates and error messages.

**Who sends it**: Payers (inside 277s).

**Who receives it**: Providers.

**Input**: Business logic or exception catch blocks.

**Output**: E.g., `STC*A3:21*20230621*U*500` (Translation: Rejected: Missing Member ID).

**Common Errors**: 
- Using non-standard STC codes, causing the provider's software to crash when trying to read the 277.

**Real Project Example**: At Humana, I architected the custom error-handling framework specifically around STC segments. If our CORE API lookup timed out, my Groovy exception handler caught the error and mapped it to a specific STC segment indicating "System Unavailable", ensuring the route didn't crash and the provider received a compliant response.

**Interview Questions**:
- *How do you handle backend API failures in an EDI pipeline?* (Answer: Catch the HTTP exception in the DataFlow and map it to a standard X12 STC error segment inside a 277 payload).
