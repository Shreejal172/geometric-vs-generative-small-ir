# Geometric vs. Generative Retrieval Models (Small Datasets)

This project compares the performance of two fundamental Information Retrieval models:
1.  **Geometric Model**: Vector Space Model (VSM) using TF-IDF and Cosine Similarity.
2.  **Generative Model**: Query Likelihood Model (QLM) using Dirichlet Smoothing.

The comparison is performed on two classic small datasets: **CISI** and **CRAN**.

## Datasets

### CISI (Information Science)
*   **Source**: [Kaggle Dataset](https://www.kaggle.com/datasets/dmaso01dsta/cisi-a-dataset-for-information-retrieval/code)
*   **Structure**: 1,460 documents (titles + abstracts), 112 queries.
*   **Relevance Judgments**: Available for 76 queries. Note that different queries have different numbers of relevant documents (e.g., Query 1 has 46, Query 4 has 8), so Recall is calculated relative to the specific query's set of relevant docs.

### CRAN (Aerodynamics)
*   **Source**: [Glasgow ID Dataset](https://ir.dcs.gla.ac.uk/resources/test_collections/cran/)

## Retrieval Models

1.  **Vector Space Model (VSM)**: Uses TF-IDF for weighting terms and Cosine Similarity to measure the angle between query and document vectors. It is effective for catching specific keywords.
2.  **Language Model (LM)**: Uses Dirichlet Smoothing ($\mu=4000$) to estimate the probability of generating the query from the document model. It handles term frequency distribution differently, penalizing long documents less aggressively than some vector normalizations.

## Evaluation Metrics

The project uses the following metrics to evaluate performance:

*   **Recall**: Calculated as `(Number of matches) / (Total relevant docs for that query)`. This is normalized per query since the number of relevant documents varies.
*   **Precision@10**: The fraction of relevant documents in the top 10 retrieved results.
*   **MAP@10 (Mean Average Precision)**: The average precision at rank 10, averaged across all queries. This rewards placing relevant documents higher in the top 10.
*   **nDCG@10**: Normalized Discounted Cumulative Gain at 10. This measures ranking quality by giving more credit to relevant items appearing earlier in the list, comparing against an ideal ranking.

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
