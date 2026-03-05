# 📜 RenAIssance-OCR Pipeline
**Evaluation Test I for Google Summer of Code (GSoC) 2026** **Organization:** CERN-HSF (RenAIssance Project)  
**Author:** Warda Khan  

## 🎯 Project Abstract
This repository contains the Proof of Concept (PoC) and code evaluation for the RenAIssance project's **Test I: Optical Character Recognition of printed sources**. The primary objective is to build a robust OCR pipeline capable of accurately transcribing degraded 17th-century printed Spanish historical sources (e.g., the `PORCONES` dataset).

## 🧠 Architecture & Methodology
Transcribing historical documents presents extraordinary challenges, including obsolete fonts, low contrast, and severe ink degradation. Traditional monomodal OCR systems struggle significantly with these artifacts. 

To address this, I have developed a multi-stage **Vision-Language pipeline**:

1. **Document Parsing & Layout Extraction:** Utilizing `PyMuPDF` to intelligently extract the main text blocks from high-resolution PDF scans while systematically disregarding irrelevant marginalia and embellishments.
2. **Vision Engine (Feature Extraction):** Deploying a Transformer-based OCR model (`microsoft/trocr-base-printed`) as the core extraction mechanism to interpret the historical typography.
3. **Contextual Language Layer:** Integrating Google's `Gemini 2.5 Flash` strictly as a zero-shot semantic post-processor. The LLM acts as an intelligent filter to correct machine-reading artifacts and infer unclear text based on linguistic patterns, while strictly preserving historical 17th-century Spanish orthography.

## 📊 Evaluation Metrics & SOTA Alignment
The pipeline's performance was rigorously evaluated using the **Character Error Rate (CER)**. 

* **Baseline Approach (Tesseract CNN/RNN):** ~89.47% CER (Catastrophic failure on complex degraded ink patterns).
* **Proposed Pipeline (TrOCR + Gemini):** **23.53% CER 🏆**

This **~65.94% absolute reduction in error** validates the recent literature's hypothesis: Large Language Models are highly effective late-stage filters for complex historical OCR tasks, bypassing the immediate need for massive dataset-specific fine-tuning.

## 📂 Repository Structure
* `RenAIssance_Test_I.ipynb`: The main Jupyter/Colab notebook containing the entire pipeline code, from PDF parsing to metric evaluation.
* `RenAIssanceTestPdf.pdf`: The exported PDF of the notebook showcasing the fully executed output, cropped images, and CER calculations.
* `requirements.txt`: List of dependencies required to run the pipeline locally.

## 💻 How to Run Locally
1. Clone this repository:
   ```bash
   git clone [https://github.com/khanwarda/RenAIssance-OCR-GSoC26.git](https://github.com/your-khanwarda/RenAIssance-OCR-GSoC26.git)
2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
3. Open RenAIssance_Test_I.ipynb in Jupyter Notebook or Google Colab.
4. Provide your Gemini API key in the designated cell.
5. Upload the target PDF (e.g., PORCONES.23.5 - 1628.pdf) and run all cells.
