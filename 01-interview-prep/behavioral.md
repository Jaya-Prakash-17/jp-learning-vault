# Behavioral & Situational

## 1. The Need (Business Purpose)
- **The Need**: Toxic rockstars destroy teams. Companies use behavioral interviews to ensure a candidate has the emotional intelligence to handle disagreements, receive feedback, and collaborate under pressure without ego.

## 2. Core Concepts
- **Ego-less Engineering**: The code is not you. When someone critiques your code, they are not critiquing you.
- **Empirical Decision Making**: Resolving architectural disputes with data, prototypes, and benchmarking, rather than opinions and hierarchy.
- **"Disagree and Commit"**: The ability to voice strong objections, but fully support and execute the final decision once leadership makes a call.

## 3. Basic Daily Workflows
- **Peer Code Reviews**: Giving constructive, polite feedback on PRs. Receiving feedback graciously.
- **Sprint Planning**: Negotiating story points and admitting when a task is more complex than originally estimated.

## 4. Advanced Scenarios
- **Pushing Back**: Respectfully telling a Senior Architect or Product Manager that their proposed solution is dangerous or creates technical debt.
- **Blameless Post-Mortems**: Handling a production outage by focusing on fixing the system architecture, not blaming the engineer who wrote the bug.

---

## Interview Question Deep Dive

### Q: "Tell me about a time you strongly disagreed with a senior engineer's architectural decision."

**30-Second Answer**: On the Humana project, I disagreed with a senior engineer's proposal to write a massive custom Groovy script to handle X12-to-JSON mapping. I advocated for using MapBuilder instead for better maintainability. I built a quick prototype to prove MapBuilder was faster and caught SNIP errors natively.

**2-Minute Answer**: 
- **Situation**: We were tasked with transforming the inbound 276 payload into a complex JSON schema for the CORE APIs. A senior engineer wanted to write a highly customized Groovy script to parse the XML DOM and build the JSON manually because he felt MapBuilder was too rigid.
- **Task**: I needed to ensure the solution was maintainable long-term, and a 1,000-line Groovy script would become technical debt. 
- **Action**: I didn't just argue. I spent a few hours building a functional prototype in MapBuilder. I demonstrated how the visual mapping handled conditional X12 segment looping natively, and more importantly, how it automatically threw standardized errors if the data types didn't match—something the Groovy script would require hundreds of extra lines to handle gracefully.
- **Result**: We reviewed the prototype together. He acknowledged the reduced technical debt, and we went with the MapBuilder approach. However, I learned a lot from his edge-case logic, which we incorporated into the MapBuilder rules.

**Deep Dive Answer / The Lesson**: Disagreements shouldn't be philosophical; they should be empirical. Show, don't tell. By building the prototype, I removed ego from the equation and made it a discussion about code maintainability.

**Follow-up Questions**:
- *Interviewer*: "What would you have done if the senior engineer still said no?" (Answer: I would have respectfully documented my concerns about technical debt, committed fully to his architectural decision, and helped write the best Groovy script possible. "Disagree and commit.")
