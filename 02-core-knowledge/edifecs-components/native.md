# Native Engine

**What it is**: The underlying core execution engine in Edifecs optimized for maximum performance, written in highly efficient Native code (C++).

**Why it exists**: Processing 200K+ heavy X12 files per day requires immense CPU and memory efficiency. Java-based parsing can hit severe garbage collection bottlenecks. The Native engine bypasses this to provide maximum throughput.

**When to use it**: In extreme high-throughput, high-volume environments (like Clearinghouses or major Payers) where standard Java execution is too slow to meet SLAs.

**Real Examples**: 
- *Humana*: To achieve the 65K records/hour validation rate and support 100 concurrent SOAP threads for the real-time 276/277 service, we had to heavily rely on the Native execution path, collaborating with senior engineers to optimize its thread allocation.

**Common Mistakes**:
- Misconfiguring the thread pool allocation, leading to thread starvation and system lockups under heavy concurrent load.
- Assuming the Native engine handles all custom Java/Groovy logic (it doesn't; it handles core validation and translation).

**Interview Questions**:
- *Why would thread optimization matter in an Edifecs environment?* (Answer: In a real-time synchronous flow like the Humana 276/277 project, thread exhaustion in the Native engine will cause incoming API requests to queue and timeout, breaching the 2.5s SLA.)
