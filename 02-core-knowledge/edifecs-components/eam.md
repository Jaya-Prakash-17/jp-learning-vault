# Edifecs Application Manager (EAM) / Admin

**What it is**: The centralized administration and management console for the Edifecs runtime environment.

**Why it exists**: Enterprise integrations require active monitoring, configuration, and control. EAM provides the dashboard to manage services, monitor server health, and configure global properties.

**When to use it**: Used by administrators and integration engineers to deploy new routes, check system logs, manage ports, and configure thread pools.

**Real Examples**: 
- *Humana*: Utilized the EAM console to monitor the real-time 276/277 service. We actively tracked transaction volumes (200K-300K/day) and monitored thread pool exhaustion when tuning the Native Translator for performance.

**Common Mistakes**:
- Failing to configure appropriate log rotation, causing the server disk to fill up during high-volume processing.
- Leaving thread pools at default settings for high-throughput, synchronous environments.

**Interview Questions**:
- *How do you monitor the health of an Edifecs deployment?* (Answer: Via EAM dashboards, checking component states, queue depths, and actively monitoring the server logs for OutOfMemory errors or thread deadlocks.)
