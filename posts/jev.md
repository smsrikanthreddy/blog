---
aliases:
- /markdown/2026/10/04/jev
categories:
- GenAI
date: '2026-10-04'
description: What is Jev AI 
image: /images/LLM/jev.png
layout: post
title: What is Jev AI
toc: true
---

#### What is Jev AI? 

Jev AI is a "System One" model from a company called TypeSafe AI, which is fundamentally different from LLMs (System Two). But wait, what do System 1 and System 2 mean here? Where do these terms come from, and what exactly does Jev mean in this context?

System 1 and System 2 are terms popularized by Nobel Laureate Daniel Kahneman in his book *Thinking, Fast and Slow*. System 1 is fast, automatic, intuitive, and emotional. System 2 is slow, deliberative, effortful, and logical. 

LLMs are autoregressive models, meaning they predict text token by token. They are designed to excel at chat and reasoning, and they are typically optimized using RLHF (Reinforcement Learning from Human Feedback) and RLVR (Reinforcement Learning with Verifiable Rewards).

In contrast, the Jev model is optimized using Reinforcement Learning for Calibrated Decisions (RLCD).

#### How to use Jev? 

Jev accepts text data as input, but its outputs are fixed. This is where it sharply diverges from LLMs. Because the output types are strictly constrained, Jev does not structurally hallucinate—unlike LLMs, regardless of the model. Jev is also incredibly fast, sometimes up to 400x faster than comparable LLMs, because all decisions can be evaluated in parallel.

##### Jev primarily outputs:

| Question type | Goal | Returns |
| --- | --- | --- |
| Choice | Choose an option from a list | choice, probabilities, confidence |
| Score | Score the state on a rubric | score, probabilities, confidence |
| Noul | Is this statement true? | noul (0–1) |

All three question types can be mixed into a single API call. Every question is evaluated in parallel and in isolation against the same state in one go. Adding questions barely changes the response time. Each question is evaluated independently, so adding more questions does not create context-rot.

#### What is RLCD (Reinforcement Learning for Calibrated Decisions)?

RLCD is a training paradigm that optimizes models directly for the kind of outputs we want, rather than for generating text. Instead of training the model to produce human-like text, RLCD trains it to produce reliable, calibrated outputs for specific decision-making tasks. When the Jev model produces an output, it also provides a confidence score that is trustworthy. Thanks to RLCD, Jev can make reliable decisions in real-time without the hallucinations that are common in LLMs. 

#### My take on Jev

The idea of developing a fundamentally different architecture for this specific type of problem is brilliant. Just as human beings rely on both System 1 and System 2 thinking, enterprise AI systems need both Jev and LLMs for different purposes. Jev is exceptionally fast and ideal when we need fixed, reliable outputs. However, when we actually need to generate text or reason through novel problems, LLMs remain the way to go.

I am actively exploring where to fit the Jev model into our company's product offerings. I am very bullish on Jev and am already testing several use cases. Check out the links below for more details on AI, GenAI, and Jev.

##### Srikanth's Blog: https://smsrikanthreddy.github.io/blog/
##### Jev Website: https://typesafe.ai