# Role Profile: Healthcare Solution Architect

## The Role
The Solution Architect does not write the code or build the maps. The Architect sits in a room with the client's CIO, looks at their 15-year-old legacy mainframe, and designs the blueprint for how to migrate it to AWS using modern middleware, ensuring it complies with HIPAA and CAQH. 

## Core Responsibilities
- Designing highly available (HA), fault-tolerant integration pipelines.
- Selecting the right technology stack (e.g., "We should use Kafka for the queue, Edifecs for the validation, and AWS S3 for the archive").
- Defining security postures (OAuth2, TLS, encryption at rest for PHI).
- Creating architectural diagrams and presenting them to executive leadership.

## Why You Want This
- **The Pinnacle**: This is the highest technical individual contributor (IC) role. It commands the highest salary and the most respect.
- **Strategic Impact**: You are no longer fixing bugs; you are preventing them from existing by designing flawless systems.

## The Interview Focus
To pass an interview for this role, you must demonstrate:
1. **System Design**: You will be given a whiteboard (or virtual equivalent) and asked to design a system from scratch. (e.g., "Design a clearinghouse that can ingest 1 million 837 claims a day, validate them, and route them to 50 different payers").
2. **Trade-off Analysis**: You must be able to explain *why* you chose a specific technology. ("I chose an asynchronous SQS queue here instead of a synchronous HTTP call because the backend system cannot handle peak load and needs throttling").
3. **Executive Presence**: Can you explain a highly complex technical architecture to a non-technical VP of Finance?

## Target Keywords for Resume
- System Design & Architecture
- High Availability (HA) / Disaster Recovery (DR)
- AWS / Cloud Migration
- HL7 FHIR / Modern Interoperability
- CAQH CORE Compliance Architect
