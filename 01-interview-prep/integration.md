# Integration Patterns

## 1. Architecture & The Need
- **The Need**: Systems speak different languages. A hospital's mainframe might output flat X12 files, but a modern Payer's adjudication system requires nested JSON REST APIs.
- **Architecture**: Middleware engines sit between systems. They decouple the source format from the destination format, handling translation, orchestration, authentication, and routing.

## 2. Core Concepts
- **Translation vs Transformation**: Translation is changing the format (X12 string -> XML DOM). Transformation is changing the structure (XML DOM -> differently mapped JSON).
- **Synchronous vs Asynchronous**: Sync (HTTP) requires the connection to remain open until a response is received (e.g., 276/277). Async (SFTP/JMS) means dropping a file and walking away (e.g., Batch 837s).
- **REST vs SOAP**: REST uses JSON and standard HTTP verbs (GET/POST). SOAP uses rigid XML and WSDL definitions.

## 3. Basic Daily Workflows
- **API Testing**: Using Postman to simulate incoming JSON requests or mock external dependencies.
- **Mapping**: Drawing lines from Source Node to Target Node in tools like MapBuilder to align data fields.
- **Error Review**: Investigating HTTP 500 (Server Error) or HTTP 400 (Bad Request) status codes in logs.

## 4. Advanced Scenarios
- **Throttling & Rate Limiting**: Implementing queues (JMS/Kafka) so a batch of 50,000 X12 claims doesn't accidentally DDOS an internal REST API that can only handle 10 requests per second.
- **Handling Nulls & Data Types**: Converting X12 (which is entirely strings) to strict JSON schemas (which require decimals, booleans, and arrays).
- **OAuth2**: Automatically handling token expiry and refresh flows before hitting external APIs.

---

## Interview Question Deep Dive

### Q: "How do you handle transforming a flat, delimited legacy X12 file into a deeply nested JSON REST API payload?"

**30-Second Answer**: I use an integration engine to first parse the X12 text into an internal XML DOM. Then, I apply mapping logic—using visual tools like MapBuilder or scripts like Groovy—to extract the necessary fields, handle looping structures, and construct the final JSON payload.

**2-Minute Answer**: Direct string-parsing of X12 to JSON is a nightmare because X12 relies on contextual loops. For example, the `NM1` segment means "Provider" in loop 2000A, but means "Patient" in loop 2000C. The architecture requires a two-step process:
1. **Translation**: The Native Translator reads the X12 and builds an XML tree in memory, assigning context to each segment.
2. **Transformation**: I use MapBuilder to map the nodes. For repeating X12 structures (like multiple Service Lines in loop 2400), I implement `For-Each` loops in the map to generate corresponding JSON arrays. 

**Deep Dive Answer**: The real difficulty lies in data typing and null handling. X12 segments are often optional. If your mapping logic attempts to pull a patient's middle initial from an X12 file where the `NM104` element is missing, it will throw a Null Pointer Exception. You must wrap your mapping logic in `If-Exists` conditionals and cast the string values to the appropriate primitive types before generating the JSON payload.

**Real Example**: During the State of Colorado project, I built 837I to XML maps. I heavily utilized conditional, element-level logic to ensure that optional institutional billing codes were only mapped if present, preventing the entire pipeline from failing on sparse claims.

**Follow-up Questions**:
- *Interviewer*: "What if the target JSON API rate limits your requests to 10 per second, but your batch 837 file has 5,000 claims?"
