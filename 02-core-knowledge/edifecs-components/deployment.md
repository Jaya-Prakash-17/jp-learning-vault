# Deployment & Migration

**What it is**: The process of moving Edifecs artifacts (Maps, Profiles, Routes, DataFlows) from lower environments (Dev) to higher environments (Test, Staging, Prod).

**Why it exists**: To maintain strict version control and ensure that code tested in Dev behaves exactly the same way in Production.

**When to use it**: During release cycles, phase go-lives, or applying critical hotfixes.

**Real Examples**: 
- *Humana Phase-1 Go-Live*: Managed the packaging and deployment of the real-time 276/277 routes, custom Groovy scripts, and X12 STC error handling frameworks into the production environment, securing formal written appreciation for a successful zero-downtime delivery.

**Common Mistakes**:
- Forgetting to migrate global properties or external dependencies (like Groovy JARs), causing routes to fail immediately in Prod.
- Hardcoding environment-specific URLs (like DEV CORE API endpoints) in Maps or Scripts instead of using dynamic environment properties.

**Interview Questions**:
- *What precautions do you take before a production go-live?* (Answer: Ensure all endpoint URLs are parameterized, verify thread pool configurations match the anticipated production load, and ensure TM logging levels are set to ERROR/WARN rather than DEBUG to prevent database bloat.)
