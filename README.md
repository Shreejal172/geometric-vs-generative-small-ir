# Geometric vs. Generative Retrieval Models (Small Datasets)

This project compares the performance of two fundamental Information Retrieval models:
1.  **Geometric Model**: Vector Space Model (VSM) using TF-IDF and Cosine Similarity.
2.  **Generative Model**: Query Likelihood Model (QLM) using Dirichlet Smoothing.

The comparison is performed on two classic small datasets: **CISI** and **CRAN**.

## Datasets

*   **CRAN (Cranfield Collection)**: [https://ir.dcs.gla.ac.uk/resources/test_collections/cran/](https://ir.dcs.gla.ac.uk/resources/test_collections/cran/)
*   **CISI (Institute for Scientific Information)**: [https://www.kaggle.com/datasets/dmaso01dsta/cisi-a-dataset-for-information-retrieval/code](https://www.kaggle.com/datasets/dmaso01dsta/cisi-a-dataset-for-information-retrieval/code)

## Observations & Conclusion

For these specific small datasets, the **TF-IDF (Geometric) model generally performs better** than the Query Likelihood Model.

**Reasons:**
*   **Data Sparsity**: Small datasets like CISI and CRAN have limited vocabulary and document count, making it difficult for probabilistic models to accurately estimate language models without overfitting or underfitting.
*   **Robustness of TF-IDF**: TF-IDF is highly effective at keyword matching and assigning weights to rare terms, which is often sufficient for retrieving relevant documents in smaller, focused collections where semantic complexity is lower.
*   **Smoothing Sensitivity**: The Query Likelihood Model relies heavily on smoothing parameters (like $\mu$ in Dirichlet smoothing). On small datasets, finding a static parameter that generalizes well across all queries is challenging.

## Future Improvements

To enhance the performance of the retrieval system, specifically the generative components, the following improvements are proposed:

1.  **Using Larger Datasets**: Larger and more diverse datasets can be utilized to improve the model’s performance, especially for the probabilistic Query Likelihood Model (QLM). More data allows for better probability estimation and generalization.
2.  **Query Expansion**: Query Expansion can be introduced to handle semantic nuances and similar words efficiently. Additionally, the use of **Pseudo-Relevance Feedback (PRF)** can be implemented to automatically bridge the gap between short queries and document abstracts by analyzing common words in initially retrieved documents (helping to capture word relations).
3.  **Dynamic Smoothing**: The system can be improved by introducing a method to automatically fine-tune the smoothing parameter. Instead of using a static value provided by the user, the program could iterate multiple times to find the optimal smoothing value dynamically.
