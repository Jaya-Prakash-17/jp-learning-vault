# Large Language Models (LLMs)

## What is an LLM?
At its core, an LLM is a highly advanced autocomplete engine. It is not a database of facts, and it does not "think" or "search the internet" natively. It takes a sequence of text (a prompt) and predicts the most mathematically probable next word (token) based on the massive dataset it was trained on. 

As a software engineer, you interact with LLMs not by training them, but by orchestrating them via APIs.

## Core Concepts (Developer Perspective)

### 1. Tokens
LLMs don't read words; they read tokens. A token is roughly 3/4 of a word. API pricing and limits are strictly based on token counts. If you feed a 10,000-line XML payload into an LLM, you are charged for the tokens, and it eats into your Context Window.

### 2. Context Window
The "short-term memory" of the model for a single conversation. If a model has a 128K token context window, you can paste roughly a 300-page book into the prompt, and it can analyze the whole thing at once. Once you exceed the context window, the model "forgets" the beginning of the conversation.

### 3. System Prompts
The hidden instructions given to the model before the user ever interacts with it. 
*Example*: `"You are an expert EDI Integration Engineer. Never use Markdown formatting, only output raw JSON. Always validate SNIP Level 2 before answering."*

### 4. Hallucinations
Because LLMs are prediction engines, if they don't know the answer, they will mathematically guess the most plausible-sounding answer. This is why you **never** trust an LLM to write production mapping logic without a deterministic test suite backing it up.

## The Shift: Generative vs. Deterministic
- **Deterministic (Edifecs Native Translator)**: Given file A, you will get output B, 100% of the time, in 5 milliseconds.
- **Generative (LLM)**: Given prompt A, you might get output B, or output B', in 5 seconds. 

You do not replace deterministic integration engines with LLMs. You use LLMs to *wrap* the deterministic engine (e.g., having an LLM read an unstructured email from a trading partner, extract the `Sender ID`, and pass it to your deterministic Edifecs route).
