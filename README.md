# Project Title:  
**Distinguishing Human vs. LLM-Generated Shakespearean Sonnets**

## Project Overview  
This project investigates how machine-generated sonnets differ from original Shakespearean sonnets in terms of structure, style, semantics, and attention patterns. Using a classification approach, we aim to reveal key linguistic and literary features that differentiate human creativity from algorithmic imitation.

## Dataset

| Source                 | Count | Label |
|------------------------|-------|-------|
| Shakespearean Sonnets | 149   | 0     |
| LLM-Generated Sonnets | 145   | 1     |
| **Total**              | 294   |       |

- **LLM Model**: `mistralai/Mistral-7B-Instruct-v0.1`
- **Shakespeare data**: [Project Gutenberg #1041](https://www.gutenberg.org/ebooks/1041)
- **Generation method**: Few-shot prompting with Shakespearean structure

## Preprocessing Strategy

Three levels of data:
1. **Original Text**: Raw text including all stopwords and pronouns
2. **Processed A**: Removed stopwords + personal pronouns
3. **Processed B**: Further removed Renaissance-specific expressions (e.g., *thee*, *thou*)

## Surface-Level Analysis

| Metric               | Human | LLM   |
|----------------------|-------|-------|
| Lexical Diversity    | ↑     | ↑     |
| Syntactic Diversity  | ↑     | ↑     |
| Entropy              | ↑     | ↑     |

Key findings:
- LLMs used more thematic vocabulary like *"fleeting," "mortal,"* while humans used personal references.
- LLMs showed more lexical variety but lower syntactic diversity in raw form.

## Classification Model

- **Model**: `bert-base-uncased`
- **Training Size**: 80% of 294 sonnets
- **Evaluation Metric**: F1 Score
- **Tokenizer**: Fixed-length input, FP16 precision

### Results
- **Accuracy/F1**: 100% across all datasets
- **Observation**: Preprocessing slightly increased training loss but didn't degrade performance.

## t-SNE Embedding Visualization

- **t-SNE Analysis** conducted for:
  - Original Data
  - Processed A
  - Processed B
- Best separation seen in **Processed B**, especially at **layer 11**

### Layer-wise Observations

| Layer Group  | Role                                 | Observation |
|--------------|--------------------------------------|-------------|
| Layers 1–4   | Lexical/Surface Features             | Mixed       |
| Layers 5–8   | Semantic Coherence                   | Partial sep.|
| Layers 9–12  | Stylistic Abstractions               | Full sep.   |

## Attention Entropy

- **Human Poems**: Focused, low entropy
- **LLM Poems**: Diffuse, high entropy
- **With preprocessing**: Distinctions become clearer
- **Layer 11**: Optimal for classification difference

## Zero-Shot Classification

| Class      | Precision | Recall | F1 Score |
|------------|-----------|--------|----------|
| **Human**  | 0.50 → 0.50 | 1.00 → 0.95 | 0.67 → 0.65 |
| **LLM**    | 0.00 → 0.36 | 0.00 → 0.03 | 0.00 → 0.05 |

- Model: `facebook/bart-large-mnli`
- Preprocessing improved LLM detection but overall LLM recall remained low

## Key Takeaways

1. **Structure Helps, But Isn't Enough**: Even structurally similar LLM poems are distinguishable via deeper features.
2. **Optimal Layer**: Layer 11 shows maximum human vs. LLM separation.
3. **Attention Insight**: Humans focus; LLMs diffuse attention.
4. **Zero-shot Limitation**: Bias toward "Human" unless surface clues are removed.

##  Practical Implications

- **For Classification**: Use BERT embeddings from layers 8–10
- **For Analysis**: Use middle layers (5–8) for stylistic insight
- **Preprocessing Tip**: Avoid over-cleaning; remove noise, not signal

##  Limitations

- Small dataset (294 sonnets)
- Focused on English + Shakespearean genre
- Results may not generalize to modern or non-English poetry

## Future Directions

- Incorporate modern and multilingual poetic corpora
- Examine ethical and interpretability concerns in AI poetry classification
- Explore other architectures (e.g., LLaMA2, GPT-NeoX)

## 🔗 Useful Links

-  [Full Report Website](https://kang88kang88.wixsite.com/dh205kjy)
-  [Processing Code](https://kang88kang88.wixsite.com/dh205kjy/processing-code)
-  [Model & t-SNE Visuals](https://kang88kang88.wixsite.com/dh205kjy/enbedding)
-  [Zero-shot Analysis](https://kang88kang88.wixsite.com/dh205kjy/zreoshot)
output_path.write_text(readme_content.strip(), encoding="utf-8")
output_path.name
