# Edifecs Transaction Management (TM)

**What it is**: The component responsible for tracking, storing, and providing visibility into the lifecycle of every transaction processed by the platform.

**Why it exists**: In healthcare, if a claim is lost, the provider doesn't get paid. TM provides the audit trail and visibility needed for compliance, troubleshooting, and reporting.

**When to use it**: It runs continuously in the background. Integration engineers query TM to trace exactly where a specific payload failed or to prove that an SLA was met.

**Real Examples**: 
- *Humana*: For the 276/277 modernization, we needed to ensure our turnaround time SLA (under 3s) was being met. TM allowed us to trace the lifecycle of a 276 entering the system and the 277 leaving, proving we hit the 2.5s-3s mark.

**Common Mistakes**:
- Logging the entire raw payload (PHI) into TM dashboards without masking, causing severe HIPAA violations.
- Over-logging every minor step in a high-volume real-time pipeline, which destroys database performance.

**Interview Questions**:
- *If a provider claims they sent an 837 but the backend didn't receive it, how do you troubleshoot?* (Answer: Search Transaction Manager using the specific ISA Control Number, Member ID, or Provider NPI to trace the payload's journey and find the exact point of failure.)
