# AI Engineering Overview

## Definition
AI Engineering is the discipline of building robust, scalable software systems that leverage Large Language Models (LLMs) and Machine Learning to automate reasoning, categorization, and generation tasks.

## Why it exists
Traditional software engineering relies on deterministic rules (`if X then Y`). This fails when dealing with unstructured data (like doctor's clinical notes, emails, or free-text claim appeals). AI Engineering introduces probabilistic models into the software stack, allowing systems to "understand" and process unstructured human data at scale.

## Commands (Python / LangChain)
- `pip install langchain openai chromadb`: Standard stack installation.
- `response = llm.invoke("Summarize this text")`: Basic LLM call.
- `vector_store.similarity_search("HIPAA rules")`: Querying a vector database for relevant context.

## Architecture
- **Large Language Models (LLMs)**: The brain (e.g., GPT-4, Claude). They predict the next word based on vast training data.
- **RAG (Retrieval-Augmented Generation)**: Since LLMs hallucinate and don't know private company data, RAG connects them to a database. You retrieve private data first, hand it to the LLM, and say "Answer the question using *only* this data."
- **Vector Databases**: Databases (like Pinecone or Chroma) that store text as arrays of numbers (Embeddings). They allow for "semantic search" (finding concepts that mean the same thing, even if the keywords differ).
- **Agents**: LLMs equipped with "tools" (like a calculator, web browser, or SQL executor). The LLM is prompted to reason about a task and autonomously decide which tools to execute to solve it.

## Interview Questions
**Q: "What is the difference between Fine-Tuning an LLM and using RAG?"**
*Answer*: Fine-Tuning changes the actual "brain" of the model by training it on new examples; it is expensive, slow, and bad for storing factual knowledge. RAG (Retrieval-Augmented Generation) leaves the model alone but gives it an open book to read from during the prompt. RAG is cheaper, allows for real-time updates (just update the database), and prevents hallucinations because you can cite the retrieved source document.

**Q: "How would you use an LLM in a Healthcare EDI pipeline?"**
*Answer*: I would not use an LLM to parse X12 syntax—deterministic engines like Edifecs Native Translator are infinitely faster and 100% accurate. However, I *would* use an LLM Agent to handle EDI rejections. If an 837 claim denies with a vague clinical error, an Agent could read the denial, retrieve the patient's unstructured clinical notes via a FHIR API, and automatically draft the narrative for an Appeal letter.

## Cheat Sheet (The RAG Pipeline)
1. **Document Loading**: Ingesting PDFs, Confluence pages, or text.
2. **Chunking**: Splitting massive documents into small 500-word paragraphs.
3. **Embedding**: Converting those text chunks into mathematical vectors using an embedding model.
4. **Storage**: Saving the vectors in a Vector Database.
5. **Retrieval**: When a user asks a question, embedding the question and finding the closest matching chunks in the database.
6. **Generation**: Injecting the retrieved chunks into the prompt and asking the LLM to generate the final answer.
