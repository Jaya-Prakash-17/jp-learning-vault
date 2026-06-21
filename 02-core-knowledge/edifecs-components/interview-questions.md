# Edifecs Technical Interview Questions

**Self-Testing Q&A (Platform & Components)**

**1. "What is the role of Route vs. DataFlow?"**
*Answer*: Route is the highway—it connects endpoints (like an HTTP listener) to internal processes. DataFlow is the factory—it sits inside the Route and manipulates, maps, and executes business logic on the payload.

**2. "How did you reduce turnaround time for Humana?"**
*Answer*: 
1. Consolidated scattered Groovy scripts in the DataFlow to reduce execution overhead. 
2. Collaborated on Native Translator tuning to optimize how X12 strings were parsed into XML. 
3. Optimized thread allocation for SOAP concurrent requests.

**3. "Why use MapBuilder instead of writing Java code?"**
*Answer*: MapBuilder is purpose-built for healthcare EDI. It handles complex looping, hierarchical X12 structures, and SNIP validations natively, which would require massive amounts of fragile, hard-to-maintain code in raw Java.

**4. "How do you handle custom business rules that SpecBuilder can't handle?"**
*Answer*: I use Groovy scripts embedded within the DataFlow. For example, during the Humana project, I used Groovy to perform complex string manipulation and logic evaluation for member validation against the ECIS services.

**5. "If a route is performing slowly in production, where do you look first?"**
*Answer*: Check EAM for thread exhaustion or memory leaks. Then check Transaction Manager to isolate which specific component (e.g., the Translator, or an external API call) is taking the most time. In Humana, we found legacy Groovy components were causing massive I/O latency.
