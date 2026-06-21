# Edifecs Profiles (Validation)

**What it is**: A compiled set of validation rules (created in SpecBuilder) that dictate exactly what constitutes a "valid" file based on HIPAA and client business logic.

**Why it exists**: To protect backend systems. If a Payer's core adjudication system crashes when a Date of Birth is missing, the Edifecs Profile will catch that missing DOB at the front door and reject the file with a 999 or 277CA.

**When to use it**: Executed immediately upon receiving a file from an external trading partner to ensure SNIP Level 1-7 compliance before any mapping or routing occurs.

**Real Examples**: 
- *State of Colorado*: Tested and deployed custom Edifecs Profiles integrated with CAQH CORE validation services to ensure all inbound 837I files strictly adhered to state-specific institutional billing rules.

**Common Mistakes**:
- Deploying a Profile that is too strict for the real world, causing perfectly valid partner files to fail on obscure or optional SNIP 5 (code set) rules.
- Hardcoding validation rules in custom Groovy scripts instead of leveraging the Profile engine.

**Interview Questions**:
- *How do you ensure inbound claims meet CAQH CORE requirements?* (Answer: By compiling those business rules into a custom Edifecs Profile via SpecBuilder, ensuring the validation happens natively and rapidly before the payload enters the DataFlow.)
