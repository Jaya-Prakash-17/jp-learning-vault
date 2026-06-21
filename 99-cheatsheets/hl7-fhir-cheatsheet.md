# HL7 FHIR Cheat Sheet

### Core Concepts
- **FHIR**: Fast Healthcare Interoperability Resources. The modern API standard for healthcare.
- **Resources**: The fundamental building blocks (JSON/XML). Everything in FHIR is a Resource.
- **References**: How resources link together (e.g., An `Observation` references a `Patient`).
- **RESTful**: Uses standard HTTP verbs (GET, POST, PUT, DELETE) over HTTPS.

### Critical Resources
| Resource | Purpose | Example Use Case |
| :--- | :--- | :--- |
| **Patient** | Demographics | Name, DOB, MRN, Address. |
| **Practitioner**| Doctor / Nurse | NPI, Name, Specialty. |
| **Encounter** | The Visit | A specific hospital stay or telehealth appointment. |
| **Observation** | Clinical Data | Blood pressure reading, lab results. |
| **Condition** | Diagnosis | Diabetes, COVID-19 (ICD-10 codes). |
| **MedicationRequest**| Prescription | Ordering Amoxicillin. |

### API Actions (CRUD)
| HTTP Verb | Action | FHIR Example |
| :--- | :--- | :--- |
| **GET** | Search / Read | `GET /Patient/123` (Read) or `GET /Patient?name=Smith` (Search) |
| **POST** | Create | `POST /Patient` (Sends JSON body to create new patient) |
| **PUT** | Update | `PUT /Patient/123` (Updates existing patient record) |
| **DELETE** | Remove | `DELETE /Patient/123` |

### Security & Profiling
- **SMART on FHIR**: The security layer. Uses standard OAuth2 to authorize third-party apps securely.
- **USCDI**: US Core Data for Interoperability. The government-mandated minimum set of health data that must be accessible.
- **Profiles**: Constrained versions of generic FHIR resources (e.g., US Core Profile mandates Race/Ethnicity on the Patient resource).

### Interview Triggers
- 🚨 **"X12 vs FHIR"** ➡️ Trigger: X12 = Financial, Batch, Flat Text, B2B. FHIR = Clinical, Real-Time, JSON/REST APIs, Web/Mobile developer friendly.
- 🚨 **"How to find a patient's lab result"** ➡️ Trigger: Query the `Observation` resource, filtering by the `patient` reference ID and the specific LOINC `code` for that lab test.
