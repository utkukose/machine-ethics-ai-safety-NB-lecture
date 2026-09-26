<div align="center">

# Week 12: Security of LLM Applications: Prompt Injection, Jailbreaks and Data Extraction

**Machine Ethics and Artificial Intelligence Safety (11118BLG001)**  
Prof. Dr. Utku Kose, Süleyman Demirel University

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/weeks/week-12/NB12_llm_security.ipynb) [![Interactive lab](https://img.shields.io/badge/interactive%20lab-open-1D5B78)](https://utkukose.github.io/machine-ethics-ai-safety-NB-lecture/weeks/week-12/lab.html) [![Lecture notes](https://img.shields.io/badge/lecture%20notes-Word-566A73)](Week12_Lecture_Notes.docx) [![Course home](https://img.shields.io/badge/course-home-B97813)](../../README.md)

</div>

## Overview

Language models are now embedded in applications that read e-mail, browse the web and call tools. This week examines the resulting attack surface, from direct and indirect prompt injection to jailbreaks and training data extraction, and the layered defences and red teaming practices that reduce the risk [1, 2, 3].

**Estimated study time:** 6 to 8 hours.

## Learning outcomes

By the end of the week, students are expected to explain why prompt injection follows from mixing instructions and data in one context, to distinguish direct from indirect injection, to describe the two failure modes of safety training identified for jailbreaks, to explain training data extraction and membership inference, and to design and evaluate layered defences for an LLM-integrated application.

## Study path

| Step | Activity | Suggested time |
|---|---|---|
| 1 | Read the lecture below or the [Word version](Week12_Lecture_Notes.docx) | 90 minutes |
| 2 | Explore the [interactive lab](https://utkukose.github.io/machine-ethics-ai-safety-NB-lecture/weeks/week-12/lab.html) | 45 minutes |
| 3 | Work through the [Colab notebook](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/weeks/week-12/NB12_llm_security.ipynb) and its exercises | 2 to 3 hours |
| 4 | Take the self-assessment in the lab (tab: Check yourself) | 20 minutes |
| 5 | Write the reflection, export the learning log and complete the weekly task | 60 minutes |

## Week at a glance

```mermaid
flowchart LR
  U["User input"] --> C["Context window: instructions and data mixed"]
  R["Retrieved content"] --> C
  C --> M["Language model"]
  M --> T["Tool calls"]
  M --> O["Rendered output"]
  A1["Direct injection"] -.-> U
  A2["Indirect injection"] -.-> R
  D["Layers: separation, instruction priority, least privilege, confirmation, output checks, red teaming"] --> M
```

## Lecture

### An attack surface made of text

An LLM-integrated application assembles a context from several sources: the developer's system prompt, the user's request and external content such as web pages, e-mails, documents and tool outputs. The model receives all of this as one sequence of tokens and has no reliable way to tell instructions from data. Perez and Ribeiro showed that simple handcrafted inputs could hijack the goal of a model or make it leak its hidden prompt, which they called goal hijacking and prompt leaking [4]. Greshake and colleagues went further with indirect prompt injection: An attacker plants instructions in content that an application is likely to retrieve, and the model follows them without any action by the user [1]. They demonstrated data theft and the manipulation of answers in real applications.

The OWASP Top 10 for LLM Applications, version 2025, lists prompt injection as the first risk, followed by sensitive information disclosure, supply chain, data and model poisoning, improper output handling, excessive agency, system prompt leakage, vector and embedding weaknesses, misinformation and unbounded consumption [2]. Figure 12.1 marks where several of these risks enter an application. Kose, Cankaya and Deperlioglu anticipated a future in which AI systems are both weapons and targets in cyber conflict [5], and LLM applications with access to tools make that anticipation concrete.

![The attack surface of an LLM-integrated application. Numbered labels mark where direct and indirect injection, excessive agency, improper output handling and system prompt leakage enter {cite:greshake2023,owasp2025}.](figures/w12_fig1.png)

*Figure 12.1. The attack surface of an LLM-integrated application. Numbered labels mark where direct and indirect injection, excessive agency, improper output handling and system prompt leakage enter [1, 2].*

<details>
<summary><b>Check your understanding.</b> What is indirect prompt injection?</summary>

A. Instructions hidden in content the model retrieves, such as a web page or an e-mail, hijack its behaviour  
B. A user types a harmful request  
C. A bug in the tokenizer  
D. A denial-of-service attack  

**Answer: A.** The attacker never talks to the model directly. The data channel becomes an instruction channel.

</details>

### Jailbreaks and automated attacks

A jailbreak is an input that makes a model produce content its safety training was meant to prevent. Wei, Haghtalab and Steinhardt explained why safety training fails with two failure modes [6]. Competing objectives arise when a model's capabilities and its safety goals conflict, for example when a prompt demands a particular response format that leaves no room for refusal. Mismatched generalisation arises when safety training does not cover a domain in which the model is capable, for example instructions written in an encoding or a language that received little safety training. Attacks that combined both failure modes succeeded against the strongest models they tested.

Zou and colleagues automated the search: A gradient-guided optimisation found adversarial suffixes that caused open-weight models to comply with harmful requests, and the same suffixes transferred to closed commercial models [7]. The result links language model security to the adversarial examples of Week 8. Robustness cannot rest on the hope that attackers will not find the right input.

<details>
<summary><b>Check your understanding.</b> What did automated searches for adversarial suffixes show?</summary>

A. Aligned models cannot be attacked  
B. Optimised token strings can make aligned models comply, and some transfer across models  
C. Only human-written jailbreaks work  
D. Suffixes only affect image models  

**Answer: B.** Transfer means that attacks developed on open models can threaten closed ones.

</details>

### Privacy and data extraction

Models can reveal what they were trained on. Carlini and colleagues extracted hundreds of verbatim sequences from the training data of GPT-2 by generating many samples and ranking them with membership signals, and the extracted text included personal names, phone numbers and e-mail addresses [8]. They also found that larger models memorised more. Shokri and colleagues introduced membership inference attacks, which decide whether a given record was part of a model's training set by training shadow models that imitate the target's behaviour [9]. Both attacks matter whenever a model is trained or fine-tuned on sensitive data, such as clinical notes or private correspondence.

<details>
<summary><b>Check your understanding.</b> What do training data extraction attacks show?</summary>

A. Models never memorise  
B. Extraction requires the model weights  
C. Models can emit memorised sequences, including personal data, when prompted suitably  
D. Only small models leak data  

**Answer: C.** Memorisation creates privacy risks, especially for rare or duplicated sequences.

</details>

### Defence in depth and red teaming

No single defence stops prompt injection reliably, so practice relies on layers. Untrusted content can be marked and separated from instructions. Models can be trained to give priority to the instructions of the developer over those found in data. Tools can follow the principle of least privilege, so that an assistant that summarises e-mail cannot send it. Consequential actions can require human confirmation, and model output can be treated as untrusted input to downstream systems, for example by rendering links only from allowed domains [2]. Detectors for injected instructions help, but they generalise poorly to paraphrases and to other languages, as the notebook shows.

Red teaming searches for failures before attackers do. Perez and colleagues used one language model to generate test cases for another and found many harmful behaviours at a scale that manual testing could not reach [3]. Ganguli and colleagues released a large data set of human red-team attacks and reported that models trained with reinforcement learning from human feedback became harder to red-team as they grew, whereas other model types did not show this trend [10].

> **Pause and reflect.** An assistant reads a university inbox and can send e-mail. Which single design change would remove the largest share of the injection risk, and what would it cost the users?

<details>
<summary><b>Check your understanding.</b> What does defence in depth mean?</summary>

A. Relying on one very strong filter  
B. Training for longer  
C. Keeping the system prompt secret  
D. Combining several independent safeguards so that one failure does not compromise the system  

**Answer: D.** No single defence against prompt injection is reliable, so layers are combined.

</details>

## Interactive lab

A scripted toy assistant, not a real language model, summarises e-mails. Some e-mails contain injected instructions. Switch defensive layers on and off to see which attacks still succeed, which legitimate e-mails are wrongly blocked and what each layer costs [1, 2, 6].

[Open the interactive lab](https://utkukose.github.io/machine-ethics-ai-safety-NB-lecture/weeks/week-12/lab.html)

![Screenshot of the Week 12 interactive lab](screenshots/lab.png)

## Colab notebook

The notebook rebuilds the toy assistant in Python, evaluates all 64 combinations of six defensive layers and trains a small detector for injected instructions, whose performance is then tested on paraphrased and Turkish attacks [1, 2].

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/weeks/week-12/NB12_llm_security.ipynb)

Screenshots of the executed notebook:

![Output 1 of the Week 12 notebook](screenshots/nb_1.png)

## Self-assessment and reflection

The lab contains a 6-question self-assessment with instant feedback and a confidence rating for each answer. A confident but wrong answer marks the first topic to revisit. The reflection prompts below are also available in the lab, where answers are saved in the browser and can be exported as a learning log.

1. Map an LLM application you use or build to Figure 12.1. Which entry point is the least protected?
2. Why did the detector fail on Turkish injections? What does that imply for systems deployed in multilingual settings?
3. What is the difference between red teaming and a penetration test of ordinary software? Name one similarity and one difference.

## Weekly task and submission

Write a threat model and defence plan of about 500 words for an LLM application in your field that reads external content and can call at least one tool. Map the risks to the OWASP 2025 list, propose at least four defensive layers with their costs and describe a red-teaming procedure. Attach the notebook with both exercises completed.

The weekly task supports self-learning and builds a personal portfolio. When the course is followed with the instructor during an active semester, the task can be sent together with the exported learning log to utkukose@sdu.edu.tr or utkukose@gmail.com for evaluation.

## Research and report assignment (optional)

**Indirect prompt injection in agentic systems.** Review attacks and defences for indirect prompt injection since 2023 and map them to the OWASP Top 10 for large language model applications [1, 2]. Assess which defences have been evaluated rigorously.

This research assignment is optional and supports self-learning. When the related weeks are followed within the course during an active semester, the report can be sent to utkukose@sdu.edu.tr or utkukose@gmail.com for evaluation. Unless the assignment states otherwise, a report has 1500 to 2500 words, follows the structure of an academic paper, cites at least six scholarly or official sources in square brackets and ends with a reference list.

## References

[1] Greshake, K., Abdelnabi, S., Mishra, S., Endres, C., Holz, T., & Fritz, M. (2023). Not what you've signed up for: Compromising real-world LLM-integrated applications with indirect prompt injection. In *Proceedings of the 16th ACM Workshop on Artificial Intelligence and Security (AISec '23)* (pp. 79-90). ACM. <https://arxiv.org/abs/2302.12173>

[2] OWASP GenAI Security Project (2024). *OWASP Top 10 for LLM Applications 2025 (version 2025, released 18 November 2024)*. OWASP Foundation. <https://genai.owasp.org/>

[3] Perez, E., Huang, S., Song, F., Cai, T., Ring, R., Aslanides, J., Glaese, A., McAleese, N., & Irving, G. (2022). Red teaming language models with language models. In *Proceedings of the 2022 Conference on Empirical Methods in Natural Language Processing* (pp. 3419-3448). Association for Computational Linguistics. <https://arxiv.org/abs/2202.03286>

[4] Perez, F., & Ribeiro, I. (2022). Ignore previous prompt: Attack techniques for language models. arXiv preprint arXiv:2211.09527. <https://arxiv.org/abs/2211.09527>

[5] Kose, U., Cankaya, S. F., & Deperlioglu, O. (2017). Cyber wars under the shadow of artificial intelligence: A future perspective. *International Journal of Engineering Science and Application*, 2(2), 71-76.

[6] Wei, A., Haghtalab, N., & Steinhardt, J. (2023). Jailbroken: How does LLM safety training fail?. In *Advances in Neural Information Processing Systems 36*. <https://arxiv.org/abs/2307.02483>

[7] Zou, A., Wang, Z., Carlini, N., Nasr, M., Kolter, J. Z., & Fredrikson, M. (2023). Universal and transferable adversarial attacks on aligned language models. arXiv preprint arXiv:2307.15043. <https://arxiv.org/abs/2307.15043>

[8] Carlini, N., Tramèr, F., Wallace, E., et al. (2021). Extracting training data from large language models. In *30th USENIX Security Symposium* (pp. 2633-2650).

[9] Shokri, R., Stronati, M., Song, C., & Shmatikov, V. (2017). Membership inference attacks against machine learning models. In *2017 IEEE Symposium on Security and Privacy (SP)* (pp. 3-18). IEEE. <https://doi.org/10.1109/SP.2017.41>

[10] Ganguli, D., Lovitt, L., Kernion, J., et al. (2022). Red teaming language models to reduce harms: Methods, scaling behaviors, and lessons learned. arXiv preprint arXiv:2209.07858. <https://arxiv.org/abs/2209.07858>

---

<sub>Machine Ethics and Artificial Intelligence Safety. Prof. Dr. Utku Kose, Süleyman Demirel University. ORCID [0000-0002-9652-6415](https://orcid.org/0000-0002-9652-6415). Content licensed under CC BY 4.0. This course is updated in line with current developments in the field. Last update: September 2026.</sub>
