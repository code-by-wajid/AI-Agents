# Class 10 - Build a Stock Analyzer Agent with n8n

## Lesson Overview

This lesson covers designing and automating a **stock analyzer agent** using n8n — connecting financial data sources, processing and filtering stock market information, and building automated workflows that analyze trends. The end goal: an agent that can fetch stock data, run basic analysis, and deliver actionable insights with no manual effort.

## What I Learned

- Setting up n8n for financial data workflows
- Integrating stock APIs for real-time market data
- Automating analysis with conditional logic and data transformation
- Sending alerts, reports, or summaries to preferred channels (e.g. email, Slack)
- **Sub-workflows** — how to build one n8n workflow that calls *another* n8n workflow as a reusable step

## Sub-Workflows, in Depth

A **sub-workflow** is a separate, self-contained n8n workflow that gets triggered/called *from within* another workflow — similar to how a function works in programming: you write the logic once, then call it wherever it's needed instead of duplicating it.

**Why sub-workflows matter for an agent like this:**

- **Reusability** — e.g., a "fetch stock data from API" step could be its own sub-workflow, then reused by multiple different parent workflows (a daily report workflow, an on-demand chat query, an alert-triggered workflow) without rebuilding the API call logic each time.
- **Cleaner main workflow** — instead of one giant workflow with dozens of nodes handling API calls, data transformation, and conditional logic all in one canvas, the main workflow can stay simple and readable by delegating specific jobs to sub-workflows.
- **Easier debugging** — if something breaks, it's easier to isolate which sub-workflow (e.g., "data fetch" vs. "analysis" vs. "alert sending") is failing, rather than untangling one massive workflow.
- **Matches real agent design** — this is the same principle behind giving an AI agent multiple distinct tools (like the receptionist agent's separate Sheets/Calendar/Gmail tools) rather than one do-everything tool: modular pieces are easier to build, test, and maintain than one monolithic block.

**How it fits the Stock Analyzer:** the overall agent likely breaks down into separate concerns — fetching real-time market data via a stock API, running the analysis/conditional logic on that data, and formatting + sending the resulting report or alert. Structuring each of these as its own sub-workflow means each piece can be tested independently before being chained together into the full pipeline.

## Key Takeaway

Sub-workflows bring standard software engineering practice (modularity, separation of concerns, reusability) into no-code automation. As workflows grow more complex — like a full stock analysis pipeline with data fetching, conditional logic, and multi-channel alerts — breaking them into sub-workflows keeps the system maintainable instead of becoming an unreadable tangle of nodes.

---

*Part of the "AI Agents" course repository — Master AI Agents by Tech7Academy.*