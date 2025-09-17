# 📄 BPG Workflow v3.3: AI Sales Proposal Generator

An advanced n8n workflow that automates the creation of personalized, data-driven sales proposals. It enriches initial customer data with external research and generates a comprehensive, 10-section proposal in HTML format.

## 🎯 The Problem

The sales team was spending hours manually researching potential clients and writing proposals from scratch. The process was inconsistent, and key information from different sources (CRM, industry knowledge, client website) was difficult to consolidate, leading to generic and less impactful proposals.

## ✨ The Solution

This n8n workflow acts as a centralized brain for proposal generation:
1.  It is triggered by a **Webhook** from a portal, receiving initial customer data (name, industry, problems, goals, etc.).
2.  It enriches this data by invoking two sub-workflows:
    *   **Challenge Analyzer:** Identifies common challenges for the client's specific industry.
    *   **Web Crawler:** If a client website is provided, it scrapes the site for supplementary information to further personalize the proposal.
3.  It loads a central **Knowledge Base** containing detailed information about Mirakam's products, modules, and services.
4.  It dynamically assembles a highly detailed, multi-part prompt for an LLM, combining all four sources of truth: customer data, industry challenges, website info, and the internal knowledge base.
5.  The LLM generates a complete 10-section proposal according to a strict HTML structure.
6.  The final HTML is sent back as the webhook response, ready to be displayed or saved.
7.  **(Bonus Feature)** The workflow includes robust error handling and logs every successful or failed execution to a Google Sheet for monitoring and analysis.

This automation ensures every proposal is deeply personalized, accurate, and generated in minutes instead of hours.

## 🗺️ Workflow Diagram

This diagram illustrates the execution flow of the BPMS Proposal Generator workflow.

![Workflow Diagram](images/Entire%20V3.3.png)

## 🛠️ Tech Stack
*   **Automation:** n8n (with sub-workflow execution)
*   **AI/LLM:** AvaCloud API (OpenAI Compatible)
*   **Data Enrichment:** n8n Webhook, HTTP Request (for web crawling)
*   **Data Handling:** JSON, HTML
*   **Logging:** Google Sheets API

## ⚙️ How It Works (Node by Node)
1.  **Webhook Node:** Receives initial customer data from a sales portal.
2.  **Execute Workflow (ChallengeAnalyzer):** Fetches generic industry challenges to provide broader context.
3.  **If Node:** Checks if a customer website URL was provided in the input data.
4.  **Execute Workflow (AiWebCrawler):** If a URL exists, this sub-workflow is called to scrape the site.
5.  **Set Node (Knowledge Base):** Loads the internal Mirakam product data as a JSON object.
6.  **Set Node (Build Prompt):** The core of the workflow. Assembles the master prompt from all available data sources.
7.  **HTTP Request (Send to AvalAi):** Sends the final prompt to the LLM and receives the generated HTML.
8.  **Respond to Webhook Node:** Returns the final HTML as a direct response to the initial request.
9.  **Google Sheets Nodes (Success/Failure Path):** Logs the outcome of every execution for tracking and debugging.

## 🚀 How to Use
1.  Download the `BPG-v3.3.json` file.
2.  **Important:** This workflow depends on two other sub-workflows (`AiWebCrawler` and `IndustryChallengeAnalyzer`). You must import and activate them in your n8n instance first.
3.  Import the main workflow into your n8n instance.
4.  Configure your credentials for the AvalAi API (in the HTTP Request node) and Google Sheets.
5.  Update the Webhook node with your path.
6.  Activate the workflow and send customer data to the Webhook URL.
