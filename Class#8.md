# Class 8 - Retrieval Augmented Generation: Vector RAG + Receptionist

## Lesson Overview

This lesson adds a knowledge base to the receptionist agent (built in Class 7) using **Vector RAG**. The agent becomes able to instantly answer questions about the restaurant's menu, policies, hours, and location by searching through uploaded documents — transforming it from a booking-only bot into an intelligent assistant that can answer *any* question about the business.

## What is Vector RAG, in Depth?

Vector RAG is the practical implementation of the RAG concept covered in Class 3 (retrieve → rank → generate), specifically using **vector similarity search** as the retrieval mechanism.

The core problem it solves: an LLM's knowledge is frozen at training time and generic — it has no idea what's on *this specific restaurant's* menu, what *this business's* refund policy is, or what hours *this location* is open. Vector RAG solves this by letting the agent search a private set of documents at the moment of the query, and using what it finds to ground its answer in real, current, business-specific facts.

**Why "vector" search instead of normal keyword search?**

- Keyword search only matches exact words. If a customer asks "Do you have anything for someone who can't eat wheat?" but the menu document says "gluten-free options," a keyword search would miss it entirely — no shared words.
- Vector search matches by **meaning**, not exact wording. Because both phrases get converted into vectors that land close together in "meaning space," the system can find the gluten-free menu section even though no words match directly.
- This is what makes RAG "smart" — it retrieves based on semantic similarity, not brittle exact-match rules.

## Step-by-Step: How Vector RAG Actually Works

### 1. Preparing Documents

Source documents (menu PDFs, policy docs, FAQs) first need to be **chunked** — broken into smaller pieces (e.g., a paragraph or a menu section at a time) rather than embedding one giant document as a single block.

*Why chunking matters:* if an entire 10-page document were turned into a single vector, a search for "gluten-free options" would retrieve the *whole* document, most of which is irrelevant. Smaller chunks mean the retrieval step can pull back just the specific paragraph that actually answers the question, keeping the AI's context focused and accurate.

### 2. Creating Embeddings

Each chunk of text is passed through an **embedding model**, which converts it into a vector (a list of numbers, often hundreds or thousands of dimensions long). This vector is a mathematical fingerprint of the chunk's meaning.

Two chunks with similar meaning (e.g., "we close at 10pm" and "our closing time is 10:00 PM") will produce vectors that are mathematically close to each other, even though the wording differs completely.

### 3. Storing in a Vector Database

The embeddings are stored in a **vector database** — a database purpose-built for storing vectors and performing fast similarity search across potentially millions of them. Two options covered in this lesson:

- **Pinecone** — a managed, cloud-hosted vector database; simple to set up, handles scaling automatically, but is a paid/usage-based service.
- **Supabase** — an open-source backend platform that includes Postgres with a vector extension (`pgvector`); a good option for someone wanting more control or to stay within free tiers, since it can be self-hosted or used on Supabase's free plan.

### 4. Retrieval at Query Time

When a customer asks the agent a question:

1. The customer's question itself gets converted into an embedding (same process as step 2).
2. The vector database searches for the stored chunks whose vectors are **closest** (most similar in meaning) to the question's vector.
3. The top-matching chunks (e.g., top 3-5 results) are retrieved.

### 5. Generation

The retrieved chunks are inserted into the LLM's context alongside the original question (typically via the system prompt or a tool result), and the model generates a natural-language answer **grounded in that retrieved text** — rather than guessing or hallucinating an answer from generic training knowledge.

## Connecting Vector RAG to the Receptionist Agent (Class 7 tie-in)

The receptionist agent already has tools for taking *actions* (Google Sheets for bookings, Google Calendar for scheduling, Gmail for confirmations — from Class 7). Vector RAG adds a new kind of tool: a **knowledge retrieval tool**, which the agent can call whenever a question requires looking something up rather than performing an action.

This means the agent's system prompt now needs to help it decide **when to use which tool** — e.g.:

- "What are your hours?" → call the Vector RAG knowledge tool
- "Book me a table for 2 at 7pm" → call the Google Calendar / Sheets tools
- "Do you have gluten-free pasta?" → call the Vector RAG knowledge tool

This is the same tool-selection logic introduced in Class 6 (how agents decide when to call a tool), now extended to include a retrieval tool alongside action tools.

## Example Test Queries

- "Do you have gluten-free options?" → should retrieve the relevant menu section, not the whole menu
- "What are your hours?" → should retrieve the specific hours-of-operation chunk from the policy doc
- "Where are you located?" → should retrieve the location/address chunk

## Key Takeaway

Vector RAG turns static documents into a searchable, meaning-based knowledge layer for an agent. Combined with action tools (Sheets/Calendar/Gmail), the receptionist agent now covers both halves of what a real front-desk employee does: **answering questions accurately** and **taking real actions** — which is what makes it deployable as an actual production assistant rather than a demo.

---

*Part of the "AI Agents" course repository — Master AI Agents by Tech7Academy.*