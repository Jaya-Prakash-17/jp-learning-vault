# AI Engineering Interview Questions

*(For a Software/Integration Engineer, not an ML Scientist)*

**Q: "What is the difference between RAG and Fine-Tuning?"**
*Answer*: Fine-tuning requires retraining the model's weights to teach it a new style or format; it is expensive and bad for factual recall. RAG (Retrieval-Augmented Generation) uses a Vector Database to search for relevant private documents at runtime, injecting them directly into the prompt. RAG is cheaper, prevents hallucinations, and allows you to trace the answer back to a source document.

**Q: "What makes an AI system 'Agentic'?"**
*Answer*: An LLM is just a text generator. A system becomes "Agentic" when it is given an objective, a loop to reason (like the ReAct pattern), and access to executable Tools (like a bash terminal or a REST API). Instead of just outputting text, an Agent autonomously takes actions, observes the results of those actions, and adjusts its plan until the objective is met.

**Q: "How would you give an LLM access to our proprietary patient database safely?"**
*Answer*: I would not give the LLM direct SQL access, as that invites SQL injection and hallucinations. Instead, I would build an API (or an MCP Server) that exposes highly constrained, read-only tools (e.g., `get_patient_status(member_id)`). I would provide the LLM with the JSON schema of that specific tool. The LLM decides *when* to call the tool and with what parameters, but the deterministic API layer actually executes the query safely.

**Q: "What is the Context Window, and why does it matter?"**
*Answer*: The context window is the maximum number of tokens (words/pieces of words) the model can hold in its working memory for a single prompt. If I try to paste a 10,000-page Edifecs manual into a model with a 4K context window, it will fail or forget the beginning. Managing context windows via chunking and RAG is the primary challenge in AI engineering.

**Q: "If an AI Agent is writing code for our enterprise system, how do you ensure it follows our specific coding standards?"**
*Answer*: I would implement a `skills.md` or `.cursorrules` file at the root of the repository. This file serves as the system prompt for the agent, explicitly defining the persona, forbidden libraries, architectural patterns, and providing "golden" code snippets. Furthermore, I would force the agent to run the automated unit test suite before it is allowed to commit any code.
