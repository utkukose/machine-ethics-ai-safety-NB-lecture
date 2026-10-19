<div align="center">

# Week 05: Algorithmic Fairness I: Harms, Metrics and Impossibility

**Machine Ethics and Artificial Intelligence Safety (11118BLG001)**  
Prof. Dr. Utku Kose, Süleyman Demirel University

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/weeks/week-05/NB05_fairness_metrics.ipynb) [![Interactive lab](https://img.shields.io/badge/interactive%20lab-open-1D5B78)](https://utkukose.github.io/machine-ethics-ai-safety-NB-lecture/weeks/week-05/lab.html) [![Lecture notes](https://img.shields.io/badge/lecture%20notes-PDF-566A73)](Week05_Lecture_Notes.pdf) [![Course home](https://img.shields.io/badge/course-home-B97813)](../../README.md)

</div>

## Overview

Machine learning systems allocate loans, jobs, medical attention and police attention. This week studies how unfair outcomes arise across the machine learning life cycle, how group and individual fairness are measured, and why several natural fairness criteria cannot hold together [1, 2, 3].

**Estimated study time:** 6 to 8 hours.

## Learning outcomes

By the end of the week, students are expected to trace a fairness harm to its source in the life cycle. They should be able to compute demographic parity, equal opportunity, equalized odds and predictive parity from a confusion matrix. They should also be able to state the impossibility results of Kleinberg and colleagues and of Chouldechova. Finally, they should be able to justify the choice of a fairness criterion for a concrete application.

## Study path

| Step | Activity | Suggested time |
|---|---|---|
| 1 | Read the lecture below or the [PDF version](Week05_Lecture_Notes.pdf) | 90 minutes |
| 2 | Explore the [interactive lab](https://utkukose.github.io/machine-ethics-ai-safety-NB-lecture/weeks/week-05/lab.html) | 45 minutes |
| 3 | Work through the [Colab notebook](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/weeks/week-05/NB05_fairness_metrics.ipynb) and its exercises | 2 to 3 hours |
| 4 | Take the self-assessment in the interactive lab (tab: Check yourself) | 20 minutes |
| 5 | Answer the reflection prompts in the interactive lab, export the learning log and complete the weekly task | 60 minutes |

## Week at a glance

```mermaid
flowchart LR
  H["Historical, representation and measurement bias"] --> D["Training data"]
  D --> M["Model and threshold"]
  M --> E["Evaluation by group"]
  E --> DP["Demographic parity"]
  E --> EO["Equal opportunity, equalized odds"]
  E --> PP["Predictive parity, calibration"]
  DP --> I["Impossibility: choose and justify"]
  EO --> I
  PP --> I
```

## Lecture

### Where unfairness enters

Suresh and Guttag organised sources of harm along the machine learning life cycle [1]. Historical bias exists in the world before any data is collected. Representation bias arises when some groups are under-sampled. Measurement bias arises when features or labels are poor proxies for the construct of interest. Aggregation, learning, evaluation and deployment biases arise later. Aggregation bias occurs when one model is fitted to heterogeneous groups, and learning bias when the objective amplifies disparities. Evaluation bias occurs when benchmarks do not represent users, and deployment bias when a system is used differently from how it was designed. Mehrabi and colleagues surveyed the resulting landscape of definitions and methods [4].

Three cases show the variety of mechanisms. An investigation by ProPublica reported that a recidivism risk tool produced higher false positive rates for Black defendants than for white defendants [5]. Obermeyer and colleagues found that a widely used health algorithm predicted health care costs as a proxy for health needs [6]. Less money had been spent on Black patients with the same needs, so the algorithm assigned them lower risk scores. Buolamwini and Gebru found that commercial gender classification systems had error rates of up to 34.7 percent for darker-skinned women [7]. For lighter-skinned men, the maximum error rate was 0.8 percent. The first case concerns error rates, the second the choice of label and the third representation in training and evaluation data.

<details>
<summary><b>Check your understanding.</b> When does historical bias enter a model?</summary>

A. When the optimiser diverges  
B. When a random seed changes  
C. When the data faithfully record a world that was already unjust  
D. When the test set is too small  

**Answer: C.** A perfectly measured dataset can still encode past injustice, which the model then learns.

</details>

### Group fairness criteria

Most criteria compare statistics of a classifier across groups defined by a protected attribute. Demographic parity requires equal selection rates. Equalized odds requires equal true positive rates and equal false positive rates, and equal opportunity relaxes it to equal true positive rates only [8]. Predictive parity requires equal precision, so that a positive prediction means the same probability of a positive outcome in every group. Calibration within groups strengthens this to every score level.

Each criterion encodes a different view of what equal treatment means. Demographic parity treats unequal selection rates as the harm, which suits settings where historical labels themselves reflect discrimination. Equal opportunity treats unequal chances for qualified individuals as the harm. Predictive parity protects the meaning of a score for the people who use it. Dwork and colleagues proposed a complementary individual notion: Similar individuals should receive similar outcomes, where similarity is defined by a task-specific metric [9]. The difficulty moves to the metric, which must itself be justified.

<details>
<summary><b>Check your understanding.</b> Equal opportunity requires which quantity to be equal across groups?</summary>

A. True positive rates  
B. Selection rates  
C. Precision  
D. Overall accuracy  

**Answer: A.** Equal opportunity asks that qualified individuals have the same chance of a positive decision in every group.

</details>

### Impossibility results

Kleinberg, Mullainathan and Raghavan considered three conditions: calibration within groups and balance of scores for the positive and for the negative class [2]. They proved that the three cannot hold together except in two degenerate situations, namely perfect prediction or equal base rates across groups. Chouldechova showed a closely related result for binary predictions [3]. When prevalence differs between groups, a predictor with equal positive predictive value cannot also have equal false positive and false negative rates. The recidivism debate illustrates both results. The tool was reported to be roughly calibrated across groups, while its error rates differed, and both observations can be true at once [3, 5].

The results do not show that fairness is hopeless. They show that fairness criteria express value judgments that must be chosen, justified and documented. Figure 5.1 shows the mechanism in its simplest form: A single threshold applied to two groups with different score distributions yields different error rates and selection rates.

![Synthetic scores for two groups with different base rates. The same threshold of 0.5 yields different true positive rates, false positive rates and selection rates.](figures/w05_fig1.png)

*Figure 5.1. Synthetic scores for two groups with different base rates. The same threshold of 0.5 yields different true positive rates, false positive rates and selection rates.*

<details>
<summary><b>Check your understanding.</b> When base rates differ between groups, an imperfect classifier cannot at the same time satisfy</summary>

A. accuracy and precision  
B. any two metrics whatsoever  
C. demographic parity and nothing else  
D. calibration within groups and equal false positive and false negative rates  

**Answer: D.** This is the core of the impossibility results of Kleinberg and colleagues and of Chouldechova.

</details>

### Fairness as a socio-technical question

Metrics are computed on data, and data carry the history of the institutions that collected them. The health algorithm studied by Obermeyer and colleagues was well calibrated for cost and still unfair for need, because cost was the wrong label [6]. A fairness audit therefore begins with questions that no metric can answer. What is the decision for, and who is affected? What does each type of error cost each group, and who had a voice in answering these questions [1]?

> **Pause and reflect.** In a university admission model, is a false negative (rejecting a student who would have succeeded) worse than a false positive? Does the answer differ for students from under-represented schools?

<details>
<summary><b>Check your understanding.</b> What does it mean to treat fairness as a socio-technical question?</summary>

A. Ignoring metrics  
B. Considering context, institutions and affected people, not only model metrics  
C. Delegating all decisions to lawyers  
D. Optimising accuracy first and fairness later  

**Answer: B.** Metrics capture only part of fairness. The deployment context decides which harms matter.

</details>

## Interactive lab

Two synthetic groups receive scores from the same model. Move the thresholds and the base rate of group B and watch the fairness gaps. Untick the single-threshold option to try equalising true positive rates, which is the idea behind post-processing in Week 6 [2, 8].

[Open the interactive lab](https://utkukose.github.io/machine-ethics-ai-safety-NB-lecture/weeks/week-05/lab.html)

![Screenshot of the Week 5 interactive lab](screenshots/lab.png)

## Colab notebook

The Colab notebook builds a synthetic lending data set in which group B carries a historical disadvantage. It trains a model that never sees the group attribute and measures every fairness criterion of the lecture. An optional section repeats the audit on the Adult census data set when an internet connection is available [2, 8].

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/weeks/week-05/NB05_fairness_metrics.ipynb)

Screenshots of the executed Colab notebook:

![Output 1 of the Week 5 Colab notebook](screenshots/nb_1.png)
![Output 2 of the Week 5 Colab notebook](screenshots/nb_2.png)

## Self-assessment and reflection

The interactive lab contains a self-assessment of six questions (tab: Check yourself). Students answer each question, state how sure they are and receive instant feedback. A confident but wrong answer marks the first topic to revisit. The reflection prompts below also appear in the interactive lab (tab: Reflect and submit). Answers written there are saved in the browser and can be exported as a learning log.

1. Which source of harm in the framework of Suresh and Guttag is most likely in a data set from your field, and how would you detect it?
2. Choose one fairness criterion for a decision system you know and defend it against the other criteria in three sentences.
3. The impossibility results turn fairness into a choice. Who should make that choice for a public-sector system, and how should it be documented?

## Weekly task and submission

**What to do.** Write a short fairness audit of one model. Use the lending model of the Colab notebook or a model and data set from your field. First, describe the decision and the groups that are compared. Second, report at least four group metrics, such as the selection rate, the true positive rate, the false positive rate and the precision of each group. Third, argue which criterion matters most for this decision and why. Finally, state one limitation of the audit.

**Where to look.** Lecture: sections "Group fairness criteria" and "Impossibility results". Interactive lab: the threshold explorer, which shows how the gaps move with the thresholds (tab: Explore). Colab notebook: Sections 1 to 3. The optional Section 4 repeats the audit on the Adult census data.

**Example.** An audit of the lending model could find that group B has a lower true positive rate at threshold 0.5. It could then argue that equal opportunity matters most, because a qualified applicant who is refused loses a real benefit.

**What to submit.** About 500 words with a table of the metrics, and the executed Colab notebook with Exercises 1 and 2 completed.

The weekly task supports self-learning and builds a personal portfolio. In an active semester, students who follow the course with the instructor can send their work for evaluation to utkukose@sdu.edu.tr or utkukose@gmail.com. The e-mail contains the items that the task lists under What to submit. It also includes the learning log exported from the interactive lab (tab: Reflect and submit).

## Research and report assignment (optional)

**Fairness definitions in a regulated domain.** Which fairness definitions are used in practice, and why?

**What to do.** Choose credit, hiring or health care. Review which fairness definitions regulators, auditors and practitioners actually use in that domain. Then relate their choices to the impossibility results of this week [2, 3].

**Where to start.** Lecture sections "Group fairness criteria" and "Impossibility results", and the guidance documents of one regulator in the chosen domain.

**Example focus.** In hiring, the four-fifths rule compares selection rates between groups, which is a form of demographic parity.

This research assignment is optional and supports self-learning. In an active semester, students who follow these weeks with the instructor can send the report for evaluation to utkukose@sdu.edu.tr or utkukose@gmail.com. The report has 1500 to 2500 words and follows the structure of an academic paper. It cites at least six scholarly or official sources in square brackets and ends with a reference list. The [report template](https://github.com/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/exams/REPORT_TEMPLATE.md) shows a suitable structure.

## References

[1] Suresh, H., & Guttag, J. (2021). A framework for understanding sources of harm throughout the machine learning life cycle. In *Equity and Access in Algorithms, Mechanisms, and Optimization (EAAMO '21)*. ACM. <https://doi.org/10.1145/3465416.3483305>

[2] Kleinberg, J., Mullainathan, S., & Raghavan, M. (2017). Inherent trade-offs in the fair determination of risk scores. In *8th Innovations in Theoretical Computer Science Conference (ITCS 2017), LIPIcs 67* (pp. 43:1-43:23). <https://doi.org/10.4230/LIPIcs.ITCS.2017.43>

[3] Chouldechova, A. (2017). Fair prediction with disparate impact: A study of bias in recidivism prediction instruments. *Big Data*, 5(2), 153-163. <https://doi.org/10.1089/big.2016.0047>

[4] Mehrabi, N., Morstatter, F., Saxena, N., Lerman, K., & Galstyan, A. (2021). A survey on bias and fairness in machine learning. *ACM Computing Surveys*, 54(6), Article 115. <https://doi.org/10.1145/3457607>

[5] Angwin, J., Larson, J., Mattu, S., & Kirchner, L. (2016). *Machine bias*. ProPublica. <https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing>

[6] Obermeyer, Z., Powers, B., Vogeli, C., & Mullainathan, S. (2019). Dissecting racial bias in an algorithm used to manage the health of populations. *Science*, 366(6464), 447-453. <https://doi.org/10.1126/science.aax2342>

[7] Buolamwini, J., & Gebru, T. (2018). Gender shades: Intersectional accuracy disparities in commercial gender classification. In *Proceedings of the 1st Conference on Fairness, Accountability and Transparency, PMLR 81* (pp. 77-91).

[8] Hardt, M., Price, E., & Srebro, N. (2016). Equality of opportunity in supervised learning. In *Advances in Neural Information Processing Systems 29*.

[9] Dwork, C., Hardt, M., Pitassi, T., Reingold, O., & Zemel, R. (2012). Fairness through awareness. In *Proceedings of the 3rd Innovations in Theoretical Computer Science Conference* (pp. 214-226). ACM. <https://doi.org/10.1145/2090236.2090255>

---

<sub>Machine Ethics and Artificial Intelligence Safety. Prof. Dr. Utku Kose, Süleyman Demirel University. ORCID [0000-0002-9652-6415](https://orcid.org/0000-0002-9652-6415). Content licensed under CC BY 4.0. This course is updated in line with current developments in the field. First version: September 2026. Last update: October 2026.</sub>
