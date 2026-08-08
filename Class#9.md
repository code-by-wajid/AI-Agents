# Class 9 - Retrieval Augmented Generation: Building an AI Tutor using SQL + SERP RAG

## Lesson Overview

This lesson builds a completely new agent — an **AI tutor for SAT prep** — combining two additional RAG types beyond the Vector RAG covered in Class 8: **SERP RAG** (for live web search) and **SQL RAG** (for structured question databases). The result is an agent that can answer study questions, search for resources online, and pull practice questions from a structured database, all within a single agent.

## The Different Types of RAG, Explained

RAG isn't one single technique — it's a family of approaches, each suited to a different kind of data source. This class covers the main types:

1. **Semantic RAG (Vector RAG)** — covered in Class 8. Retrieves based on *meaning similarity* using embeddings and a vector database (Pinecone/Supabase). Best for unstructured text like menus, policy docs, and FAQs, where the exact wording of a query won't match the source text.
2. **SQL RAG (also called ID-based RAG)** — retrieves data from a **structured database** (like a spreadsheet or SQL table) using precise, structured queries rather than meaning-based search. Instead of asking "what text is semantically similar to this question," it asks "give me rows where column X = Y" — e.g., "give me all SAT math questions tagged 'algebra' and 'medium difficulty.'"
  - Works well when the data is already organized into clear fields/columns (like a question bank with columns for subject, difficulty, question text, answer).
  - More precise and predictable than semantic search when the data has that clean structure — no risk of retrieving something "close in meaning" but factually wrong.
3. **SERP RAG** (SERP = Search Engine Results Page) — retrieves information by performing a **live web search** and pulling in real-time results, rather than searching a pre-loaded private document set. Used when the answer isn't something the business already has documented — e.g., "explain this SAT grammar rule" or "find me practice resources for the essay section," where the best answer might exist somewhere on the open web, not in an internal database.

**Structured vs. Unstructured data — why it matters for choosing RAG type:**

- **Structured data** (spreadsheets, SQL tables, clearly labeled fields) → SQL RAG is the natural fit, since the data is already organized for precise querying.
- **Unstructured data** (PDFs, free-form policy docs, paragraphs of text) → Vector/Semantic RAG is the natural fit, since there's no clean field structure to query directly — meaning-based search is needed instead.
- **Live/external information not owned by the business at all** → SERP RAG is the natural fit, pulling from the web in real time.

## Combining Multiple RAG Types in One Agent

The key lesson here: a single agent isn't limited to one retrieval method. The AI tutor agent uses **both** SQL RAG and SERP RAG side by side, with the agent's system prompt guiding *which* retrieval tool to call depending on the type of question:

- A question about a specific practice problem from the question bank → SQL RAG (structured lookup in Google Sheets)
- A question asking for an explanation, tip, or outside resource → SERP RAG (live web search)

This is the same tool-selection pattern from Class 6/8 (deciding *when* to call *which* tool), extended further to include a live web-search tool alongside database and knowledge-base tools.

## External Nodes for Web Search

To give the agent the ability to search the web, an **external search node** is added to the n8n workflow and connected to the AI Agent as a tool (similar to how Gmail/Calendar/Sheets tools were connected in Class 7). This node performs the actual SERP lookup — sending the query out to a search engine and returning results the agent can read and use to generate its answer, rather than the agent relying purely on its frozen training knowledge.

## Structuring the Question Database (Google Sheets)

For SQL RAG to work well, the question bank needs clean, consistent columns — for example: subject, topic, difficulty level, question text, correct answer, explanation. This structure is what allows the agent to run precise, filtered queries (e.g., "medium-difficulty algebra questions") instead of guessing from unstructured text.

## Key Takeaway

Different data needs different retrieval strategies — there's no single "best" RAG type. The real skill is recognizing which type of data a question is asking about (structured database, unstructured document, or live web) and routing the agent to the right retrieval tool accordingly. Combining multiple RAG types in one agent (as with this AI tutor) is what allows a single agent to competently handle a much wider range of questions than any one retrieval method could alone.

---

*Part of the "AI Agents" course repository — Master AI Agents by Tech7Academy.*