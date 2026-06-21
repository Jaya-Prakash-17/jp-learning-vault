# AI Agents & Agentic Workflows

## What is an Agent?
An LLM by itself is just a chat interface—it can only talk. An **Agent** is a system where the LLM is given **Tools** (functions it can execute) and a loop to **Reason** about its environment. 
Instead of just giving you the code to fix a bug, an Agent can read your codebase, write the fix, run the unit tests, see that the tests failed, rewrite the code, run the tests again, and push a PR.

## Terminology Clarified

### 1. AI Agent
A discrete, autonomous software entity. It uses an LLM as its "brain." It has an objective, memory, and access to tools (like a Bash terminal, file reader, or web browser). 

### 2. Agentic AI / Agentic Workflows
"Agentic" is an adjective. It refers to a spectrum of autonomy. 
A simple script that calls an LLM is not agentic. 
A system that asks the LLM to create a 5-step plan, executes step 1, reflects on the output, and adjusts step 2 is an **Agentic Workflow**. You don't necessarily need a monolithic "Agent" framework to build agentic software; you just need loops, reflection, and tool calling.

### 3. Multi-Agent Systems
Instead of one massive Agent trying to do everything, you build specialized agents. E.g., a "Coder Agent" writes the Groovy script, and a "Reviewer Agent" analyzes it for memory leaks. They debate each other until the code is perfect.

## How to Build an Agent (The ReAct Pattern)
The most common agentic loop is **ReAct** (Reason + Act).
1. **Thought**: The LLM analyzes the user prompt. *"The user wants to know the size of server.log. I need to run a bash command."*
2. **Action**: The LLM outputs a structured JSON command calling the `execute_bash` tool with the argument `ls -lh server.log`.
3. **Observation**: The system actually runs the bash command and feeds the terminal output back to the LLM.
4. **Thought**: *"The file is 5GB. I should tell the user."*
5. **Final Answer**: *"Your log file is 5GB."*

You build this using frameworks like **LangChain**, **LlamaIndex**, or lightweight custom Python loops that handle the routing of JSON tool calls.
