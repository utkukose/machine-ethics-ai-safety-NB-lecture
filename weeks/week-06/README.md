<div align="center">

# Week 06: Algorithmic Fairness II: Mitigation and Representational Harms

**Machine Ethics and Artificial Intelligence Safety (11118BLG001)**  
Prof. Dr. Utku Kose, Süleyman Demirel University

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/weeks/week-06/NB06_fairness_mitigation.ipynb) [![Interactive lab](https://img.shields.io/badge/interactive%20lab-open-1D5B78)](https://utkukose.github.io/machine-ethics-ai-safety-NB-lecture/weeks/week-06/lab.html) [![Lecture notes](https://img.shields.io/badge/lecture%20notes-PDF-566A73)](Week06_Lecture_Notes.pdf) [![Course home](https://img.shields.io/badge/course-home-B97813)](../../README.md)

</div>

## Overview

Measuring unfairness is the first step. This week covers interventions before, during and after training, the limits of removing protected attributes, counterfactual reasoning about fairness and the representational harms that language technologies can cause [1, 2, 3, 4].

**Estimated study time:** 6 to 8 hours.

## Learning outcomes

By the end of the week, students are expected to apply reweighing and group-specific thresholds and to explain the reductions approach to fair classification. They should be able to show why fairness through unawareness fails in the presence of proxies and to describe counterfactual fairness. Finally, they should be able to analyse gender bias in word embeddings and the limits of debiasing.

## Study path

| Step | Activity | Suggested time |
|---|---|---|
| 1 | Read the lecture below or the [PDF version](Week06_Lecture_Notes.pdf) | 90 minutes |
| 2 | Explore the [interactive lab](https://utkukose.github.io/machine-ethics-ai-safety-NB-lecture/weeks/week-06/lab.html) | 45 minutes |
| 3 | Work through the [Colab notebook](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/weeks/week-06/NB06_fairness_mitigation.ipynb) and its exercises | 2 to 3 hours |
| 4 | Take the self-assessment in the interactive lab (tab: Check yourself) | 20 minutes |
| 5 | Answer the reflection prompts in the interactive lab, export the learning log and complete the weekly task | 60 minutes |

## Week at a glance

```mermaid
flowchart LR
  PRE["Pre-processing: reweighing"] --> M["Model"]
  IN["In-processing: reductions under constraints"] --> M
  M --> POST["Post-processing: group thresholds"]
  U["Deleting the protected attribute"] -. "fails through proxies" .-> M
  CF["Counterfactual fairness: causal model"] --> M
  E["Embeddings: analogies and association tests"] --> RH["Representational harms"]
  RH --> DB["Debiasing hides more than it removes"]
```

## Lecture

### Three points of intervention

Mitigation methods act on the data, on the learning algorithm or on the predictions. Kamiran and Calders proposed pre-processing techniques, including reweighing [1]. Each training example receives the weight P(group) P(label) / P(group, label). In the weighted data, group and label are then statistically independent. Pre-processing is simple and model-agnostic, but it cannot guarantee a particular fairness criterion at test time.

In-processing changes the objective. Agarwal and colleagues reduced fair classification under constraints such as demographic parity or equalized odds to a sequence of cost-sensitive classification problems. The solutions are combined into a randomised classifier with provable guarantees [2]. Post-processing changes only the decision rule. Hardt, Price and Srebro showed how to derive group-specific, possibly randomised thresholds that achieve equalized odds or equal opportunity from any score, without retraining [3]. The open-source Fairlearn toolkit implements assessment tools and several of these mitigation methods [5]. Figure 6.1 compares the three routes on the lending data of Week 5.

![Accuracy against the equal opportunity gap on the synthetic lending data of Week 5 for a threshold sweep without mitigation, with reweighing and with group-specific thresholds.](figures/w06_fig1.png)

*Figure 6.1. Accuracy against the equal opportunity gap on the synthetic lending data of Week 5 for a threshold sweep without mitigation, with reweighing and with group-specific thresholds [1, 3].*

<details>
<summary><b>Check your understanding.</b> Reweighing training examples is an example of which kind of intervention?</summary>

A. In-processing  
B. Post-processing  
C. Pre-processing  
D. Auditing  

**Answer: C.** Reweighing changes the training data before learning, so it is a pre-processing method.

</details>

### Proxies and counterfactual fairness

A tempting remedy is to delete the protected attribute. This fairness through unawareness usually fails, because other features act as proxies: Postal codes, schools, names and purchase histories can encode group membership. The Colab notebook of Week 3 showed the same effect for a morally irrelevant attribute. The Colab notebook of Week 5 showed unequal error rates for a model that never saw the group.

Kusner and colleagues defined counterfactual fairness with a causal model [6]. A prediction is counterfactually fair if it would stay the same in a world where the individual's protected attribute had been different. Everything not caused by the attribute is held fixed in that comparison. The definition captures the intuition behind many discrimination complaints. Its price is a causal model of how the protected attribute influences the other features, and conclusions depend on assumptions that must be defended.

<details>
<summary><b>Check your understanding.</b> Why does removing the protected attribute from the inputs often fail?</summary>

A. Other features act as proxies for it  
B. Models cannot be trained without it  
C. It always increases accuracy  
D. Laws forbid removing it  

**Answer: A.** Correlated features such as a postcode can carry the same information.

</details>

### Representational harms in language technology

Fairness is not only about decisions. Bolukbasi and colleagues showed that word embeddings trained on news text completed analogies such as man is to computer programmer as woman is to homemaker. They proposed hard debiasing: Identify a gender direction and remove it from words that should be gender-neutral [4]. Caliskan, Bryson and Narayanan adapted the implicit association test to embeddings and reproduced a range of documented human biases in their word embedding association test [7].

Debiasing turned out to be shallow. Gonen and Goldberg showed that, after projection, words that had been stereotypically gendered still clustered together. A classifier could also recover the removed bias from the remaining dimensions [8]. Bender and colleagues warned that ever larger language models absorb the viewpoints over-represented in their training data and called for careful curation and documentation [9]. The interactive lab reproduces both the analogy effect and the residual bias in a two-dimensional toy space.

<details>
<summary><b>Check your understanding.</b> Which is an example of a representational harm?</summary>

A. A loan application is denied  
B. A server outage delays decisions  
C. A model responds slowly  
D. A translation system assigns stereotyped genders to occupations  

**Answer: D.** Representational harms concern how groups are depicted, for example through stereotypes or erasure.

</details>

### Choosing and documenting a mitigation

No mitigation is free. Each method moves the operating point of a system. The right point depends on the costs of errors for each group and on legal constraints, such as rules on using protected attributes at decision time. A defensible process names the criterion and explains why it fits the decision. It reports the trade-off between accuracy and fairness together with its uncertainty. It records the choice in documentation such as a model card, which Week 14 covers [10].

> **Pause and reflect.** Group-specific thresholds equalise true positive rates but treat identical scores differently. Is that fair? Consider the argument from the perspective of an applicant in each group.

<details>
<summary><b>Check your understanding.</b> How do documentation practices such as model cards support mitigation?</summary>

A. They hide the model weights  
B. They record intended use, evaluation across groups and known limitations  
C. They replace evaluation  
D. They guarantee fairness  

**Answer: B.** Documentation makes choices and limitations visible to users, auditors and affected people.

</details>

## Interactive lab

Eight occupation words and four gendered words live in a two-dimensional toy space, which is illustrative rather than trained. Neutralise the gender direction step by step, watch the analogy test change, and check whether the stereotype can still be recovered from the remaining dimension [4, 8].

[Open the interactive lab](https://utkukose.github.io/machine-ethics-ai-safety-NB-lecture/weeks/week-06/lab.html)

![Screenshot of the Week 6 interactive lab](screenshots/lab.png)

## Colab notebook

The Colab notebook applies reweighing and group-specific thresholds to the lending data of Week 5 and compares their fairness and accuracy. It also shows how to run the same assessment with Fairlearn when it is installed [1, 3, 5].

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/weeks/week-06/NB06_fairness_mitigation.ipynb)

Screenshots of the executed Colab notebook:

![Output 1 of the Week 6 Colab notebook](screenshots/nb_1.png)

## Self-assessment and reflection

The interactive lab contains a self-assessment of six questions (tab: Check yourself). Students answer each question, state how sure they are and receive instant feedback. A confident but wrong answer marks the first topic to revisit. The reflection prompts below also appear in the interactive lab (tab: Reflect and submit). Answers written there are saved in the browser and can be exported as a learning log.

1. Which of the three mitigation routes would be legally and practically feasible in your country for credit decisions, and why?
2. In the interactive lab, the analogy test changed before the residual bias disappeared. What does that suggest about using a single bias metric?
3. Describe a representational harm that a language model could cause in Turkish or another language you use, and how you would test for it.

## Weekly task and submission

**What to do.** Apply one mitigation method of this week to one model. The lending model of the Colab notebook is acceptable. First, report accuracy and at least two fairness metrics before and after the mitigation. Second, explain who gains and who loses from the change, in terms of the errors that each group experiences. Third, state whether you would deploy the method and what you would record in its documentation.

**Where to look.** Lecture: sections "Three points of intervention" and "Choosing and documenting a mitigation". Colab notebook: Section 2 for reweighing, Section 3 for group-specific thresholds and Section 4, which repeats the assessment with Fairlearn. The interactive lab of this week shows representational harms in word embeddings, which suits a task on a language model.

**Example.** Group-specific thresholds can close the gap in true positive rates while lowering overall accuracy slightly. Qualified applicants in group B then gain approvals, and the lender accepts a few more defaults in that group.

**What to submit.** About 400 words with a table of the results before and after, and the executed Colab notebook with Exercises 1 and 2 completed.

The weekly task supports self-learning and builds a personal portfolio. In an active semester, students who follow the course with the instructor can send their work for evaluation to utkukose@sdu.edu.tr or utkukose@gmail.com. The e-mail contains the items that the task lists under What to submit. It also includes the learning log exported from the interactive lab (tab: Reflect and submit).

## Research and report assignment (optional)

**Representational harms in Turkish language technologies.** How biased are Turkish language technologies, and what can be done about it?

**What to do.** Review the evidence on gender bias in machine translation and in language models for Turkish, where the pronoun o carries no gender [4, 7]. Then evaluate the mitigations that have been proposed.

**Where to start.** Lecture section "Representational harms in language technology" and the interactive lab of this week, which shows bias in a toy embedding space.

**Example focus.** Translating "o bir doktor" and "o bir hemşire" into English shows whether a system assigns genders to occupations.

This research assignment is optional and supports self-learning. In an active semester, students who follow these weeks with the instructor can send the report for evaluation to utkukose@sdu.edu.tr or utkukose@gmail.com. The report has 1500 to 2500 words and follows the structure of an academic paper. It cites at least six scholarly or official sources in square brackets and ends with a reference list. The [report template](https://github.com/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/exams/REPORT_TEMPLATE.md) shows a suitable structure.

## References

[1] Kamiran, F., & Calders, T. (2012). Data preprocessing techniques for classification without discrimination. *Knowledge and Information Systems*, 33(1), 1-33. <https://doi.org/10.1007/s10115-011-0463-8>

[2] Agarwal, A., Beygelzimer, A., Dudík, M., Langford, J., & Wallach, H. (2018). A reductions approach to fair classification. In *Proceedings of the 35th International Conference on Machine Learning, PMLR 80* (pp. 60-69).

[3] Hardt, M., Price, E., & Srebro, N. (2016). Equality of opportunity in supervised learning. In *Advances in Neural Information Processing Systems 29*.

[4] Bolukbasi, T., Chang, K.-W., Zou, J. Y., Saligrama, V., & Kalai, A. T. (2016). Man is to computer programmer as woman is to homemaker? Debiasing word embeddings. In *Advances in Neural Information Processing Systems 29*.

[5] Weerts, H., Dudík, M., Edgar, R., Jalali, A., Lutz, R., & Madaio, M. (2023). Fairlearn: Assessing and improving fairness of AI systems. *Journal of Machine Learning Research*, 24(257), 1-8.

[6] Kusner, M. J., Loftus, J., Russell, C., & Silva, R. (2017). Counterfactual fairness. In *Advances in Neural Information Processing Systems 30*.

[7] Caliskan, A., Bryson, J. J., & Narayanan, A. (2017). Semantics derived automatically from language corpora contain human-like biases. *Science*, 356(6334), 183-186. <https://doi.org/10.1126/science.aal4230>

[8] Gonen, H., & Goldberg, Y. (2019). Lipstick on a pig: Debiasing methods cover up systematic gender biases in word embeddings but do not remove them. In *Proceedings of the 2019 Conference of the North American Chapter of the Association for Computational Linguistics (NAACL-HLT)* (pp. 609-614). Association for Computational Linguistics. <https://arxiv.org/abs/1903.03862>

[9] Bender, E. M., Gebru, T., McMillan-Major, A., & Shmitchell, S. (2021). On the dangers of stochastic parrots: Can language models be too big?. In *Proceedings of the 2021 ACM Conference on Fairness, Accountability, and Transparency (FAccT '21)* (pp. 610-623). <https://doi.org/10.1145/3442188.3445922>

[10] Mitchell, M., Wu, S., Zaldivar, A., Barnes, P., Vasserman, L., Hutchinson, B., Spitzer, E., Raji, I. D., & Gebru, T. (2019). Model cards for model reporting. In *Proceedings of the Conference on Fairness, Accountability, and Transparency (FAT* '19)* (pp. 220-229). ACM. <https://doi.org/10.1145/3287560.3287596>

---

<sub>Machine Ethics and Artificial Intelligence Safety. Prof. Dr. Utku Kose, Süleyman Demirel University. ORCID [0000-0002-9652-6415](https://orcid.org/0000-0002-9652-6415). Content licensed under CC BY 4.0. This course is updated in line with current developments in the field. First version: September 2026. Last update: October 2026.</sub>
