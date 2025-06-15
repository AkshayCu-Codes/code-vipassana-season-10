# 🧠 Task 1: Single-Agent Kitchen Renovation App using Vertex AI ADK

This project demonstrates how to prototype and build a single-agent application using the Vertex AI Agent Development Kit (ADK). The goal is to create an agent that generates a kitchen renovation proposal and stores the result in a Google Cloud Storage bucket.

> Where does building with AI start today?  
> For many, it begins with a simple question:  
> “Can the model actually help solve a real-world problem I care about?”  
> This project shows how to go from a prompt-based prototype in Google AI Studio to a fully functioning agent using Vertex AI and ADK.

---

## ⚙️ Setup Instructions

### 1. Clone the Repository

git clone https://github.com/AkshayCu-Codes/code-vipassana-season-10.git
cd code-vipassana-season-10/01-single-agent-adk

### 2. Create and Activate Virtual Environment

python3 -m venv .venv
source .venv/bin/activate

### 3. Install Dependencies

pip install -r requirements.txt

### 4. Configure Environment Variables

Create a `.env` file in the root directory with the following:

STORAGE_BUCKET=next-demo-store

Make sure this Cloud Storage bucket exists in your Google Cloud project.

---

## 🗂️ Project Structure

task-1/  
├── .env                  – Environment variables  
├── __init__.py           – Module entry point  
├── agent.py              – Agent logic using ADK  
├── requirements.txt      – Python dependencies  
├── context.md            – Background and goals  
├── solution.md           – Step-by-step process  
└── README.md             – Setup and run instructions

---

## ☁️ Google Cloud Setup

### Authenticate and Set Project

gcloud auth list  
gcloud config set project <YOUR_PROJECT_ID>

### Create a Cloud Storage Bucket

gsutil mb -l us-central1 gs://next-demo-store

### Allow Public Access (for demo purposes only)

gsutil iam ch allUsers:objectViewer gs://next-demo-store

Note: Disable “Prevent public access” if it's enabled. For production setups, use stricter permissions.

---

## 🚀 Run the Agent

Run the agent script:

python agent.py

This will:  
– Generate a renovation proposal  
– Store it as a PDF  
– Upload it to your GCS bucket

---

## 🧠 Agent Flow Summary

**Input:** User prompt about kitchen renovation  
**Process:** Uses Gemini and store_pdf tool  
**Output:** Proposal PDF uploaded to GCS

---

## 🛠️ Tools & Technologies Used

– Google AI Studio (Gemini 2.5 Pro & 2.0 Flash)  
– Vertex AI Agent Development Kit (ADK)  
– Google Cloud Storage  
– Python 3.9+  
– Cloud Shell or Local Terminal

---

## 📬 Feedback & Contributions

Feel free to open issues or submit pull requests for improvements.
