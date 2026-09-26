<div align="center">

# Final Capstone: Building and Auditing a Safer AI System

**Machine Ethics and Artificial Intelligence Safety (11118BLG001)**  
Prof. Dr. Utku Kose, Süleyman Demirel University

[![Course home](https://img.shields.io/badge/course-home-B97813)](../../README.md)

</div>

## Overview

The final capstone integrates Weeks 8 to 14: robustness, uncertainty and calibration, interpretability, the alignment and security of language model applications, and governance [1, 2, 3, 4]. Each student chooses one of the three advanced projects below, extends the example notebook and writes a technical report that ends with a structured safety or audit argument.

## Formats

In this course, both capstones combine a coding application with a technical report. The application is a Colab notebook that extends one of the three example notebooks and runs from top to bottom without errors. The report of 2500 to 4000 words follows the course report template. Each student works individually unless the instructor announces otherwise. The weights below are indicative; in active semesters the instructor confirms them at the start of the semester.

## Advanced application projects

Each project comes with an example Colab notebook that implements a working baseline. The capstone extends the baseline as described, evaluates the extensions and reports the results.

### Project 1: A safety case for a clinical risk model

A malignancy classifier trained on a public diagnostic dataset is examined for adversarial robustness, calibration, conformal coverage and detection of distribution shift, and the evidence is assembled into claims, arguments and evidence [2, 5, 6, 7].

**Required extensions.** Add a non-linear model and a stronger attack, such as projected gradient descent [1], report class-conditional conformal coverage, and evaluate at least two realistic shift scenarios with a monitor that raises alarms. Rewrite the safety case in the Goal Structuring Notation, identify the weakest claim and state what additional evidence would be needed before any clinical use.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/exams/final/FIN1_clinical_safety_case.ipynb) Example notebook: `FIN1_clinical_safety_case.ipynb`

![Output of the example notebook](screenshots/FIN1_clinical_safety_case_1.png)

### Project 2: Explanations under scrutiny: faithfulness, stability and manipulation

Three local attribution methods are implemented for a gradient boosting classifier and evaluated for faithfulness with deletion curves, for agreement, for stability under small input noise and with a model randomisation sanity check [8, 9, 10]. A final experiment shows how a scaffolded model can hide its reliance on a sensitive attribute from perturbation-based explanations [11].

**Required extensions.** Add at least one further attribution method, for example GEMEX or integrated gradients on a differentiable model [12], and one further faithfulness metric. Test whether a defence, such as on-manifold perturbations, restores the hidden attribute in the scaffolding experiment, and discuss what the results imply for audits that rely on explanations [13].

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/exams/final/FIN2_explanations_under_scrutiny.ipynb) Example notebook: `FIN2_explanations_under_scrutiny.ipynb`

![Output of the example notebook](screenshots/FIN2_explanations_under_scrutiny_1.png)
![Output of the example notebook](screenshots/FIN2_explanations_under_scrutiny_2.png)

### Project 3: Red-teaming an LLM-integrated agent: attack families and layered defences

An e-mail assistant that summarises retrieved documents is attacked with five families of indirect prompt injection, including obfuscated and Turkish-language payloads [3, 14]. Because the example must run offline, the language model is replaced by a transparent simulated model whose compliance depends on features of the injected text. Four defences and their combinations are evaluated for attack success, false positives and utility [15].

**Required extensions.** Replace the simulated model with a real model through an API, keeping the key in an environment variable, or with an open model run locally, and repeat the evaluation with at least 200 documents per condition. Add two attack families and one defence, measure cross-lingual generalisation of the classifier, and propose a defence-in-depth design with a quantified residual risk.

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/exams/final/FIN3_agent_red_teaming.ipynb) Example notebook: `FIN3_agent_red_teaming.ipynb`

![Output of the example notebook](screenshots/FIN3_agent_red_teaming_1.png)
![Output of the example notebook](screenshots/FIN3_agent_red_teaming_2.png)

## Report

The technical report states the question, explains the design choices, presents the experiments with the figures produced by the notebook and discusses the ethical and safety implications and the limitations of the results. It cites at least eight sources in square brackets, at least four of them from the course readings, and links to the final Colab notebook.

