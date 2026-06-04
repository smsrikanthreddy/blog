---
aliases:
- /markdown/2026/04/23/Foundational_LLMs
categories:
- GenAI
date: '2026-04-23'
description: Foundational LLMs
image: /images/LLM/logo.png
layout: post
title: Gen AI Foundational Information
toc: true

---

### Gen AI Foundational Information

#### Introduction 
The advent of Large Language Models (LLMs) represent a sesimic shift in the field of Artificial Intelligence. 
Their ability to process, generate and understand user intent is fundamentally changing the way we interact with information and technology. 

An LLM is an advanced artificial intelligence system that specializes in processing,understanding, and generating human-like text. These systems are typically implemented as
a deep neural network and are trained on massive amounts of text data. This allows them to learn the intricate patterns of language, giving them the ability to perform a variety of tasks,
like machine translation, creative text generation, question answering, text summarization, and many more reasoning and language oriented tasks.

#### Why language models are important
- LLMs achieve an impressive performance boost from the previous state of the art NLP models across a variety of different and complex tasks which require answering questions or complex reasoning, making feasible many new applications.
  These include language translation, text summarization, text generation, question answering, code generation, sentiment analysis, etc.
- Although foundational LLMs trained in a variety of tasks on large amounts of data, perform very well out of the box and display emergent behaviours (e.g. the ability to perform tasks they have not been directly trained for) they can
  also be adapted to solve specific tasks where performance out of the box is not at the level desired through a process known as fine-tuning. This requires significantly less data and 
  computational resources than training an LLM from scratch. 
- LLMs can be further nudged and guided towards the desired behavior by the discipline of prompt engineering: the art and
 science of composing the prompt and the parameters of an LLM to get the desired response.

#### A brief history of LLMs
 - A language model predicts the probability of a sequence of words.Commonly, when given a prefix of text, a language model assigns probabilities to subsequent words. For instance, given the prefix "the cat sat on the", a language model might assign the highest probability to the word "mat" followed by "floor", "sofa", etc. and low probability to words like "ceiling", "car", etc. 
- Early language models were based on n-gram models, which are probabilistic models that use the previous n words to predict the next word. 
- Before the invention of transformers, Recurrent Neural Networks(RNNs) were the state of the art for language modeling tasks. In particular "Long short term memory (LSTM)" and "Gated Recurrent Unit (GRU)" were common architectures. 
- RNNs process text sequentially, word by word. This has a few major drawbacks. 
  - sequentially processing words is computationally inefficient. This is because they can't be parallelized
  - They suffer from vanishing/exploding gradients over long sequences. This makes it difficult for them to capture long range dependencies in text. 
    (e.g., the model might "forget" information from the beginning of a long paragraph)
- Transformers, on the other hand, are a type of neural network that can process sequences of tokens in parallel thanks to the self-attention mechanism. This makes them computationally efficient and allows them to capture long range dependencies in text.

### The Transformers

The transformer architecture was developed at Google in 2017 for use in a translation model . It’s a sequence-to-sequence model capable of converting sequences from one domain into sequences in another domain. For example, translating French sentences to English sentences. The original transformer architecture consists of two parts: an encoder and a decoder. The encoder converts the input text (e.g., a French sentence) into a representation, which is then passed to the decoder. The decoder uses this representation to generate the output text (e.g., an English translation) autoregressively . Notably, the size of the output of the transformer encoder is linear in the size of its input. Figure 1 shows the design of the original transformer architecture.

The transformer consists of multiple layers. A layer in a neural network comprises a set of
parameters that perform a specific transformation on the data. In the diagram you can see
an example of some layers which include Multi-Head Attention, Add & Norm, Feed-Forward,
Linear, Softmax etc. The layers can be sub-divided into the input, hidden and output layers.
The input layer (e.g., Input/Output Embedding) is the layer where the raw data enters the
network. Input embeddings are used to represent the input tokens to the model. Output
embeddings are used to represent the output tokens that the model predicts. For example, in
a machine translation model, the input embeddings would represent the words in the source
language, while the output embeddings would represent the words in the target language.
The output layer (e.g., Softmax) is the final layer that produces the output of the network. The
hidden layers (e.g., Multi-Head Attention) are between the input and output layers and are
where the magic happens!.


![Transformer Architecture](images/LLM/transformer.png)