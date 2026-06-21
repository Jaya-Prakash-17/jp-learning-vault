# Edifecs Cheat Sheet

### Core Components
| Component | Function | Usage |
| :--- | :--- | :--- |
| **SpecBuilder** | Validation Rules IDE | Create/Clone HIPAA Profiles. Configure SNIP 1-7 rules. |
| **MapBuilder** | Translation Logic IDE | Visually map X12 -> XML/JSON. Implement `If-Exists` logic. |
| **Route** | Transport Layer | Handles HTTP/SFTP ingress/egress. Configured in Route properties. |
| **DataFlow** | Orchestration Layer | The pipeline inside the Route. Executes Maps, Groovy, REST lookups. |
| **Native Translator** | Engine | The ultra-fast core parser that translates X12 to internal XML. |
| **EAM** | Admin Console | Monitor JVM Memory, Threads, Server Health, Deploy Routes. |
| **TM** | Transaction Manager | UI to trace individual payload lifecycles and view split components. |

### Critical Workflows
- **Deploying Logic**: SpecBuilder `.ecs` profile ➡️ Loaded into Route Configuration ➡️ Deployed via EAM.
- **Triaging Failures**: Open TM ➡️ Search by Member ID/Claim ID ➡️ Identify which DataFlow component took 10+ seconds or threw the exception.
- **Handling API Timeouts**: Groovy `try/catch` inside DataFlow ➡️ Map to X12 `STC` ➡️ Pass to Native Translator.

### Mnemonics & Mental Models
- **SpecBuilder** = The Bouncer (SNIP Validation).
- **MapBuilder** = The Translator (Data shape shifting).

### Interview Triggers
- 🚨 **"Severe Route Latency / Hanging"** ➡️ Trigger: Thread starvation. Check EAM active threads. Check TM for slow Groovy I/O or external REST timeouts. Tune `server.xml` Native Translator thread pool.
- 🚨 **"Null Pointer Exception in Map"** ➡️ Trigger: A SNIP 2 rule was relaxed in SpecBuilder, allowing a missing optional segment to hit MapBuilder. Fix: Add `If-Exists` conditional logic in MapBuilder.
