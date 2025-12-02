# 🧠 Agentic AI Resume Shortlister  
An end-to-end automated resume screening system powered by **Agentic AI**, **Google Gemini**, **Python**, **Telegram**, **Google Sheets**, and **n8n**.


https://github.com/user-attachments/assets/430a7144-c523-4c85-bb90-b786b0b18ae8


This system allows HR teams to upload **PDF resumes** or **ZIP files** containing multiple resumes through Telegram. The workflow automatically extracts information, generates ATS scores, classifies candidates, stores results in Google Sheets, and sends automated selection/rejection emails.

---

## 📌 Features

- 📥 **Resume upload through Telegram** (PDF or ZIP)
- 🤖 **AI-powered resume parsing** using Google Gemini
- 🧮 **ATS scoring automation**
- 📂 **ZIP decompression + multi-resume processing**
- 📄 **PDF text extraction**
- 📊 **Google Sheets integration (Selected / Rejected sheets)**
- 📧 **Automated Gmail notifications**
- 🔁 **Loop & Merge handling for bulk resumes**
- ⏳ **Wait-time buffer for stability**
- 🧪 **Downloadable JSON file for hands-on testing**

---

## 🏗️ Workflow Architecture (Step-by-Step)

Below is the complete flow of your Agentic AI Resume Shortlister:

---

# 1️⃣ Telegram Trigger – Resume Upload

The workflow starts when a user uploads:

- A **single PDF resume**, or  
- A **ZIP file** containing multiple PDF resumes

---

# 2️⃣ IF Node – Greeting Filter

Checks if the user sends:
- “hi”
- “hello”
- “hey”

### ✔ If TRUE:
The bot replies on Telegram:  
> **"Upload a ZIP file or a PDF file."**

### ❌ If FALSE:
Workflow moves to the **Switch Node**.

---

# 3️⃣ Switch Node – File Type Routing

Classifies the uploaded file based on its extension:

## **🟩 Case 1: .pdf File**

If the file ends with `.pdf`, the workflow performs:

### 🔹 Extract From File  
Extracts text from the PDF and separates resume sections.

### 🔹 AI Agent (Google Gemini)  
Analyzes the resume and returns:
- Name  
- Email  
- Mobile Number  
- ATS Score  

### 🔹 Python Node  
Extracts variables from the AI output JSON.

### 🔹 Edit Fields Node  
Creates fields:
- `name`
- `email`
- `mobile_no`
- `ats_score`

### 🔹 IF Node – ATS Score Check  
- **ATS > 75** → Added to **Selected Sheet**  
- **ATS < 75** → Added to **Rejected Sheet**

### 🔹 Gmail Node  
Automatically sends selection/rejection mail to the candidate.

---

## **🟧 Case 2: .zip File**

If the file ends with `.zip`, the system processes multiple resumes:

### 🔹 Compression Node  
Decompresses the ZIP file.

### 🔹 Split Out Node  
Splits all internal PDFs for individual processing.

### 🔹 Loop Over Items  
Processes each resume **one-by-one**.

Inside the loop:

#### 1. Extract PDF Text  
Resume text is extracted.

#### 2. AI Agent (Google Gemini)  
Extracts:
- Name  
- Email  
- Mobile Number  
- ATS Score  

#### 3. Python Node  
Extracts JSON values.

#### 4. Edit Fields Node  
Creates structured output objects.

#### 5. IF Node  
- **ATS > 75** → Insert into **Selected Sheet**
- **ATS < 75** → Insert into **Rejected Sheet**

#### 6. Gmail Node  
Sends email to each processed candidate.

### 🔹 Merge Node  
Merges both email outputs.

### 🔹 Wait Node  
8 seconds delay added for stable email processing.

---

# 📊 Output Sheets

### **Selected Candidates Sheet**
| Name | Email | Mobile | ATS Score |

### **Rejected Candidates Sheet**
| Name | Email | Mobile | ATS Score |

All candidate details and scores are automatically logged.

---

# 📦 Download the Workflow JSON

You can download the `.json` workflow file and directly import it into **n8n** for hands-on testing.
https://github.com/shubham132004/Resume-Shortlister-Using-N8N/tree/main/JSON%20FILE

---

# 🧰 Tech Stack

- **n8n (Advanced workflow automation)**
- **Google Gemini Chat Model (AI-powered resume parsing)**
- **Python**
- **Telegram Bot**
- **Gmail API**
- **Google Sheets**
- **File Compression & PDF Parsing**

---

# 🖼️ Workflow Screenshot

> <img width="1284" height="715" alt="Screenshot 2025-12-02 112247" src="https://github.com/user-attachments/assets/1c607ab0-f0dc-4713-9091-e0c149a2261c" />


---


