# Predicting Asset Intensity from Business Descriptions Using BERT

This project explores how large language models, specifically BERT, can be leveraged to understand and predict key financial ratios of U.S. public companies based solely on their business description texts. Using a set of recent annual financial data and company descriptions, the project builds and evaluates models to predict three core financial ratios, demonstrating the intersection of NLP and financial analysis for corporate insight.

## Tools Used

- Python (pandas, numpy, scikit-learn, transformers, matplotlib, seaborn, plotly)
- Jupyter/Colab Notebook (interactive analyses, code execution, and documentation)
- BERT/DistilBERT (via HuggingFace `transformers` library)
- Compustat via WRDS (data extraction)
- Various CSV datasets (provided and downloaded)

## Dataset Overview

### Sources

- Business Descriptions:  
  `stock_des.csv`- Contains the ticker and a recent business description for each firm.
- Financial Statement Data:  
  Raw annual financial data for 2,800+ U.S. companies, selected via tickers and datadates in 2023, extracted from Compustat through WRDS.
- Reference Files:  
  `rev.csv`, `ta.csv` - Additional auxiliary files with company financial info.

### Key Variables

- `ticker`: Stock symbol for each company (linking key across datasets).
- `description`: Natural-language company description.
- Raw financial fields: `at` (total assets), `sale` (sales/revenue), `seq` (shareholders' equity), and others.
- Derived ratios: Three financial ratios calculated for analysis.

## Methodology & Analysis

### Data Preparation

- **Merging:** Linked `stock_des.csv` with annual financial data using `ticker`.
- **Cleaning:** Checked for missing values and extreme outliers for all required variables.
- **Ratio Construction:** Computed three significant and widely available financial ratios of choice for each company
  - Gross Profit to Assets ratio
  - Gross Profit to Margin ratio
  - Debt to Assets ratio
- **Categorization:** For each ratio, created a binary classification (`High` vs. `Low`), typically using the median split to ensure balanced classes.
- **Filtering:** Excluded companies missing required text or ratio information.

### Text Analysis with BERT

- **Tokenization:** Company descriptions were tokenized and encoded using a pretrained BERT (DistilBERT) model.
- **Embedding:** BERT-generated embeddings (vector summaries) for each description, capturing deep semantic meaning in the text.
- **Input Standardization:** Sequences padded/truncated for model compatibility.

### Predictive Modeling

Separate **logistic regression models** were trained for each ratio's high/low category label, using the BERT-derived textual embeddings as features.

#### Model Development Flow

1. **Feature Extraction:** Transform business descriptions to BERT embeddings.
2. **Train/Test Split:** Partition data for consistent out-of-sample evaluation.
3. **Logistic Regression:** Fit the classifier to predict each ratio (high/low), based on text features.
4. **Dummy Baseline:** Trained a "majority class" dummy classifier for comparison.
5. **Evaluation:** Assessed each model's accuracy using cross-validation and compared it with the dummy baseline.

## Key Results

**Summary Table:**

| Ratio                       | BERT Model Accuracy | Baseline Accuracy |
|-----------------------------|--------------------|------------------|
| Gross Profit to Asset ratio | 77.72%             | 50.9%            |
| Gross Profit to Margin      | 76.13%             | 50.9%            |
| Debt to Asset ratio         | 60.03%             | 50.9%            |

These results show that pretrained language models extract meaningful financial signals from business narratives, particularly for profitability and asset utilization ratios, and add clear value over naive baselines.

- BERT-based models significantly outperformed the random/dummy baseline of 50.9% accuracy for all three financial ratios, confirming substantial predictive power in company business descriptions.
- **Gross Profit to Asset Ratio:** Achieved the highest predictive accuracy at 77.72%, indicating that business descriptions are especially informative about a firm’s operational structure and asset utilization.
- **Gross Profit to Margin Ratio:** Was also highly predictable from text, with a strong accuracy of 76.13%, suggesting business narratives effectively reflect profitability characteristics.
- **Debt to Asset Ratio:** Demonstrated moderate predictability at 60.03%, exceeding chance but indicating that leverage signals are present in textual descriptions, albeit to a lesser extent.

## Business Insights & Interpretation

- Business descriptions do encapsulate meaningful signals relating to company structure, strategy, and risk, as evidenced by their correlation with certain financial ratios.
- The model is most effective for ratios aligned with visible business strategies (e.g., asset intensity, leverage) as opposed to those heavily influenced by hidden accounting or exogenous factors.
- Model limitations include the challenge of capturing quantitative nuance and the need for large training sets to leverage deep learning on financial texts.
- Potential Applications: Screening companies for targeted financial risk, due diligence, or automated investor research—reducing manual analyst effort.

## Learning & Takeaways

- Textual data is a valuable but imperfect predictor; it works best when financial structures are inherently described in the business narrative.
- BERT provides a robust toolkit for semantic feature extraction in financial contexts.
- Interpreting NLP models in finance requires domain knowledge to assess which ratios are text-reflective and where alternate data is essential.
- Next steps could involve combining textual embeddings with classic financial ratios for richer, multimodal predictive models.

## Project Details

- **Project Completed:** Spring 2024  
- **Course:** BA870/AC820 Financial Analytics, Boston University MSBA

*This README documents a project at the intersection of NLP and finance, demonstrating how deep learning methods like BERT can unlock new signals about corporate financial health from narrative texts.*
