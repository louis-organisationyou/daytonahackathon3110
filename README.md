DriveGraph Auditor — Personal Drive to Enterprise Workspace Migration Audit

🛑 The Problem

When businesses scale and attempt to migrate from legacy, consumer @gmail.com Google Drives to proper Google Workspace environments, they hit a critical wall: files owned by external contractors or personal accounts cannot have their ownership transferred. The migration fails in bulk, leaving IT blind to what files are "stuck" and who actually owns them.

🚀 What This Demo Does (Live Capabilities)

Crawls: Reads a target Google Drive folder and extracts file metadata and ownership permissions.

Maps: Writes File, User, and Folder nodes, along with OWNS and LOCATED_IN edges, to Neo4j Aura.

Audits: Executes a precise Cypher graph query to instantly report files owned outside the core company domain, highlighting critical migration blockers.

🧠 Architecture & Sponsor Integrations

This project heavily leverages the Hackathon sponsor stack to solve a real-world enterprise problem:

Daytona (Secure Execution): The Drive API crawl involves highly sensitive OAuth tokens and company data. By orchestrating the crawl inside an ephemeral Daytona Sandbox, we guarantee that user tokens and file structures never persist on vulnerable infrastructure. (sandbox_runner.py included).

Nosana (Decentralized AI Inference): To categorize thousands of files, we batch file text to the Nosana GPU Network using their OpenAI-compatible endpoint. This provides low-cost, parallel LLM summarization without hitting centralized API rate limits. (summarize.py included).

Neo4j (Knowledge Graph): Relational SQL databases require nightmare joins to untangle nested Drive permissions. By utilizing Neo4j Aura, we model the Drive as a graph. A single Cypher query traverses the ownership web to find external dependencies instantly.

📂 Evidence & Artifacts

Please check the /evidence folder in this repository for execution proof:

neo4j_graph_screenshot.png — Visual representation of the ownership graph in Neo4j Workspace.

audit_report.md — The raw output of the Cypher query identifying external owners.

💻 How to Reproduce

Provision a free Neo4j AuraDB instance.

Copy .env.example to .env and add your NEO4J_URI, NEO4J_USERNAME, and NEO4J_PASSWORD.

Set up your Daytona CLI and execute python sandbox_runner.py to spawn the secure environment.

Run the Cypher query located in audit.cypher to generate the migration report.

🗺️ Roadmap

v2: Connect live summarize.py outputs to write (:Topic) nodes back to Neo4j.

v3: Daytona-scheduled full-Drive crawls + automated Google Drive file duplication to bypass ownership locks.

***
demo displayed only on end user PC.
