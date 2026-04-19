*n8n AI-Powered QA Agent & Knowledge Base*
This project implements a complete agentic automation system. It allows users to submit information via a web form into a private knowledge base, which a custom AI Agent then uses to provide grounded, accurate answers to user queries without "hallucinating."

🏗 System Architecture
The project consists of two distinct n8n workflows:

1. The Ingest Workflow (Data Collection)

Trigger: Captures data via the n8n Form Submission node.

Logic: Uses If nodes and Edit Fields to validate email domains (e.g., checking for n8n.io) and flag entries as "Trusted."

AI Enhancement: Employs a Basic LLM Chain with a system prompt to automatically analyze submissions and generate relevant tags/keywords.

Storage: Saves the cleaned, enriched data into an n8n Data Table.

2. The Agent Workflow (Chat Experience)

Trigger: An On Chat Message trigger provides an interactive interface.

Brain: An AI Agent node powered by OpenAI (GPT-4o/GPT-4o-mini).

Memory: Uses Simple Memory to keep track of the conversation context across multiple messages (Stateless to Stateful transition).

Tools: Includes a custom Data Table Tool that allows the agent to search the Q&A database using specific queries or tags generated during the conversation.

🛠 Tech Stack
Automation: n8n (v2.73+)

LLM: OpenAI (via n8n nodes)

Database: n8n Native Data Tables

Interface: n8n Chat Hub

🚀 Key Features
Grounded Answers: The agent is instructed via a System Message to only use the provided database tools, reducing the risk of false information.

Fuzzy Search: The AI can interpret messy human input and map it to relevant database entries using tags.

Production Ready: Includes versioning (V1, V2) and execution logging for easy troubleshooting.

🔧 Setup & Configuration
Ingest Setup:

Create a Data Table named Q&A with columns: Name, Email, Question, Answer, Tags, and isTrusted (Boolean).

Set up the Form Trigger and map the fields to the Data Table Insert node.

Agent Setup:

Connect the AI Agent node to an OpenAI Chat Model.

Configure the Data Table Tool with a specific description so the AI knows when to search for answers.

Enable the Chat Hub toggle in the Chat Trigger to make the agent accessible.

🧠 Lessons Learned
Reference Nodes: Using a "No-Op" node as a reference point to simplify data mapping from branched paths.

Prompt Engineering: Designing system messages to define the agent's role and behavior constraints.

Tool Parameters: Using the "Magic" button to allow the AI to dynamically set search terms for the database.
