# 🤖 Knowelege Base Agent: Knowledge Base (KB) Editor v1 (WIP)

An n8n workflow that functions as an intelligent agent, allowing authorized users to update a central JSON knowledge base using simple, natural language commands.

## 🎯 The Problem

Our company's core product and service information is stored in a structured JSON file. Updating this file manually is:
*   **Slow:** Requires finding the file, understanding its structure, and carefully making edits.
*   **Error-Prone:** A single missing comma or bracket can invalidate the entire file, breaking other systems that rely on it.
*   **A Technical Bottleneck:** Non-technical staff (like sales) cannot make updates themselves, creating a dependency on the technical team for minor changes.

## ✨ The Solution

This n8n agent automates and simplifies the update process entirely:
1.  It receives a user command (e.g., "Add 'PDF export' as a feature for the Report Generator module") via a simple Webhook.
2.  It reads the latest version of the `knowledge_base.json` file.
3.  It securely sends the file's content and the user's command to an LLM.
4.  The LLM intelligently performs the requested edit and returns the full, updated JSON.
5.  The agent validates the returned data to ensure it's a valid JSON structure.
6.  It archives the new version with a timestamp (`knowledge_base_YYYY-MM-DDTHH-mm-ss.json`) and updates the main `knowledge_base_latest.json`.
7.  It records the change in a `changelog.csv` file for auditing purposes.

This solution empowers non-technical users to manage the knowledge base, drastically reduces the risk of human error, and creates a full version history of all changes.

---

## 🗺️ Workflow Diagram

This diagram illustrates the execution flow of the KB Editor Agent workflow.

![Workflow Diagram](images/KBA%20v1.png)

---

## 🛠️ Tech Stack
*   **Automation:** n8n
*   **AI/LLM:** AvaCloud API (OpenAI Compatible)
*   **Data Handling:** JSON
*   **Core Logic:** JavaScript (n8n Code & Set Nodes)
*   **Versioning/Logging:** n8n File I/O Nodes

---

## ⚙️ How It Works (Node by Node)
1.  **Webhook Node:** Receives the user command (e.g., `{ "command": "Update...", "user": "asghar" }`).
2.  **Read Binary File (latest):** Reads the `knowledge_base_latest.json` to get the current context.
3.  **Basic LLM Chain:** Sends the context and command to the LLM for editing.
4.  **Code Node:** Cleans and validates the LLM's output, ensuring it is a perfect JSON object.
5.  **Set Node:** Prepares dynamic variables like the timestamped filename and the log entry string.
6.  **Write Binary File (Version):** Saves the new JSON to the `/versions` folder with a timestamp.
7.  **File Operation (Copy):** Copies the new version to overwrite `knowledge_base_latest.json` in the `/live` folder.
8.  **Append to File (Log):** Adds a new line to `changelog.csv` detailing the change.

---

## 🚀 How to Use
1.  Download the `workflow.json` file.
2.  Import it into your n8n instance.
3.  **Crucially, create the necessary folder structure on your n8n server:** `/files/live/`, `/files/versions/`.
4.  Place your initial `knowledge_base_latest.json` and an empty `changelog.csv` into the `/files/live/` directory.
5.  Configure your LLM credentials in the "OpenAI Chat Model" node.
6.  Activate the workflow and use the Webhook URL to send commands.
