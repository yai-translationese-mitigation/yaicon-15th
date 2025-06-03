# YAICON 15th Korean-English Translationese Mitigation (Team Name: 그것팀되다)
This work was presented at the 15th YAICON.

## 👥 Team Members

| Name                | Degree & Major                                   | Role                                         |
|---------------------|--------------------------------------------------|----------------------------------------------|
| Hyun Gu Kang (강현구)     | B.A. German Language & Literature / B.Sc. Applied Statistics | Team Lead, KE-T5 Model, Preliminary Presentation |
| Min Gyu Kim (김민규)       | M.Sc. Statistics & Data Science             | Related Work, Final Presentation             |
| Kyeong Won Park (박경원)   | M.Sc. Artificial Intelligence               | mT5-small / mT5-base Model                |
| Hyun Bo Sim (심현보)       | B.Sc. Electrical & Electronic Engineering   | Dataset                 |
| Yumin Cheong (정유민)      | M.D. Candidate                              | Dataset, Evaluation Metrics                  |

## 📌 Background

Although recent advancements in large language models (LLMs) have significantly improved machine translation quality, translationese remains a persistent issue. Translationese refers to unnatural linguistic patterns that arise from the direct transfer of source-language structures or expressions into the target language. In English-to-Korean translation, this often results in awkward word order, overuse of pronouns (e.g., “그”, “그녀”), or overly formal constructions such as “~에 대하여”.

These artifacts not only reduce the readability and fluency of the translated text but also compromise the reliability of machine translation evaluation. For instance, Artetxe et al. (2020a) demonstrated that test sets containing translationese can lead to overly optimistic performance scores, thus misrepresenting the true effectiveness of cross-lingual models.

In this context, mitigating translationese in English–Korean translations presents both a linguistic and technical challenge. Hence, the goal of our project is to design and implement a method to detect and reduce translationese using fine-tuned encoder–decoder models.


## 🎯 Objectives

We aim to build a style transfer model that rewrites translationese Korean sentences into more natural Korean while preserving their original meaning.


## 📊 Dataset

Given the absence of parallel corpora for this task, we constructed a pseudo-parallel dataset based on the English–Korean parallel corpus from AI Hub, available at [traintogpb/aihub-koen-translation-integrated-base-1m](https://huggingface.co/datasets/traintogpb/aihub-koen-translation-integrated-base-1m).

To create translationese-style sentences, we applied back-translation and filtered the results using automatic metrics such as BERTScore to ensure semantic consistency. The resulting pseudo-parallel dataset contains approximately 500K sentence pairs, built through the following steps:

1. **Base Data**: English–Korean parallel sentences from AI Hub  
2. **Back-Translation**: Generation of translationese-style Korean using a fine-tuned NLLB model ([NLLB-en2ko](https://huggingface.co/NHNDQ/nllb-finetuned-en2ko))  
3. **Filtering**:
   - Retained sentence pairs with BERTScore (F1) ≥ 0.9 to ensure semantic preservation
   - Removed sentences containing non-Korean characters or noisy artifacts

The final dataset consists of pseudo-parallel sentence pairs that are suitable for supervised fine-tuning of style transfer models.

Each row in the CSV file includes:
- `ko_translationese`: Korean sentences generated via back-translation from English
- `ko`: Comparable native Korean sentences


## 🧠 Model and Training

We fine-tuned the following pretrained encoder–decoder models:

- [`KE-T5-base`](https://huggingface.co/KETI-AIR/ke-t5-base) – Korean-specific model
- [`mT5-small`](https://huggingface.co/google/mt5-small) and [`mT5-base`](https://huggingface.co/google/mt5-base) – multilingual T5 variants

Each model was trained using standard cross-entropy loss on the filtered pseudo-parallel dataset.


## 📈 Evaluation

To assess the effectiveness of translationese mitigation, we employed both quantitative and qualitative evaluation metrics.

### 🔢 Quantitative Metrics

- **BERTScore** (semantic preservation):  
  All models showed a drop in BERTScore compared to the original (0.87), with final scores of:
  - mT5-small: 0.75  
  - mT5-base: 0.83  
  - KE-T5-base: 0.81

- **Perplexity** (fluency of generated text):  
  Lower perplexity indicates more natural language.  
  - KE-T5-base: **1.36**  
  - mT5-small: 12.84  
  - mT5-base: 9.56

- **MATTR** (Moving Average Type-Token Ratio, measures lexical diversity):  
  All models showed slightly improved lexical variety.  
  - Original: 0.9941  
  - mT5-small: 0.9966  
  - mT5-base: 0.9960  
  - KE-T5-base: 0.9977

### 👀 Qualitative Analysis

- **Human Evaluation**:  
  - **KE-T5-base** generated the most fluent and natural Korean expressions, although it occasionally distorted meaning (e.g., incorrect pronoun references or changes in subject).
  - **mT5 models** produced more literal translations with fewer semantic deviations, but retained some of the rigid and unnatural expressions typical of translationese.


## ⚠️ Limitations

- **Data quality**: Even original AI-Hub translations often contained translationese, making clean ground truth difficult to obtain.
- **Model accuracy**: KE-T5 sometimes sacrificed meaning accuracy for fluency.
- **CE Loss limitation**: Cross-entropy loss alone may not sufficiently penalize stylistic artifacts.


## 🔮 Future Directions

- Explore **data augmentation** techniques to enrich stylistic diversity
- Introduce **additional losses** (e.g., classifier-guided loss, reconstruction loss, cycle loss) to improve style control

## 🙋 Acknowledgements

This project was presented at the 15th YAICON, a research contest held every semester by [YAI](https://y-ai.notion.site/), the AI academic society of Yonsei University.  
We thank all members of YAI for their valuable feedback and support.

## 📄 License

This project is licensed under the MIT License.
