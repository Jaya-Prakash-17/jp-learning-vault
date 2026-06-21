# Edifecs Route

**What it is**: The orchestration layer that determines how a message moves from an inbound endpoint to an outbound endpoint through various processing steps.

**Why it exists**: Data doesn't just translate; it needs to be picked up from SFTP/API, validated, routed conditionally based on content, translated, and dropped off. Route manages this overarching pipeline.

**When to use it**: Used as the backbone for any Edifecs integration to connect endpoints (JMS, HTTP, File) to internal processing components (DataFlow, Translator).

**Real Examples**: 
- *Humana*: Configured HTTP routes to ingest real-time 276 inquiries via API. The route orchestrated the payload parsing, triggered the Groovy pipeline components, and managed the synchronous HTTP response back to the client.

**Common Mistakes**:
- Creating massive, monolithic routes instead of modularizing them into reusable sub-routes.
- Hardcoding endpoint URLs instead of using environment variables, breaking the route in higher environments.

**Interview Questions**:
- *How did you handle API orchestration in Edifecs for Humana?* (Answer: Configured a synchronous HTTP route that received the 276, passed it to a DataFlow for mapping and CORE API lookups, and returned the generated 277 back down the same synchronous channel.)