A common structure for reports is given in the [report template](https://github.com/utkukose/machine-ethics-ai-safety-NB-lecture/blob/main/exams/REPORT_TEMPLATE.md).

## Assessment criteria

| Criterion | Weight | What is assessed |
|---|---|---|
| Technical correctness and reproducibility | 30% | The notebook runs end to end, the implementation is correct and results are reproducible with the stated seeds. |
| Depth of the extensions | 25% | The required extensions are implemented thoughtfully and go beyond the example. |
| Analysis and interpretation | 20% | Results are analysed with appropriate metrics, comparisons and uncertainty. |
| Ethical and safety reasoning | 15% | The report connects the results to the concepts and debates of the course. |
| Writing and referencing | 10% | The report is clear, well structured and correctly referenced. |

## Submission

This capstone also supports self-learning and can be completed at any pace. When the course is taught actively in a semester, the final capstone is sent by e-mail to utkukose@sdu.edu.tr or utkukose@gmail.com no later than 23:53 (Türkiye time) on the last Sunday of Week 14, with the report and all code files attached or linked.

## References

[1] Madry, A., Makelov, A., Schmidt, L., Tsipras, D., & Vladu, A. (2018). Towards deep learning models resistant to adversarial attacks. In *International Conference on Learning Representations (ICLR)*. <https://arxiv.org/abs/1706.06083>

[2] Angelopoulos, A. N., & Bates, S. (2023). Conformal prediction: A gentle introduction. *Foundations and Trends in Machine Learning*, 16(4), 494-591. <https://doi.org/10.1561/2200000101>

[3] Greshake, K., Abdelnabi, S., Mishra, S., Endres, C., Holz, T., & Fritz, M. (2023). Not what you've signed up for: Compromising real-world LLM-integrated applications with indirect prompt injection. In *Proceedings of the 16th ACM Workshop on Artificial Intelligence and Security (AISec '23)* (pp. 79-90). ACM. <https://arxiv.org/abs/2302.12173>

[4] National Institute of Standards and Technology (2023). *Artificial Intelligence Risk Management Framework (AI RMF 1.0), NIST AI 100-1*. U.S. Department of Commerce. <https://doi.org/10.6028/NIST.AI.100-1>

[5] Goodfellow, I. J., Shlens, J., & Szegedy, C. (2015). Explaining and harnessing adversarial examples. In *International Conference on Learning Representations (ICLR)*. <https://arxiv.org/abs/1412.6572>

[6] Guo, C., Pleiss, G., Sun, Y., & Weinberger, K. Q. (2017). On calibration of modern neural networks. In *Proceedings of the 34th International Conference on Machine Learning, PMLR 70* (pp. 1321-1330).

[7] Kelly, T., & Weaver, R. (2004). The Goal Structuring Notation: A safety argument notation. In *Proceedings of the Dependable Systems and Networks 2004 Workshop on Assurance Cases*.

[8] Ribeiro, M. T., Singh, S., & Guestrin, C. (2016). "Why should I trust you?": Explaining the predictions of any classifier. In *Proceedings of the 22nd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining* (pp. 1135-1144). <https://doi.org/10.1145/2939672.2939778>

[9] Lundberg, S. M., & Lee, S.-I. (2017). A unified approach to interpreting model predictions. In *Advances in Neural Information Processing Systems 30*.

[10] Adebayo, J., Gilmer, J., Muelly, M., Goodfellow, I., Hardt, M., & Kim, B. (2018). Sanity checks for saliency maps. In *Advances in Neural Information Processing Systems 31*.

[11] Slack, D., Hilgard, S., Jia, E., Singh, S., & Lakkaraju, H. (2020). Fooling LIME and SHAP: Adversarial attacks on post hoc explanation methods. In *Proceedings of the AAAI/ACM Conference on AI, Ethics, and Society* (pp. 180-186). <https://doi.org/10.1145/3375627.3375830>

[12] Kose, U. (2026). *GEMEX: Geodesic Entropic Manifold Explainability (Version 1.2.2) [Python package]*. Python Package Index. <https://pypi.org/project/gemex/>

[13] Rudin, C. (2019). Stop explaining black box machine learning models for high stakes decisions and use interpretable models instead. *Nature Machine Intelligence*, 1(5), 206-215. <https://doi.org/10.1038/s42256-019-0048-x>

[14] Perez, F., & Ribeiro, I. (2022). Ignore previous prompt: Attack techniques for language models. arXiv preprint arXiv:2211.09527. <https://arxiv.org/abs/2211.09527>

[15] OWASP GenAI Security Project (2024). *OWASP Top 10 for LLM Applications 2025 (version 2025, released 18 November 2024)*. OWASP Foundation. <https://genai.owasp.org/>

---

<sub>Machine Ethics and Artificial Intelligence Safety. Prof. Dr. Utku Kose, Süleyman Demirel University. ORCID [0000-0002-9652-6415](https://orcid.org/0000-0002-9652-6415). Content licensed under CC BY 4.0. This course is updated in line with current developments in the field. Last update: September 2026.</sub>
