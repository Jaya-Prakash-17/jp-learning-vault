# API Integrations

**Question**: How did you handle API orchestration in the Humana project?

**CORE APIs & ECIS Services**:
- **Purpose**: Real-time lookups for member validation and claim status orchestration.
- **Protocol**: Orchestrated both REST (JSON) and SOAP (XML) calls directly within the Edifecs pipeline.
- **Transformation**: Built mapping logic to convert inbound X12 276 data into the specific JSON/XML schemas required by the CORE APIs, and vice versa for the response.

**Load Management & Threading**:
- **Concurrency**: The platform was load-tested and validated to support 100 concurrent SOAP threads.
- **Timeouts**: Configured strict timeout thresholds on external API calls to ensure the overall 2.5s turnaround SLA was not breached by slow backend responses.
