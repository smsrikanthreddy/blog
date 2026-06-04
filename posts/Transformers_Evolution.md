---
aliases:
- /markdown/2026/06/04/Transformers_Evolution
categories:
- GenAI
date: '2026-06-04'
description: Transformers Evolution
image: /images/LLM/logo.png
layout: post
title: Transformers Evolution
toc: true

---

### Transformer Evolution

In this post we'll see evolution of transformers, these include encoder-only, encoder-decoder, and decoder-only transfomers architectures. We start with GPT-1 and BERT and end with Google latest family of Gemini models.

#### Encoder-only Transformers

BERT (2018-Google):- 

*Bidirectional Encoder Representations from Transformers (BERT)* was developed by Google in 2018. It is an encoder-only transformer architecture which was trained on a large corpus of unlabeled data such as the BooksCorpus and Wikipedia. 
* Main innovations are :-
    - Instead of translating or producing sequences, BERT focuses on understanding context deeply by training on a masked language model objective. In this setup, random words in a sentence are replaced with a [MASK] token, and BERT tries to predict the original word based on the surrounding context.
    - Another innovative aspect of BERT’s training regime is the next sentence prediction loss, where it learns to determine whether a given sentence logically follows a preceding one. By training on these objectives, BERT captures intricate context dependencies from both the left and right of a word, and it can discern the relationship between pairs of sentences.
    - Such capabilities make BERT especially good at tasks that require natural language understanding, such as question- answering, sentiment analysis, and natural language inference, among others. Since this is an encoder-only model, BERT cannot generate text.    


#### Decoder-only Transformers

GPT-1 (2018-OpenAI):- 

* Generative pre-trained transformer 1(GPT) was developed by OpenAI in 2018. It is a decoder-only transformer architecture which was trained on a the BooksCorpus dataset (5GB - ~7B words). 
* It is able to generate text, tranlate languages, answer questions in an informative way.
* Main innovations in GPT-1 are: 
  - Combining transformers and unsupervised pre-training: Unsupervised pre-training is a process of training a language model on a large corpus of unlabeled data. Then, supervised data is used to fine-tune the model for a specific task, such as translation or sentiment classification. 
  - Task-aware input transformations: There are different kinds of tasks such as textual entailment and question-answering that require a specific structure. For example, textual entailment requires a premise and a hypothesis; question-answering requires a context document; a question and possible answers. One of the contributions of GPT-1 is converting these types of tasks which require structured inputs into an input that the language model can parse, without requiring task-specific architectures on top of the pre-trained architecture.
* Main drawbacks are :- 
  - the model was prone to generating repetitive text, especially when given prompts outside the scope of its training data. 
  - It also failed to reason over multiple turns of dialogue and could not track long-term dependencies in text. 
  - Additionally, its cohesion and fluency were limited to shorter text sequences, and longer passages would lack cohesion.


GPT-2(2019-OpenAI) :- 

* GPT-2 main innvovation was a direct scale-up, with tenfold increase in both its parameter count and the size of training dataset
- Data :- Trained on a large (40GB) and diverse dataset called WebText, which consists of 45M webpages from Reddit with a karma rating of atleast three. Karma 3 means - reasonable level of quality.
- Parameters :- 1.5 Billion parameters, which was an order of magnitude larger than the previous model. More parameters increases the model learning capacity and improves its ability to capture complex patterns in the training data
* The authors trained 4 models with 117M (same as GPT-1), 345M, 762M and 1.5B parameters and found that the model with the most paramerters performed better on every subsequent task.
* Scaling up resulted in a model that was able to generate more coherent and realistic text then GPT-1. It demonstrated significant improvement in capturing long range dependencies and common sense reasoning. 
* Despite larger model, it did not perform well in some tasks like reading comprehension, summarization and translation
* its significant achivement is its ability to perform zero-shot learning on a variety of tasks. Zero-shot task transfer is the ability of a model to generalize to a new task without being trained on it, which requires the model to understand the task based on the given instruction.
* GPT-2 was able to perform tasks such as machine translation, text summarization, and reading comprehension without any explicit supervision.

GPT-3/3.5/4 (2020/2022/2023-OpenAI) :- 



#### Encoder-Decoder Transformers