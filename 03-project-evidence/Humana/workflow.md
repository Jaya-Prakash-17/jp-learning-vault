# Workflow

**Question**: Walk me through the end-to-end EDI workflow for the Humana 276/277 service.

**1. Ingress & Parsing**
- Receive inbound 276 payload.
- Edifecs validates the payload structure (SNIP levels 1 & 2).
- Transform X12 payload into structured JSON/XML for processing.

**2. Orchestration & Lookups**
- Trigger ECIS services and CORE APIs.
- Execute member validation (ID, DOB match).
- Perform claim status lookup in Humana's backend systems.

**3. Business Logic Execution**
- Execute Groovy scripts for complex conditional logic and data manipulation.
- Determine if the claim is pending, paid, or denied based on backend response.
- Map the backend status to standardized X12 STC (Status Information) segments.

**4. Egress & Response**
- Native Translator builds the final 277 X12 payload.
- Final validation of outbound payload to ensure HIPAA compliance.
- Transmit the real-time response back to the provider within the strict 2.5s SLA.
