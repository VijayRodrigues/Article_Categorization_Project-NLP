# Article Categorization Project

This project aims to build a machine learning model to automatically categorize articles into predefined categories, such as World affairs, Sports, Business, and Sci/Tech. The goal is to improve the categorization process for a media organization, InfoWorld, to help them better organize and deliver content to their audience in a timely and accurate manner.

## Project Overview

InfoWorld, a leading media organization, faces the challenge of efficiently categorizing a large volume of articles. Manual categorization is time-consuming, prone to errors, and can delay content delivery, which affects user engagement. To tackle this issue, we build a predictive model to automatically categorize articles using machine learning algorithms, improving timeliness and engagement.

## Business Problem

The media industry faces continuous challenges such as:

- **Information Overload**: The massive volume of articles makes manual categorization impractical.
- **Timeliness**: Delays in categorization can lead to outdated or irrelevant content being served.
- **User Engagement**: Personalized content delivery is crucial for maintaining user interest.

InfoWorld’s task is to build an automated solution to categorize articles into topics like World, Sports, Business, and Sci/Tech using machine learning.

## Data Dictionary

- **Article**: The body of the article containing detailed information and context.
- **Category**: The classification of the article (e.g., World affairs, Business, Sports, Sci/Tech).

## Model Overview

We compared different machine learning models for this task:

1. **Random Forest (base)**: A base Random Forest classifier without any hyperparameter tuning or class weighting.
2. **Random Forest with class_weights**: A Random Forest classifier that accounts for class imbalance by using class weights.
3. **Random Forest (tuned)**: A Random Forest classifier that has been hyperparameter-tuned for better generalization.
4. **Flan (base prompt)**: A language model (Flan) using a base prompt.
5. **Flan (improvised prompt)**: A language model (Flan) with an improvised prompt for improved performance.

## Model Performance Comparison

### Training Performance Comparison

The following table summarizes the performance of different models on the training set:

| **Model**                        | **Accuracy** | **Recall** | **Precision** | **F1**    |
|-----------------------------------|--------------|------------|---------------|-----------|
| **Random Forest (base)**          | 1.0          | 1.0        | 1.0           | 1.0       |
| **Random Forest with class_weights** | 1.0          | 1.0        | 1.0           | 1.0       |
| **Random Forest (tuned)**         | 0.961250     | 0.961250   | 0.961432      | 0.961184  |
| **Flan (base prompt)**            | 0.906250     | 0.906250   | 0.908978      | 0.905704  |
| **Flan (improvised prompt)**      | 0.904062     | 0.904062   | 0.907620      | 0.903372  |

### Observations:
- **Random Forest (base)** and **Random Forest with class_weights** achieved perfect scores (1.0) across all metrics, but this likely indicates **overfitting** to the training data.
- The **Random Forest (tuned)** model demonstrated slightly lower performance (~0.961), indicating **better generalization** and likely a more robust model.
- The **Flan models**, both base and with an improvised prompt, showed **good training performance (~0.90)**, but they underperformed compared to the Random Forest models. Minor changes in the prompt did not result in significant gains in performance.

### Validation Set Performance Comparison

On the validation set, the performance metrics for the models were as follows:

| **Model**                        | **Accuracy** | **Recall** | **Precision** | **F1**    |
|-----------------------------------|--------------|------------|---------------|-----------|
| **Random Forest (base)**          | 0.897        | 0.897      | 0.897         | 0.897     |
| **Random Forest with class_weights** | 0.895        | 0.895      | 0.895         | 0.895     |
| **Random Forest (tuned)**         | 0.896        | 0.896      | 0.896         | 0.896     |
| **Flan (base prompt)**            | 0.227        | 0.227      | 0.227         | 0.227     |
| **Flan (improvised prompt)**      | 0.230        | 0.230      | 0.230         | 0.230     |

### Observations:
- **Random Forest (base)** performed the best on the validation set across all metrics (~0.897), outperforming both the tuned and class-weighted versions.
- **Flan models** experienced a significant performance drop, with metrics around **0.22–0.23**, suggesting poor generalization and potentially inadequate prompt formulation or model limitations for this task.
- The **improvised prompt** for Flan did not show significant improvements over the base prompt, and in some metrics, it performed slightly worse.

## Insights and Recommendations

### Actionable Insights:
- **Random Forest** remains the most reliable choice for the task due to its consistent performance across both training and validation sets.
- The **perfect training scores** for the base and class-weighted Random Forest models suggest overfitting. They should be used with caution and validated thoroughly.
- **Flan models** are not yet viable for this classification task. Their poor generalization performance indicates that they overfit to the training data and likely misunderstand the task structure.
- **Prompt engineering** alone is insufficient for closing the performance gap for Flan models. **Few-shot prompting or fine-tuning** may be necessary for improvement.

### Recommendations:
- **Random Forest (base or tuned)** should be prioritized for production use due to its strong and stable performance on unseen data.
- Avoid deploying **Flan-based models** for the current classification task as they fail to generalize well.
- If **interpretability** or **natural language interaction** is important for the business use case, Flan can still be used for secondary tasks such as explanation generation or content summarization but not as the primary classifier.
- **Further investment in prompt engineering** for Flan is not recommended unless the use case demands more language-based reasoning.
- For higher accuracy and robustness, consider exploring **tree-based boosting models** like **XGBoost** or **LightGBM** as potential alternatives.
- **Monitor model performance post-deployment** to ensure it aligns with validation results and accounts for possible data drift.
