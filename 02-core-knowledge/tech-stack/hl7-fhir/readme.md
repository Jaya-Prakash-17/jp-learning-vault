# HL7 FHIR Overview

## Definition
**FHIR** (Fast Healthcare Interoperability Resources) is the modern standard for exchanging healthcare information electronically, created by the HL7 organization. 

## Why it exists
Legacy healthcare standards like X12 and HL7v2 are deeply complex, highly rigid, and rely on archaic formats (pipe-delimited or asterisk-delimited text). They are impossible for modern web and mobile developers to use easily. FHIR was created to modernize healthcare data by adopting the exact same technologies that power the rest of the internet: **RESTful HTTP APIs** and **JSON/XML** formats.

## Commands (API Usage)
FHIR operates over standard HTTP verbs.
- `curl -X GET https://server.fire.ly/Patient/123`: Retrieve patient 123.
- `curl -X GET "https://server.fire.ly/Observation?patient=123&code=8480-6"`: Search for Patient 123's systolic blood pressure.
- `curl -X POST -d @patient.json https://server.fire.ly/Patient`: Create a new patient.

## Architecture
- **Resources**: The fundamental building blocks of FHIR. Everything is a resource. A `Patient` is a resource. A `Practitioner` is a resource. An `Encounter` (a hospital visit) is a resource. 
- **References**: Resources are linked together. An `Observation` resource (like a blood test result) will have a "subject" reference pointing back to the `Patient` resource's URL.
- **Profiles**: Base FHIR is generic. A Profile is a constrained version of a resource (e.g., "The US Core Patient Profile mandates that race and ethnicity must be included").

## Interview Questions
**Q: "What is the difference between X12 and FHIR?"**
*Answer*: X12 is primarily designed for B2B financial and administrative batch processing (Claims, Remittances). It is highly compressed and heavily regulated. FHIR is a modern, RESTful API standard designed for real-time clinical data exchange (EHR integrations, patient mobile apps). 

**Q: "If a patient visits a doctor and gets a prescription, how would that map to FHIR resources?"**
*Answer*: The person is the `Patient` resource. The doctor is the `Practitioner`. The visit itself is the `Encounter`. The diagnosis is a `Condition` resource linked to the Encounter. The prescription is a `MedicationRequest` resource linked to both the Patient and the Practitioner.

## Cheat Sheet
| Concept | Explanation |
| :--- | :--- |
| **SMART on FHIR** | The security layer. It uses OAuth2 and OpenID Connect to authenticate users and authorize access to FHIR data securely. |
| **Bundle** | A FHIR resource that acts as a container to group multiple other resources together (often used for search results or bulk data). |
| **USCDI** | United States Core Data for Interoperability. The minimum baseline of health data that the US government mandates must be accessible via APIs. |
