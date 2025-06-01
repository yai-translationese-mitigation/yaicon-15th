# YAICON 15th 영한 번역투 완화 (그것팀되다)
This work was presented at the 15th YAICON and won the 1st Prize!

## 📌 Background

Korean sentences translated from English often exhibit syntactic and lexical features that are uncommon in native Korean writing. These unnatural patterns, referred to as *translationese*, can be observed, for example, in the frequent use of pronouns such as "그", "그녀", and formulaic phrases like "에 관하여", which are rarely found in naturally written Korean.

Translationese not only reduces the readability and linguistic naturalness of the text, but also distorts the evaluation of machine translation models. For instance, Artetxe et al. (2020a) demonstrated that test sets containing translationese can lead to overly optimistic performance scores, especially for cross-lingual models, thus misrepresenting their true effectiveness.

In this context, mitigating translationese in English–Korean translations is both a linguistically and technically significant challenge. The goal of our project is to design and implement a method to detect and reduce translationese using fine-tuned KE-T5 models.


