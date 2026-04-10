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
   - Accuracy
   - Consistency
   - Weighted & Variance Prompt Sensitivity
   - Failure Taxonomy
   - High-Risk Analysis
