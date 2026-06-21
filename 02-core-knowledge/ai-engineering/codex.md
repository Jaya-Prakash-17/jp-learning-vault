# Code Generation Models (Codex / Copilot)

## The Evolution of AI Coding
There are three distinct tiers of AI-assisted coding tools today:

### Tier 1: Autocomplete (e.g., GitHub Copilot, OpenAI Codex)
- **How it works**: As you type, the model reads the file you currently have open and predicts the next 5-10 lines of code. 
- **Use Case**: Eliminating boilerplate. Writing standard loops, getters/setters, or simple regex logic. It does not understand your overall system architecture; it only understands the immediate context.

### Tier 2: Chat & Instruct (e.g., Cursor Chat, ChatGPT)
- **How it works**: A sidebar in your IDE. You highlight a block of code and say, *"Optimize this Groovy script."* The model rewrites it, and you manually click "Accept."
- **Use Case**: Refactoring, explaining legacy code, or generating unit tests for a specific function.

### Tier 3: Agentic Coding (e.g., Devin, Claude Code, Antigravity)
- **How it works**: You give a high-level prompt: *"Migrate this HTTP integration route to use OAuth2."* The Agent explores the codebase, edits 5 different files across 3 directories, installs new dependencies, and runs the build script.
- **Use Case**: Feature development, complex refactoring, and codebase-wide updates.

## Best Practices for Code Generation
- **Never trust the hallucination**: AI models will invent libraries that don't exist. Always verify the imports.
- **Context is King**: If you want the AI to write a good Edifecs MapBuilder script, you must paste in an example of a *good* script first. Zero-shot generation in niche proprietary languages (like Edifecs specific Groovy bindings) often fails without examples.
