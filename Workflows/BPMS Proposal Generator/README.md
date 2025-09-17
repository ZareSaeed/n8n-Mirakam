# 📄 BPMS Proposal Generator

This project contains a series of n8n workflows designed to automate the creation of detailed, personalized, and data-driven sales proposals for the ICAN BPMS product suite.

## 🎯 The Problem
Manually creating comprehensive sales proposals is a time-intensive process. It requires gathering client-specific information, researching their industry, referencing internal product documentation, and formatting it all into a consistent, professional document. This manual approach is slow, prone to inconsistency, and doesn't scale well.

## ✨ The Solution
This workflow automates the entire proposal generation process. It acts as a central engine that consolidates multiple data sources—client requirements, web research, internal knowledge bases—and uses a Large Language Model (LLM) to generate a complete, multi-section proposal in HTML format.

The core logic ensures that every proposal is not only generated quickly but is also highly tailored to the prospective client's unique needs and industry context.

---

## 📂 Available Versions

This project has evolved over time. Each version represents a significant improvement in functionality or approach. The latest recommended version is **v3.3**.

*   **[v3.3](./v3.3/)** - **Latest Version:** The most advanced version, utilizing a new, structured product knowledge base for highly accurate and consistent content generation.
*   *(Older versions like v3.2, v3.1, and v2 can be linked here as they are added to the repository.)*

---

## 🧩 Helper Sub-Workflows

The main proposal generator relies on helper sub-workflows for specific data enrichment tasks. These helpers must be imported and activated in your n8n instance for the main workflow to function correctly.

*   **[AiWebCrawler](./Helpers%20(Sub-Workflows)/AiWebCrawler/)**: Scrapes a client's website to extract relevant information (like mission, services, and team) for deep personalization.
*   **[Industry Challenges Analyzer](./Helpers%20(Sub-Workflows)/Industry%20Challenges%20Analyzer/)**: Provides context on common challenges and pain points within a client's specific industry.

## 🛠️ Core Technology
*   **Automation:** n8n (with sub-workflow execution)
*   **AI/LLM:** AvaCloud API (OpenAI Compatible)
*   **Data Format:** JSON, HTML
*   **Data Enrichment:** Web Scraping, Google Sheets
