# Edifecs DataFlow

**What it is**: A visual pipeline designer within Route that handles complex, multi-step message processing, mapping, and script execution.

**Why it exists**: While "Route" moves messages between endpoints, "DataFlow" manipulates the message *inside* the pipeline. It allows chaining together Maps, Groovy scripts, validations, and external API lookups seamlessly.

**When to use it**: When a payload requires transformation, business rule execution, or external lookups before reaching its final destination.

**Real Examples**: 
- *Humana*: Built complex DataFlows to parse JSON/XML/X12 payloads, trigger Groovy scripts for member validation (DOB, ID matching) against external CORE APIs, and generate the final outbound response.

**Common Mistakes**:
- Using too many scattered Groovy script components inside a single DataFlow. Consolidating them reduces massive I/O overhead.
- Not handling exceptions properly within the DataFlow, causing the entire route to crash silently.

**Interview Questions**:
- *How did you optimize turnaround time on the Humana project?* (Answer: I identified that fragmented Groovy scripts in the DataFlow were causing latency. I consolidated the pipeline components, which shaved ~2 seconds off the overall transaction time.)
