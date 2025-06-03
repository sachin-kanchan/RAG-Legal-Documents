
## Setup and Usage

1.  **Environment:** Ensure a Python 3.x environment with necessary libraries installed (e.g., LangChain, OpenAI, ChromaDB, RAGAS, NLTK, scikit-learn, Pandas, Matplotlib, Jupyter).
2.  **OpenAI API Key:** Set your OpenAI API key as an environment variable named `OPENAI_API_KEY`.
3.  **Data:**
    *   Place the `rag_legal` directory (with `corpus` and `benchmarks` subfolders containing the respective `.txt` and `.json` files) in the project's root, or adjust paths within the notebook.
4.  **NLTK Resources:** The notebook handles the download of required NLTK resources (e.g., `punkt`, `stopwords`) if not already present.

## Running the Analysis

1.  Launch the Jupyter Notebook (`Aravind_Sachin_RAG_Legal_Docs.ipynb`).
2.  Execute the cells sequentially to perform:
    *   Data loading, cleaning, and preprocessing.
    *   Exploratory Data Analysis and visualization.
    *   Document chunking and embedding.
    *   Creation or loading of the ChromaDB vector store (controlled by the `use_existing_db` variable).
    *   Initialization of the RAG chain.
    *   Automated evaluation against benchmark questions using ROUGE, BLEU, and RAGAS metrics. The number of questions for full evaluation can be adjusted via `NUM_QUESTIONS_FOR_OVERALL_EVAL`.

## Key Findings & Conclusion

The project successfully demonstrated the construction of a functional RAG pipeline using `gpt-4.1-mini`. Key findings from the evaluation on 100 benchmark questions include:

*   **Corpus Understanding:** Exploratory Data Analysis, including TF-IDF similarity matrices (New Plot 2 versions), revealed a diverse legal corpus.
    *   The "First 10 Documents" plot showed a tight cluster for specific corporate/financial agreements (`Doc7-Century Bancorp`, `Doc8-GP_Strategies_C`, `Doc9-Virtusa Corpora` with similarity scores 0.88-0.95) and moderate similarities for potential tech/service agreements.
    *   The "Random 10 Documents" plot showed more dispersed similarities but highlighted pairs like `Doc1-KIROMICBIOPHARM` and `Doc3-GLOBALTECHNOLOG` (0.79 similarity), indicating varied but specific inter-document relationships.
*   **High Faithfulness:** The system generates answers highly grounded in the retrieved context (RAGAS Faithfulness: **0.9451**).
*   **Good Answer Relevancy:** Answers are generally pertinent to the questions (RAGAS Answer Relevancy: **0.7158**).
*   **Retrieval Performance:**
    *   Context Precision was moderate at **0.5692**, suggesting that while relevant context was retrieved, some noise was also present.
    *   Context Recall was also moderate at **0.4800**, indicating the retriever fetched about half of the ideally necessary information. This is a primary area for future optimization.
*   **Lexical vs. Semantic Evaluation:**
    *   ROUGE scores (e.g., ROUGE-1 F1: **0.3660**) showed some lexical overlap with ground truths.
    *   However, the BLEU score was consistently **0.0000**, and RAGAS Answer Correctness was relatively low at **0.3368**. This common discrepancy in RAG systems suggests that while answers are faithful to the *retrieved context* and relevant to the *question*, their phrasing often differs significantly from the (often snippet-like) ground truth answers.

**In conclusion,** this RAG system provides a solid foundation for legal information extraction, particularly excelling in its faithfulness to retrieved evidence. Future work should focus on enhancing the retrieval mechanism (especially context recall and precision), further prompt engineering, and continued qualitative analysis to complement quantitative metrics and refine the system's ability to align with specific answer formats if required.

## Potential Future Work

*   Advanced chunking and retrieval strategies (e.g., semantic chunking, MMR, re-ranking).
*   Deeper prompt engineering and experimentation with different LLM models for generation.
*   Targeted investigation into the zero BLEU scores.
*   Expansion of qualitative analysis to complement quantitative metrics.

## Contributing

Contributions, issues, and feature requests are welcome. Please feel free to check the [issues page](https://github.com/sachin-kanchan/RAG-Legal-Documents/issues) of this repository. 

## License

Consider adding a license (e.g., MIT, Apache 2.0) if you plan to share this project publicly.
