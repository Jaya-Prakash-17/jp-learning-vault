# Claude Code & CLI Agents

## What is Claude Code?
Claude Code is an agentic command-line interface (CLI) tool. Unlike web-based chat interfaces (where you copy/paste code back and forth), Claude Code lives directly in your terminal, inside your project directory.

## How it Works
When you type `claude` in your terminal, you are launching an **Agent**. 
It has native tools attached to it:
- **File System Access**: It can use `grep` and `cat` to read your codebase.
- **Code Editing**: It can run commands to create, modify, and delete files.
- **Command Execution**: It can run `npm test` or `mvn clean install` to see if the code it just wrote actually compiles.

## The Agentic Workflow
If you ask Claude Code: *"Fix the null pointer exception in the DataFlow mapper."*
1. It will search your directory for `Mapper.java` or `Mapper.groovy`.
2. It will read the file.
3. It will write the fix.
4. It will run your test suite.
5. If the test fails, it will read the stack trace, realize its mistake, and rewrite the code automatically before finally reporting back to you.

## Why this is a paradigm shift
It moves the developer from being a **Code Writer** to being a **Code Reviewer and Orchestrator**. You provide the high-level architecture and business rules, and the Agent handles the syntax, boilerplate, and repetitive testing loops.
