# LLM-Paraphrase-Evaluation - Paraphrase Robustness in Large Language Models
Evaluating paraphrased answer consistency of large language models in multiple-choice commonsense questions.

## Overview
This project investigates the robustness of large language models to paraphrased inputs. We evaluate whether models produce consistent and correct answers when the same commonsense question is paraphrased into varying levels of semantic and structural change. 

The project uses the **CommonsenseQA** dataset:

Talmor, A., Herzig, J., Lourie, N., & Berant, J. (2019).  
*CommonsenseQA: A Question Answering Challenge Targeting Commonsense Knowledge*.  
Proceedings of NAACL-HLT 2019.  
https://aclanthology.org/N19-1421

### BibTeX Citation

```bibtex
@inproceedings{talmor-etal-2019-commonsenseqa,
  title = "{C}ommonsense{QA}: A Question Answering Challenge Targeting Commonsense Knowledge",
  author = "Talmor, Alon and Herzig, Jonathan and Lourie, Nicholas and Berant, Jonathan",
  booktitle = "Proceedings of NAACL-HLT 2019",
  year = "2019",
  publisher = "Association for Computational Linguistics",
  url = "https://aclanthology.org/N19-1421",
  doi = "10.18653/v1/N19-1421"
}
```
## Models Used
- **T5 Paraphrase Model**
  - Model: `Vamsi/T5_Paraphrase_Paws`
- **BART Large MNLI**
  - Model: `facebook/bart-large-mnli`
- **Model Inference (LLaMA, Mistral, Yi)
  - LLaMA 2 7B Chat
    - Model: `meta-llama/Llama-2-7b-chat-hf`
  - Mistral 7B Instruct
    - Model: `mistralai/Mistral-7B-Instruct-v0.1`
  - Yi 6B Chat
    - Model: `01-ai/Yi-6B-Chat`

## Objectives
- Analyze semantic drift using Natural Language Inference
- Evaluate model accuracy across paraphrases
- Measure consistency between original and paraphrased questions
- Quantify model instability using prompt sensitivity metrics
- Identify failures with failure taxonomy and high-risk analysis

## Pipeline
1. **Data Preparation**
   - Load CommonsenseQA dataset
   - Filter and preprocess questions

2. **Paraphrase Generation**
   - Generate paraphrases using T5
   - Control variants using temperature, top-p, and top-k
   - Categorize paraphrases into light, medium, and strong

3. **Semantic Filtering (NLI)**
   - Use NLI model (BART Large MNLI)
   - Filter paraphrases that do not preserve meaning
  
4. **Model Inference**
   - Evaluate multiple LLMs (e.g., LLaMA2_7B, Mistral_7B, Yi_6B)
   - Zero-Shot Inference
   - Extract predicted answers
  
5. **Evaluation**
   - Accuracy (Percentage of correct predictions compared to ground truth)
   - Consistency (Agreement between original and paraphrased predictions)
   - Weighted & Variance Prompt Sensitivity (Severity of changes & variability in model behaviour)
   - Failure Taxonomy (Stability of answers)
   - High-Risk Analysis (Categorization of model failures)
  
## Project Structure

```text
LLM-Paraphrase-Evaluation/
├── data/
│   ├── raw/
│   │   └── base_df.csv
│   ├── processed/
│   │   ├── filtered_df.csv
│   │   ├── paraphrase_df.csv
│   │   ├── eval_df_long.csv
│   │   └── eval_df_with_nli.csv
│
├── results/
│   ├── experiment_outputs/
│   │   ├── exp1_df.csv
│   │   ├── exp2_df.csv
│   │   ├── exp1_df_semantic.csv
│   │   ├── exp2_df_semantic.csv
│   │
│   ├── final_results/
│   │   ├── results_exp1.csv
│   │   ├── results_exp2.csv
│   │   ├── results_exp1_semantic.csv
│   │   ├── results_exp2_semantic.csv
│   │   ├── results_exp1_raw.csv
│   │   ├── results_exp2_raw.csv
│   │   ├── results_exp1_semantic_raw.csv
│   │   └── results_exp2_semantic_raw.csv
│
│   ├── summaries/
│   │   ├── summary_exp1.csv
│   │   ├── summary_exp2.csv
│   │   ├── summary_exp1_semantic.csv
│   │   ├── summary_exp2_semantic.csv
│   │   ├── wpsi_summary.csv
│   │
│   ├── taxonomy/
│   │   ├── taxonomy_by_level_summary.csv
│   │   ├── taxonomy_by_model_summary.csv
│   │   ├── taxonomy_model_level_majority_summary.csv
│   │   ├── taxonomy_model_level_variant_summary.csv
│   │   ├── taxonomy_per_level.csv
│   │   ├── taxonomy_per_variant.csv
│   │   └── taxonomy_summary.xlsx
│
│   └── nli/
│       └── nli_heatmap_values.csv
│
├── notebooks/
├── README.md
└── requirements.txt

```

## Dependencies

All required Python packages are listed in `requirements.txt`.

To install:

```bash
pip install -r requirements.txt
```

