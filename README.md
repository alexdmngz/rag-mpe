# MPE 25/26: Intro RAG Bake-Off for Technical Q&A

### Overview
The MPE 2526 project is an evaluation pipeline for Retrieval-Augmented Generation (RAG) systems. It compares the performance and accuracy of different retrieval methodologies (BM25, Dense retrieval, and Hybrid) in answering multiple-choice questions. The project evaluates these models using a custom dataset (`ModelizaciónEmpresaUCMData.json`) and utilizes the research paper "REFRAG: Rethinking RAG based Decoding" as its primary knowledge base.

### Key features
* **Document processing:** Automates the extraction, cleaning, and semantic chunking of technical PDF documents into text format to serve as a knowledge base.
* **Retrieval pipelines:** Implements and compares three distinct retrieval strategies:
    * **BM25:** Traditional sparse lexical retrieval.
    * **Dense retrieval:** Semantic search using SentenceTransformers (`all-mpnet-base-v2`) and the ChromaDB vector database.
    * **Hybrid retrieval:** A customizable combination of BM25 and Dense retrieval scores, balanced by an alpha parameter.
* **Re-ranking:** Enhances retrieval accuracy using a Cross-Encoder (`ms-marco-MiniLM-L-6-v2`) to re-rank the top candidates.
* **LLM evaluation:** Uses the Gemini API (`gemini-2.5-flash-lite`) to answer questions based on the retrieved context, forcing the model to provide both the answer and the source reasoning.
* **Metrics & dashboards:** Calculates overall prediction accuracy and "Source Attribution Accuracy" (using fuzzy matching to verify if the LLM cited the correct reference) to determine the best-performing pipeline.

### Structure
* `src/`: Contains the main pipeline (`Script.py`) which orchestrates the document processing, sets up ChromaDB, runs the BM25/Dense/Hybrid retrievals, calls the Gemini API, and calculates the final evaluation metrics.
* `notebooks/`: Contains `Code.ipynb` for exploratory data analysis, prototyping the retrieval logic, and visualizing results.
* `data/`: Stores the evaluation dataset `ModelizaciónEmpresaUCMData.json`, containing questions, options, correct answers, and target paper references.
* `docs/`: Contains the target knowledge base documents, including the REFRAG research paper (`Paper.txt` and `Report & Results.pdf`).

Note that every document inside this repository is written in Spanish