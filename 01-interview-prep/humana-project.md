# Humana Project Deep Dive

## 1. The Need (Business Purpose)
- **The Need**: Humana was experiencing massive call center volume from providers asking "Where is my claim?" Legacy batch processing took days to return a status. They needed a real-time, sub-3-second synchronous API to instantly return claim statuses (276/277).

## 2. Core Concepts
- **Synchronous Integration**: The HTTP socket stays open until the final EDI response is generated.
- **Orchestration**: Using Groovy to coordinate multiple REST API calls (Demographics, Claim Status) inside a single transaction.
- **Graceful Degradation**: If an internal system fails, returning a compliant X12 STC error rather than breaking the socket.

## 3. Basic Daily Workflows
- **Monitoring Load**: Watching the EAM dashboard to ensure the 65K records/hour load was not exhausting thread pools.
- **Payload Triaging**: Using Transaction Manager to trace a failed 276 request to see if the failure happened at the API Gateway (authentication) or the DataFlow (mapping).

## 4. Advanced Scenarios
- **Native Translator Tuning**: Adjusting the `server.xml` to balance HTTP listener threads with X12 parsing threads to prevent queuing under heavy concurrent load.
- **Consolidating Groovy**: Refactoring multiple scattered Groovy components into a single, optimized script to eliminate the massive I/O overhead of passing payloads between nodes.

---

## Interview Question Deep Dive

### Q: "Walk me through the architecture of your Humana 276/277 solution."

**30-Second Answer**: We exposed a synchronous API to ingest X12 276 inquiries. The payload was validated via Edifecs Profiles, parsed into XML using the Native Translator, and run through a DataFlow. Inside the DataFlow, Groovy scripts orchestrated CORE API lookups to validate the member and fetch claim status. The JSON response was then mapped back to an X12 277 and returned to the client in under 3 seconds.

**2-Minute Answer**: The challenge was the volume (300K/day) and the strict latency SLA. The architecture started with the Edifecs API Gateway. Once a 276 arrived, it bypassed heavy database logging to save I/O time. It entered the DataFlow, where we used MapBuilder to translate the X12 NM1/DMG segments into a JSON payload. This JSON was sent via a REST component to Humana's internal ECIS services to verify the Date of Birth and Member ID. 

If the member was found, we fetched the claim status from Facets. Then, we mapped the internal status codes to standard X12 STC (Status Information) segments. Finally, the Native Translator rebuilt the X12 277 string, and the Route returned the HTTP response to the provider.

**Deep Dive Answer**: The most critical architectural decision was the custom error-handling framework. In a synchronous HTTP route, if the backend CORE API returns a 500 error or times out, Edifecs will naturally crash the route and return a raw stack trace to the provider, which violates HIPAA/CAQH rules. I implemented `try/catch` logic within the Groovy pipeline. If the API timed out, we caught it, instantiated a dummy XML response, mapped an STC segment indicating "System Unavailable," and pushed it to the Translator. This guaranteed a compliant response even during outages.

**Real Example**: This architecture successfully validated at 65K records/hour and 100 concurrent SOAP threads, resulting in an 80% TAT reduction (from 13.5s to 2.5s).

**Follow-up Questions**:
- *Interviewer*: "How did you prove the system could handle 65K records/hour?"
