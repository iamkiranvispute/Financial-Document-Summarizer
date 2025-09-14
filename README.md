# 📊 Financial Report Summarizer (AI-Powered)

An end-to-end pipeline for **summarizing large financial reports (100–300+ pages)** into concise executive summaries.  
The system extracts :
- Structured text
- Unstructured text,
- tables, and
- multi-column content

from PDFs -->> processes them into manageable chunks --> and generates summaries using **state-of-the-art transformer models** (BART, DistilBART, LongT5).  

**_-->> Designed for enterprise-scale use where **data privacy, auditability, and accuracy** matter more than one-off ChatGPT summaries._**

## Features

- **PDF ingestion & cleaning**
  - Handles multi-column reports, removes headers/footers, cleans noisy text.
- **Table understanding**
  - Converts tabular financial data into **narrated text + numeric stats** before summarization.
- **Hierarchical summarization**
  - Chunk → Section → Final summary (2–3 pages for a 300-page report).
- **Model flexibility**
  - Swap summarizers easily: DistilBART (fast), BART (detailed), LongT5 (longer context).
- **Evaluation metrics**
  - Compression ratio, and summary length stats.
  - ROGUE Scores can also be computed if sample summary is available.
- **Deployment ready**
  - Modular `src/` code and optional **FastAPI wrapper** for turning into an API service.

---

## Installation

Clone the repo:
 ````bash
git clone https://github.com/<your-username>/financial-report-summarizer.git
cd financial-report-summarizer
````

1. Run the notebook

   - Open notebooks/summarizer_pipeline.ipynb in Google Colab or Jupyter.
   - Update this line with your PDF path:
     ```bash
        pdf_path = "data/sample_report.pdf"
   - Run all cells → outputs appear in data/sample_outputs/.

2. Switch models
   - Change this line in the pipeline:
       ```bash
       summarizer = pipeline("summarization", model="facebook/bart-large-cnn", device=device)_
       ```
  - Options:
     - sshleifer/distilbart-cnn-12-6 → Fastest, lighter summaries.
     - facebook/bart-large-cnn → More detailed, slower.
     - google/pegasus-xsum → Too short, not recommended for long docs.
     - google/long-t5-local-base → Long input support, heavy GPU needed.

3. Outputs

    1. chunk_summaries.csv → summaries of each text chunk
    2. Table_summaries.csv → summarized narratives of tables
    3. section_summaries.csv → mid-level summaries
    4. final_summary_long.txt → final 2–3 page executive summary

## Evaluation
   The pipeline computes:
      Compression ratio → (summary length / original length).
      Average summary length → mean words per summary.
  ```bash
      Compression ratio: 0.12
      Avg chunk summary length: 65.3 words
  ```

## Why not just use ChatGPT?
- Data privacy: Enterprise docs stay on-premise. No external uploads.
- Document complexity: Handles multi-column layouts and tables that ChatGPT often scrambles.
- Traceability: Produces chunk + section + final summaries with direct mapping back to the original text.
- Evaluation metrics: Provides ROUGE/compression benchmarks for explainability.
- Scalability: API-ready, automated, not reliant on manual prompts.

## Roadmap

- Improve table summarization with TAPAS (table question answering).
- Add GPU/CPU dynamic routing for efficiency.
- Support scanned PDFs (OCR with Tesseract).
- Add Dockerfile for containerized deployment.

## 👤 Author

### **Kiran Vispute**
- LinkedIn : https://www.linkedin.com/in/kiranvispute/
- GitHub : https://github.com/iamkiranvispute/
    
