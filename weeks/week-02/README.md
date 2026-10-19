<div align="center">

# Week 02: Normative Ethics as Decision Procedures

**Machine Ethics and Artificial Intelligence Safety (11118BLG001)**  
Prof. Dr. Utku Kose, Süleyman Demirel University

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/weeks/week-02/NB02_normative_theories.ipynb) [![Interactive lab](https://img.shields.io/badge/interactive%20lab-open-1D5B78)](https://utkukose.github.io/machine-ethics-ai-safety-NB-lecture/weeks/week-02/lab.html) [![Lecture notes](https://img.shields.io/badge/lecture%20notes-PDF-566A73)](Week02_Lecture_Notes.pdf) [![Course home](https://img.shields.io/badge/course-home-B97813)](../../README.md)

</div>

## Overview

Every automated decision encodes a trade-off between values. This week introduces the four families of normative theory that dominate machine ethics: consequentialism, deontology, virtue ethics and contractualism. Each family is treated as a decision procedure that can be implemented, tested and criticised [1, 2].

**Estimated study time:** 6 to 8 hours.

## Learning outcomes

By the end of the week, students are expected to state the core claim of each theory and to write each theory as an explicit decision procedure. They should also explain why the procedures disagree on classic cases such as the trolley problem. Finally, they should be able to describe methods for acting under moral uncertainty.

## Study path

| Step | Activity | Suggested time |
|---|---|---|
| 1 | Read the lecture below or the [PDF version](Week02_Lecture_Notes.pdf) | 90 minutes |
| 2 | Explore the [interactive lab](https://utkukose.github.io/machine-ethics-ai-safety-NB-lecture/weeks/week-02/lab.html) | 45 minutes |
| 3 | Work through the [Colab notebook](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/weeks/week-02/NB02_normative_theories.ipynb) and its exercises | 2 to 3 hours |
| 4 | Take the self-assessment in the interactive lab (tab: Check yourself) | 20 minutes |
| 5 | Answer the reflection prompts in the interactive lab, export the learning log and complete the weekly task | 60 minutes |

## Week at a glance

```mermaid
flowchart TD
  C["Case with options"] --> U["Consequentialist: maximise expected well-being"]
  C --> D["Deontological: remove options that violate duties"]
  C --> V["Virtue-based: act as a virtuous agent would"]
  C --> K["Contractualist: principles no one could reasonably reject"]
  U --> M["Moral uncertainty: weigh verdicts by credence"]
  D --> M
  V --> M
  K --> M
  M --> A["Action with an explicit justification"]
```

## Lecture

### Why engineers need normative theory

A triage model trades sensitivity against the burden of false alarms. A content filter trades freedom of expression against protection from harm. Such trade-offs are made whether or not designers state them. Normative ethics offers structured ways to state and defend them [1, 2]. Pavaloiu and Kose described ethical artificial intelligence as an open question precisely because no single theory commands agreement, while deployed systems must nonetheless act [3].

A useful distinction separates a criterion of rightness from a decision procedure. A criterion states what makes an action right. A decision procedure is a method that an agent follows in order to choose. Machine ethics needs decision procedures, and this week treats each major theory as a candidate procedure. The simplification is deliberate: Writing a theory as code exposes the assumptions that prose often hides, such as how outcomes are measured and whose interests count.

<details>
<summary><b>Check your understanding.</b> Why do system designers need normative theory?</summary>

A. Every design choice that trades off harms and benefits embeds a normative position, stated or not  
B. The law requires engineers to hold philosophy degrees  
C. Normative theories output loss functions automatically  
D. Theories remove the need to consult stakeholders  

**Answer: A.** Making the position explicit allows it to be examined, justified and changed.

</details>

### Consequences and duties

Consequentialism judges actions by their outcomes. In its classical utilitarian form, the right action maximises overall well-being [4]. The computational analogue is familiar to every engineer: Choose the action with the highest expected utility. The difficulties are also familiar. Utilities must be measured and compared across people, and a simple sum can justify sacrificing a few for a small gain to many.

Deontology judges actions by their conformity to duties. Kant's categorical imperative requires acting only on maxims that could be willed as universal law and treating persons never merely as means [5]. The computational analogue is a set of constraints that remove forbidden actions before any optimisation. Constraints are transparent and predictable, but duties can conflict, and absolute prohibitions may lead to disastrous outcomes in unusual cases. Ross proposed prima facie duties that can be outweighed by stronger duties, an idea that later inspired implemented systems [6].

The trolley problem, introduced by Foot and developed by Thomson, isolates the tension between the two families [7, 8]. Diverting a runaway trolley so that it kills one person instead of five is widely judged permissible. Pushing a person from a footbridge to stop the trolley, with the same numbers, is widely judged wrong. A pure expected-utility procedure cannot distinguish the cases, whereas a constraint against using a person merely as a means can.

<details>
<summary><b>Check your understanding.</b> A rule that forbids using a person merely as a means, even to save more lives, reflects</summary>

A. act utilitarianism  
B. virtue ethics  
C. ethical egoism  
D. Kantian deontology  

**Answer: D.** Kant's formula of humanity forbids treating persons merely as means, whatever the consequences.

</details>

### Character and fair agreement

Virtue ethics shifts attention from single acts to character. An action is right if a virtuous agent would characteristically perform it in the circumstances [9]. Vallor argued that technology calls for technomoral virtues such as honesty, humility, justice and practical wisdom [10]. For machines, virtue ethics suggests learning stable dispositions from exemplary behaviour, which connects it with bottom-up learning.

Contractualism grounds morality in principles that no one could reasonably reject [11]. Rawls's thought experiment of choosing principles behind a veil of ignorance leads to special concern for the worst-off, often written as a maximin rule [12]. Gabriel argued that AI alignment should not follow the values of a single designer. It should instead seek principles that people with different moral views could endorse through a fair process [13]. A maximin rule is only a crude stand-in for these ideas, and the Colab notebook shows a case in which it diverges from what contractualists would conclude.

![Verdicts of four simplified decision procedures on six cases used in the interactive lab and Colab notebook. The procedures agree on the trolley switch case and split on the others.](figures/w02_fig1.png)

*Figure 2.1. Verdicts of four simplified decision procedures on six cases used in the interactive lab and Colab notebook. The procedures agree on the trolley switch case and split on the others.*

<details>
<summary><b>Check your understanding.</b> Rawls&#x27;s veil of ignorance asks people to choose principles</summary>

A. that maximise total welfare  
B. without knowing their own position in society  
C. that a virtuous person would choose  
D. that the majority already prefers  

**Answer: B.** Choosing without knowledge of one's own position is meant to make the choice impartial.

</details>

### Acting under moral uncertainty

No theory is uncontroversial, so an artificial agent faces moral uncertainty in addition to empirical uncertainty. MacAskill, Bykvist and Ord analysed ways of acting under such uncertainty, including maximising expected choice-worthiness across theories weighted by credence [14]. A related device is a moral parliament, in which each theory receives votes in proportion to its credence. These procedures make value trade-offs explicit and auditable. They also rest on a contested assumption, namely that the verdicts of rival theories can be compared on a common scale.

The distinction of Allen, Smit and Wallach applies here as well [15]. Top-down implementations encode a theory as rules or as an objective. Bottom-up implementations learn behaviour from examples. Hybrid designs let learned components propose actions and let explicit principles constrain or justify them, which is the architecture examined in Week 3.

> **Pause and reflect.** Consider an automated triage assistant that ranks patients only by expected life-years saved. Which theory has its designers implicitly adopted, and which patients could reasonably reject the ranking?

<details>
<summary><b>Check your understanding.</b> What does maximising expected choiceworthiness under moral uncertainty require?</summary>

A. Following only the single most probable theory  
B. Choosing an action at random  
C. Credences in theories and a way to compare their scales of choiceworthiness  
D. Unanimous agreement among all theories  

**Answer: C.** Comparing choiceworthiness across theories is the central difficulty of the approach.

</details>

## Interactive lab

Choose a case and set how much weight the decision should give to consequences, duties, character and the worst-off. The chart shows the combined score of each option, and the table shows what each pure theory would choose [7, 8, 14].

[Open the interactive lab](https://utkukose.github.io/machine-ethics-ai-safety-NB-lecture/weeks/week-02/lab.html)

![Screenshot of the Week 2 interactive lab](screenshots/lab.png)

## Colab notebook

The Colab notebook writes the four theories as Python functions and tabulates their verdicts on six cases. It measures how often they agree and builds a moral parliament that weighs them by credence [14].

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/weeks/week-02/NB02_normative_theories.ipynb)

Screenshots of the executed Colab notebook:

![Output 1 of the Week 2 Colab notebook](screenshots/nb_1.png)

## Self-assessment and reflection

The interactive lab contains a self-assessment of six questions (tab: Check yourself). Students answer each question, state how sure they are and receive instant feedback. A confident but wrong answer marks the first topic to revisit. The reflection prompts below also appear in the interactive lab (tab: Reflect and submit). Answers written there are saved in the browser and can be exported as a learning log.

1. Which of the four theories comes closest to how decisions are made in a system you know, and where does that system hide its value trade-offs?
2. The maximin rule produced a verdict that contractualists would reject. Describe one way to improve the operationalisation.
3. Is it acceptable for an AI system to act under a moral parliament whose credences were chosen by its developers? Give one argument for and one against.

## Weekly task and submission

**What to do.** Turn one decision from your field into a case for the four decision procedures of this week. First, describe the decision and two options it must choose between. Second, give each option the four attributes used in the Colab notebook: welfare, duty violation (1 or 0), character score and the outcome for the worst-off party. Justify each number in one sentence. Third, add the two options as a new case in the Colab notebook and report the verdict of each theory and of a moral parliament. Choose the credences of the parliament and defend them.

**Where to look.** Lecture: sections "Consequences and duties", "Character and fair agreement" and "Acting under moral uncertainty". Interactive lab: the case selector and the weight sliders (tab: Explore). Colab notebook: Section 1 for the format of the attributes and Section 3 for the moral parliament.

**Example.** A delivery robot can wait at a crowded crossing or take a shortcut through a pedestrian zone. The shortcut gives more welfare but breaks a traffic rule, so the deontological procedure rejects it while the utilitarian procedure chooses it.

**What to submit.** About 300 words with a table of the two options and their attributes, and the Colab notebook with Exercises 1 and 2 completed and your own case added.

The weekly task supports self-learning and builds a personal portfolio. In an active semester, students who follow the course with the instructor can send their work for evaluation to utkukose@sdu.edu.tr or utkukose@gmail.com. The e-mail contains the items that the task lists under What to submit. It also includes the learning log exported from the interactive lab (tab: Reflect and submit).

## Research and report assignment (optional)

**Moral theories inside real decision rules.** Which normative theory does an automated decision rule embody?

**What to do.** Select one deployed or proposed decision rule, such as an organ allocation score or a triage protocol. Analyse which normative theory its rule embodies [4, 5, 12]. Then discuss what a proponent of a rival theory would change, and why.

**Where to start.** Lecture sections "Consequences and duties" and "Character and fair agreement". The decision procedures in Section 1 of the Colab notebook can be used to test the rule on a few cases.

**Example focus.** A rule that allocates organs by expected life-years gained is consequentialist. A contractualist in the tradition of Rawls might add a priority for the worst-off.

This research assignment is optional and supports self-learning. In an active semester, students who follow these weeks with the instructor can send the report for evaluation to utkukose@sdu.edu.tr or utkukose@gmail.com. The report has 1500 to 2500 words and follows the structure of an academic paper. It cites at least six scholarly or official sources in square brackets and ends with a reference list. The [report template](https://github.com/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/exams/REPORT_TEMPLATE.md) shows a suitable structure.

## References

[1] Wallach, W., & Allen, C. (2009). *Moral Machines: Teaching Robots Right from Wrong*. Oxford University Press.

[2] Anderson, M., & Anderson, S. L. (Eds.) (2011). *Machine Ethics*. Cambridge University Press.

[3] Pavaloiu, A., & Kose, U. (2017). Ethical artificial intelligence: An open question. *Journal of Multidisciplinary Developments*, 2(2), 15-27.

[4] Mill, J. S. (1863). *Utilitarianism*. Parker, Son, and Bourn.

[5] Kant, I. (1785). *Grundlegung zur Metaphysik der Sitten [Groundwork of the Metaphysics of Morals]*. Johann Friedrich Hartknoch.

[6] Ross, W. D. (1930). *The Right and the Good*. Clarendon Press.

[7] Foot, P. (1967). The problem of abortion and the doctrine of the double effect. *Oxford Review*, 5, 5-15.

[8] Thomson, J. J. (1985). The trolley problem. *The Yale Law Journal*, 94(6), 1395-1415. <https://doi.org/10.2307/796133>

[9] Hursthouse, R. (1999). *On Virtue Ethics*. Oxford University Press.

[10] Vallor, S. (2016). *Technology and the Virtues: A Philosophical Guide to a Future Worth Wanting*. Oxford University Press.

[11] Scanlon, T. M. (1998). *What We Owe to Each Other*. Belknap Press of Harvard University Press.

[12] Rawls, J. (1971). *A Theory of Justice*. Harvard University Press.

[13] Gabriel, I. (2020). Artificial intelligence, values, and alignment. *Minds and Machines*, 30(3), 411-437. <https://doi.org/10.1007/s11023-020-09539-2>

[14] MacAskill, W., Bykvist, K., & Ord, T. (2020). *Moral Uncertainty*. Oxford University Press.

[15] Allen, C., Smit, I., & Wallach, W. (2005). Artificial morality: Top-down, bottom-up, and hybrid approaches. *Ethics and Information Technology*, 7(3), 149-155. <https://doi.org/10.1007/s10676-006-0004-4>

---

<sub>Machine Ethics and Artificial Intelligence Safety. Prof. Dr. Utku Kose, Süleyman Demirel University. ORCID [0000-0002-9652-6415](https://orcid.org/0000-0002-9652-6415). Content licensed under CC BY 4.0. This course is updated in line with current developments in the field. First version: September 2026. Last update: October 2026.</sub>
