# Lessons Learned

**What I will carry forward (The "Forget in 6 Months" log)**

- **Thread Tuning is Critical**: In high-volume systems (200K+ daily), poor thread management in the Native Translator or SOAP pools will crash the system under load, regardless of how clean the mapping logic is.
- **Error Handling is a Feature, not an Afterthought**: Building the X12 STC error framework reinforced that graceful degradation (returning a valid 277 error) is just as important as processing the happy path.
- **Script Consolidation**: Scattered Groovy scripts create massive I/O and execution overhead in Edifecs. Consolidating them is a primary lever for rapid performance optimization.
- **Client Communication**: Daily discussions and demonstrations were key to securing formal written appreciation for the Phase-1 go-live. Technical execution must be paired with visible, consistent client communication.
