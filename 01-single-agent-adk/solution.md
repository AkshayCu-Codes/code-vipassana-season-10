# ✅ Solution: Single-Agent Kitchen Renovation Agent with ADK

This document outlines the step-by-step solution implemented to build a kitchen renovation proposal generator using Vertex AI’s Agent Development Kit (ADK).

---

## 🔧 Step 1: Initialize Google Cloud Environment

1. Go to [Google Cloud Console](https://console.cloud.google.com/).
2. Create a new project or select an existing one.
3. Ensure billing is enabled on the project.
4. Open Cloud Shell and run:

gcloud auth list  
gcloud config set project <YOUR_PROJECT_ID>

---

## 🧪 Step 2: Prototype with Google AI Studio

Navigate to Google AI Studio.

Use a simple input like:  
“I want to renovate my kitchen. I don't know where to start. Give me a detailed plan.”

- Choose **Gemini 2.5 Pro** for long-form, detailed output.
- Next, switch to **Gemini 2.0 Flash Preview** and prompt:  
  “Add flat and circular light accessories above the island area for my current kitchen.”  
- Attach a sample kitchen image to visualize the changes.

---

## 📦 Step 3: Set Up Virtual Environment

In Cloud Shell terminal:

python -m venv .venv  
source .venv/bin/activate

Install ADK:

pip install google-adk

---

## 📁 Step 4: Create Project Structure

mkdir -p agentic-apps/renovation-agent  
cd agentic-apps/renovation-agent  
touch __init__.py agent.py requirements.txt .env

You now have the base directory: `renovation-agent/`

---

## 🧠 Step 5: Implement Agent Logic

In `__init__.py`, add:

from . import agent

Download `agent.py` from the official GitHub:  
[agent.py on GitHub](Under 01-single-agent-adk/agent.py)

This file includes:

- `root_agent` definition  
- Gemini prompt generation  
- PDF creation using `store_pdf`  
- Upload to GCS

---

## 🔐 Step 6: Configure Environment Variables

Create a `.env` file and include:

STORAGE_BUCKET=next-demo-store

---

## ☁️ Step 7: Create Cloud Storage Bucket

In Cloud Shell:

gsutil mb -l us-central1 gs://next-demo-store

Enable public access (for demo only):

gsutil iam ch allUsers:objectViewer gs://next-demo-store

Alternatively, go to **Cloud Console > Storage > Bucket > Permissions**:

- Add `allUsers` as **Storage Object Viewer**
- Uncheck **"Prevent public access"**

---

## 📜 Step 8: Define Dependencies

In `requirements.txt`, add:

google-adk

Include any other packages used in the agent logic.

---

## ▶️ Step 9: Run the Agent

From the root directory:

adk run .

Optional (for web UI preview):

adk web

---

## 🎯 What the Agent Does

- Takes your kitchen renovation prompt  
- Uses Gemini to generate a detailed proposal  
- Converts it into a PDF  
- Uploads it to your Cloud Storage bucket

---

## ✅ Completion

Your agent is now live and functional. You can now test and enhance it by:

- Adding more tools (multi-agent support)  
- Using image generation  
- Connecting to additional APIs for personalization

---
