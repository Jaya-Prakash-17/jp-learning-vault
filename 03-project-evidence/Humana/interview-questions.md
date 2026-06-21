# Interview Questions

**Self-Testing Q&A (Humana Project)**

1. **"Can you describe a time you significantly improved system performance?"**
   - *Strategy*: Highlight the Humana 80% TAT reduction. Detail the Groovy script consolidation and Native Translator tuning.

2. **"How do you handle API failures in a real-time EDI pipeline?"**
   - *Strategy*: Discuss the custom error-handling framework and the use of X12 STC segments for graceful degradation (handling timeouts, DOB mismatches, and member-not-found scenarios).

3. **"Describe the scale of the systems you've worked on."**
   - *Strategy*: Quote the Humana metrics directly: 200K-300K daily transactions, 65K records/hour load testing, 100 concurrent SOAP threads.

4. **"Have you ever had to integrate legacy EDI with modern APIs?"**
   - *Strategy*: Explain the workflow of parsing an X12 276, transforming it to JSON/XML for CORE API lookups, and generating the outbound X12 277 response.
