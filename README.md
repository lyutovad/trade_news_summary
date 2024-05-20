## Trade News Summarization Project



This project focuses on summarizing trade news articles to efficiently extract key insights, aiding stakeholders in the fast-paced trade environment. The summarization process involves data exploration, model training, and performance evaluation using specific metrics.

**Project Structure**

1. **Data Exploration and Analysis (data_eda)**[README.md](setup/README.md)
   - Files: [eda.ipynb](data_eda/eda.ipynb), [eda_numbers.ipynb](data_eda/eda_numbers.ipynb)`
   - Purpose: To explore and analyze the data for better model performance.

2. **Metrics Evaluation (metrics)**
   - Files: [simple_model_score.ipynb](metrics/simple_model_score.ipynb)
   - Purpose: To evaluate the performance of the models using various metrics.

3. **Model Training (models)**
   - Files: [finetune-TinyLlama-1.1B-Chat.ipynb](models/finetune-TinyLlama-1.1B-Chat.ipynb), [finetune-mistral-7b-for-news-summary.ipynb](models/finetune-mistral-7b-for-news-summary.ipynb), [mt5-multilingual-xlsum.ipynb](models/mt5-multilingual-xlsum.ipynb)
   - Purpose: To provide code examples for training different models for summarization tasks.
---
**Detailed Description**

This project aims to enhance the effectiveness of summarizing trade news articles, which is challenging due to the specific data requirements, such as country references, product details, and key figures. The project involves:

1. **Data Exploration and Analysis**
   - Initial exploration to understand data requirements and distribution.
   - Analysis to determine the impact of various factors on the summary length and content coverage.

2. **Model Training**
   - Utilized multiple models, including MT5, TinyLlama, and Mistral Instruct, each chosen for their capabilities in handling multilingual data and instruction-following tasks.
   - Training involved fine-tuning models on a dataset of trade news articles in both Russian and English.

3. **Metrics Evaluation**
   - The performance of the models was evaluated using BERTScore, which provides insights into precision, recall, and F1 scores.
   - The evaluation focused on how well the models could convey the necessary information from the original text in the summaries.

---

**Dataset**

The dataset comprises news articles related to trade in Russian and English. It includes manually curated summaries with essential elements such as import/export data, company mentions, and product/country references. The dataset was preprocessed to remove introductory words, replace vague time references with specific dates, and ensure company mentions were included.

---
**Models**

- **MT5 Model**: Selected for its multilingual capabilities and effectiveness in handling diverse language pairs.
- **TinyLlama Model**: Chosen for its compact size and rapid inference speed, suitable for chat applications and efficient processing.
- **Mistral Instruct Model**: Tailored for instruction-following tasks with a focus on thematic coherence.

---
**Results**

The project resulted in a functional model that significantly improved the summarization process compared to previous extractive methods. The MT5 model was integrated into the news processing pipeline, replacing part of the annotators' tasks and streamlining workflows. However, challenges remain in handling complex news articles, which require manual adjustments.

---
**Conclusion**

This research phase involved testing various Transformer models and evaluating their performance. The selected MT5 model is actively used in the news processing pipeline, though further improvements are needed for complex news articles. Future work includes experimenting with entity extraction, sentence compression, and factual consistency verification to enhance summarization quality.

**References**

Refer to the project documentation for a detailed list of references and further reading on the methodologies and models used.
