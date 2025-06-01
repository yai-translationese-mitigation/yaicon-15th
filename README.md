# YAICON 15th Korean-English Translationese Mitigation (Team Name: 그것팀되다)
This work was presented at the 15th YAICON and won the 1st Prize!

## 👥 Team Members

| Name                | Degree & Major                                   | Role                                         |
|---------------------|--------------------------------------------------|----------------------------------------------|
| Hyun Gu Kang (강현구)     | B.A. German Language & Literature / B.Sc. Applied Statistics | Team Lead, KE-T5 Model, Preliminary Presentation |
| Min Gyu Kim (김민규)       | M.Sc. Statistics & Data Science             | Related Work, Final Presentation             |
| Kyeong Won Park (박경원)   | M.Sc. Artificial Intelligence               | mT5-small / mT5-base Modeling                |
| Hyun Bo Sim (심현보)       | B.Sc. Electrical & Electronic Engineering   | Dataset Collection & Curation                |
| Yumin Jeong (정유민)       | M.D. Candidate                              | Dataset, Evaluation Metrics                  |

## 📌 Background

Korean sentences translated from English often exhibit syntactic and lexical features that are uncommon in native Korean writing. These unnatural patterns, referred to as *translationese*, can be observed, for example, in the frequent use of pronouns such as "그", "그녀", and formulaic phrases like "에 관하여", which are rarely found in naturally written Korean.

Translationese not only reduces the readability and linguistic naturalness of the text, but also distorts the evaluation of machine translation models. For instance, Artetxe et al. (2020a) demonstrated that test sets containing translationese can lead to overly optimistic performance scores, especially for cross-lingual models, thus misrepresenting their true effectiveness.

In this context, mitigating translationese in English–Korean translations is both a linguistically and technically significant challenge. The goal of our project is to design and implement a method to detect and reduce translationese using fine-tuned KE-T5 models.

## 🎯 Objectives

This project aims to explore whether syntactic translationese in English–Korean parallel corpora can be detected and mitigated using transformer-based models. We hypothesize that fine-tuning a Korean-specific T5 model on filtered data can reduce translationese features and improve both fluency and evaluation fairness.


## 📊 Dataset

The dataset consists of Korean sentences that were either directly written in Korean or translated from English. We manually filtered and labeled examples with signs of translationese (e.g., unnatural word order, redundant pronouns). The CSV file includes the following columns:

- `ko_translationese`: Korean sentences translated from English
- `ko`: Comparable native Korean sentences


## 🧠 Model and Training

We use the [`KE-T5-base`](https://huggingface.co/KETI-AIR/ke-t5-base) model, which is a Korean-specific encoder–decoder transformer.  
The model was fine-tuned using a sequence-to-sequence objective to rewrite translationese-style Korean sentences into more natural forms.

Training was conducted using:
- Batch size: 16
- Learning rate: 3e-4
- Epochs: 3


## 📈 Evaluation

To evaluate the effectiveness of translationese mitigation, we used both automatic metrics and qualitative analysis.  
We observed that the fine-tuned KE-T5 model was able to reduce the frequency of unnatural pronouns and rigid expressions.

| Metric        | Before | After |
|---------------|--------|-------|
| BLEU Score    | 21.4   | 24.7  |
| Pronoun Usage | High   | Reduced |


## 📄 License

This project is licensed under the MIT License.
