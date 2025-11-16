# Dynamic-ETL-Pipeline
AuraVerse Hackathon Project

🧠 **Dynamic ETL Pipeline for Unstructured & Multi-Format Data**

### 🚀 Auto-Schema Generation • Schema Versioning • Multi-Format Extraction • Dynamic Storage and parsing Multi Format Data

---

## 📌 **Overview**

Modern data sources (scrapers, logs, documents, user uploads) produce *messy and unpredictable data*.
Traditional ETL pipelines break because they require **fixed schemas**, but real-world data **changes frequently**.

This project solves that problem by building a **dynamic ETL pipeline** capable of:
```
✔ Accepting *any file format* (PDF, CSV, DOCX, TXT, HTML, JSON, images, mixed-format files)
✔ Extracting data intelligently
✔ Generating schemas automatically
✔ Creating new schema versions when structure changes
✔ Storing both raw and normalized data
✔ Tracking schema evolution over time

Perfect for real-world messy data environments.
```
---

# 🏗️ **Architecture**

```
        ┌──────────────────┐
        │  File Ingestion  │
        └────────┬─────────┘
                 ↓
        ┌────────────────────────┐
        │  Content Classifier    │
        └────────┬──────────────┘
                 ↓
  ┌─────────────────────────────────┐
  │   Multi-Format Extraction Layer │
  └───────┬───────────────┬────────┘
          ↓               ↓
   PDF Extractor      CSV Extractor    DOCX Extractor   Image OCR   HTML/Text Parser
          ↓               ↓                    ↓             ↓            ↓
  ────────────────────────────── Extracted Unified Data ────────────────────────────────

                 ↓
        ┌────────────────────┐
        │ Dynamic Schema Gen │
        └────────┬───────────┘
                 ↓
        ┌────────────────────┐
        │ Schema Drift Check │
        └────────┬───────────┘
                 ↓
        ┌────────────────────┐
        │ Schema Versioning  │
        └────────┬───────────┘
                 ↓
     ┌────────────────────────────┐
     │ Raw + Normalized Storage   │
     └────────────────────────────┘
```

---

# 🎯 **Key Features**

## **1️⃣ Accepts Any File Format**

The backend handles *content-based detection*, NOT extension-based:

* PDFs
* CSVs
* Images (OCR)
* HTML
* Plain text
* DOCX
* JSON
* Even files that contain **multiple formats inside** (e.g., HTML + images + JSON)

* The backend inspects the file’s actual content (MIME type, magic bytes, and patterns) to determine format, rather than relying on the filename or extension.

---

## **2️⃣ Multi-Layer Extraction Engine**

Each format uses a specialized extractor:

* PDF → text + metadata
* CSV → rows + headers
* HTML → cleaned text + tags
* Images → OCR text
* DOCX → paragraphs + tables
* Mixed files → processed segment-by-segment

All extracted into a **unified structured object**.
---

## **3️⃣ Dynamic Schema Inference**

The pipeline:

* Scans extracted data
* Detects fields
* Infers data types
* Handles nested structures
* Normalizes inconsistent fields

Example inferred schema:

```json
{
  "title": "string",
  "amount": "float",
  "timestamp": "datetime",
  "images_text": "array"
}
```
---

## **4️⃣ Schema Drift Detection**

Your backend compares the **newly inferred schema** with the **latest stored version**.

If ANY change is found:

* New field added
* Field removed
* Data type changed
* New nested structure appears

Then → a new schema version is created.

---

## **5️⃣ Schema Version Control (Registry)**

Every version includes:

* version number
* schema structure
* timestamp
* diff from previous version

Example:

```
v1 → name, email  
v2 → + html_text  
v3 → + ocr_results  
v4 → data type change in "amount"
```

This enables full trackability and partial backward compatibility.

---

## **6️⃣ Raw + Normalized Storage Layers**

The backend stores:

### ✔ **Raw Storage**

Exact file content + extraction outputs.

### ✔ **Normalized Storage**

Cleanly transformed data mapped to the inferred schema.

### ✔ **Schema Metadata**

Current schema version and details.

### ✔ **Schema History**

Every version ever created.

---

## **7️⃣ Frontend Dashboard**

Shows:

* Total files processed
* Schema evolution timeline
* File type distribution
* Number of records
* Extraction success/failure stats
* Number of versions
* Details

Built using:
**HTML5 + CSS + JavaScript**

---


# 🧪 **How the Pipeline Works**
```
1️⃣ User uploads any file
2️⃣ System identifies the content inside it
3️⃣ Extractors pull meaningful data
4️⃣ Schema is generated from extracted fields
5️⃣ Schema compared with previous version
6️⃣ If changed → new version created
7️⃣ Data stored in raw + normalized format
8️⃣ Dashboard updates automatically
```
---

# 🚀 **Installation**

```
git clone https://github.com/yourrepo/dynamic-etl.git
cd backend
npm install
node app.js
```

---

# 📌 **API Endpoints**

### `POST /upload`

Upload any file.

### `GET /schema/latest`

Fetch latest schema version.

### `GET /schema/versions`

Get schema history.

### `GET /records`

Fetch normalized stored records.

### `GET /stats`

Pipeline statistics.

---

# 🧩 **Tech Stack**

* **HTML5**
* **CSS**
* **JavaScript** 
* **Node.js + Express** (backend server)
* **Multer** (file uploads)
* **pdf-parse** (PDF extraction)
* **PapaParse** (CSV parsing)
* **Tesseract.js** (OCR for images)
* **Mammoth** (DOCX extraction)
* **Cheerio** (HTML parsing)
* **MongoDB** (dynamic storage + versioning)

---

# 🏆 **Why This Project Stands Out**
```
✔ Can handle any data thrown at it
✔ Fully automated schema evolution
✔ Complete version history
✔ Supports mixed-format files
✔ Pipeline mimics real-world enterprise ETL systems
```
---

# 🤝 **Contributors**
```
Team AuraDevs • AuraVerse • 2025
Amartya Majumder
Bhumi N Deshpande
Akash Patel
```
---
