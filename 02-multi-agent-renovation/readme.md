# 🏡 Multi-Agent Kitchen Renovation App using Vertex AI ADK

This project demonstrates a sophisticated **multi-agent system** built with the Vertex AI Agent Development Kit (ADK). It automates a full kitchen renovation workflow using separate agents for proposal generation, permit checking, and material order status. All agents are coordinated by a root orchestrator.

---

## 🤖 What Is a Multi-Agent System?

A multi-agent system is a set of autonomous programs (agents), each with a focused responsibility, that work together to accomplish a larger goal. Careful planning is required to:

1. Determine the specialization and roles of each agent.
2. Design a root agent that routes and synthesizes results.
3. Choose a communication and state tracking strategy suitable for your agents.

---

## 📦 System Overview

The system includes:

* **RenovationProposalAgent** — Crafts a detailed kitchen renovation plan.
* **PermitsAndComplianceAgent** — Checks building code and permit requirements.
* **OrderStatusCheckAgent** *(Optional)* — Retrieves real-time status of material orders from a database.
* **RootAgent** — Orchestrates and aggregates results from the above agents based on user input.

---

## ⚙️ Setup Instructions

### 1. Set Up Google Cloud Project

1. Open the [Google Cloud Console](https://console.cloud.google.com/).
2. Ensure your project has an active billing account.
3. (Optional) Redeem Google Cloud credits if available.
4. Launch the integrated Cloud Shell from the Console.
5. Confirm Python 3.9+ is available in the shell.

---

### 2. Create and Activate Virtual Environment

```bash
cd ~/workspace
python -m venv .venv
source .venv/bin/activate
```

---

### 3. Install Vertex AI ADK

```bash
pip install google-adk
```

---

### 4. Create Project Directory and Files

```bash
mkdir renovation-agent
cd renovation-agent
touch __init__.py agent.py requirements.txt .env
```

Populate the files:

* `__init__.py`: *(Leave empty or use to import `agent.py`)*
* `agent.py`: Contains implementation of:

  * `RootAgent`
  * `RenovationProposalAgent`
  * `PermitsAndComplianceAgent`
  * `OrderStatusCheckAgent` *(optional)*
* `requirements.txt`:

  ```txt
  google-adk
  google-cloud-storage
  python-dotenv
  ```
* `.env`:

  ```env
  GOOGLE_CLOUD_PROJECT=your-project-id
  GOOGLE_CLOUD_LOCATION=us-central1
  STORAGE_BUCKET=next-demo-store
  CHECK_ORDER_STATUS_ENDPOINT=https://<your-cloud-run-url>
  ```

---

### 5. (Optional) Setup Order Status Agent

If you're including the **OrderStatusCheckAgent**, follow these steps:

1. **Create AlloyDB**:

   * Set up a cluster.
   * Create a table: `material_order_status` with relevant sample data.

2. **Develop Cloud Run Service**:

   * Use Java to connect to AlloyDB.
   * Expose a REST endpoint: `/check-order-status`
   * Ensure proper configuration for AlloyDB connectivity.

3. **Deploy** the service to Cloud Run and obtain the public endpoint URL.

---

### 6. Create Google Cloud Storage Bucket

```bash
gsutil mb -l us-central1 gs://next-demo-store
gsutil iam ch allUsers:objectViewer gs://next-demo-store
```

> 🔐 **Important:** This setup is meant for demonstration. Do **not** expose your bucket to the public in production environments.

---

### 7. Run the Agent System

Start the ADK runtime:

```bash
adk run .
```

Launch the web UI interface:

```bash
adk web
```

Then try queries like:

```text
Generate a renovation proposal, verify permits, and check order status for cabinets and flooring.
```

---

## 🧠 How It Works

1. **RootAgent** receives the user request.
2. **RenovationProposalAgent** uses Gemini to create the renovation plan.
3. **PermitsAndComplianceAgent** checks regulatory constraints.
4. **OrderStatusCheckAgent** (if used) fetches data from Cloud Run and AlloyDB.
5. **RootAgent** compiles and saves the final results as a **PDF** in **Cloud Storage**.

---

✅ **Completed!**

You’ve built a fully functioning multi-agent renovation assistant using ADK, with modular reasoning and real-time data integration.

Feel free to experiment, improve the agents, or package this for deployment!
