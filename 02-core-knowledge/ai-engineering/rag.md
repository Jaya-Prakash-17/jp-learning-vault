# Retrieval-Augmented Generation (RAG)

## What is RAG?
Large Language Models only know what they were trained on (which stopped months ago) and they do not know your company's private data. 

**RAG** is the architectural pattern of giving the LLM an "open book" to read from. Before you send the user's question to the LLM, you query a private database, pull the relevant documents, paste them into the prompt, and say: *"Answer the user's question using ONLY the provided context."*

## Why RAG instead of Fine-Tuning?
- **Fine-Tuning**: Re-training the model's brain. Expensive, slow, and terrible for memorizing facts (the model will still hallucinate).
- **RAG**: Cheap, instant (just update your database), and highly accurate. If a user asks a question, you can provide the exact source document link because you retrieved it.

## The RAG Pipeline (How to build it)

### 1. Document Loading & Chunking
You cannot pass a 5,000-page Edifecs manual to an LLM on every question; it's too expensive and slow. You must parse the PDF and split it into "chunks" (e.g., 500-word paragraphs).

### 2. Embeddings
Computers don't understand words; they understand numbers. An Embedding Model translates a chunk of text into a massive array of numbers (a vector) representing the "meaning" of the text. 
- *Example*: The vectors for "Dog" and "Puppy" will be mathematically very close. The vector for "Carburetor" will be far away.

### 3. Vector Database
You store all these vectors in a Vector DB (like Pinecone, Chroma, or pgvector).

### 4. Semantic Search (Retrieval)
A user asks: *"How do I tune the Native Translator?"* 
You convert that question into a vector, ask the Vector DB to find the 3 closest matching chunks, and retrieve them.

### 5. Generation
You take those 3 chunks, shove them into a System Prompt, append the user's question, and send it to the LLM to generate the final human-readable answer.
