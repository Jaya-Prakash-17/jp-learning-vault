# AI-Assisted Development & Skills Files

## The Philosophy
AI-assisted development does not replace software engineers. It replaces the mechanical act of typing syntax. The engineer's job shifts entirely to **System Architecture, Prompt Engineering, and Code Review**. 

To get good code out of an AI Agent, you must constrain its behavior using Skills and Instructions.

## What is a `skills.md` file?
When an Agent (like Claude Code or an IDE-integrated AI) opens your repository, it is blind. It doesn't know your team's coding standards. A `skills.md` (or `.cursorrules` / `instructions.md`) file is a declarative manifesto you place in the root of your project to teach the Agent *how* to code in your specific environment.

### How to Build a Powerful Skills File
A great skills file should define:
1. **The Persona**: *"You are an expert Healthcare Integration Engineer strictly adhering to CAQH CORE standards."*
2. **The Tech Stack**: *"This project uses Groovy 3.0, Java 11, and Edifecs API conventions."*
3. **Forbidden Actions**: *"NEVER use the `rm` command. NEVER hardcode IP addresses. Do not use generic Python libraries for X12 parsing."*
4. **Architectural Patterns**: *"If an API times out, you MUST catch the exception and map it to an STC segment. Do not return a 500 stack trace."*
5. **Code Examples**: Provide a perfect 10-line snippet of how your team handles database connections so the AI can mimic your exact style.

## Managing AI Agents
- **Give them plans, not tasks**: If a task is complex, force the agent into "Planning Mode". Make it write an `implementation_plan.md` first. Review the plan as an engineer, approve it, and *then* let the agent write the code.
- **Test-Driven AI**: The best way to manage an agent is to write the failing Unit Tests yourself. Then, tell the agent: *"Write the code to make these tests pass."* This guarantees the agent's output is functionally correct.
