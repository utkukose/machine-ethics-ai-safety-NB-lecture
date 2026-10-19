# Syllabus: Machine Ethics and Artificial Intelligence Safety

| Item | Details |
|---|---|
| Course | Machine Ethics and Artificial Intelligence Safety |
| Course code | 11118BLG001 |
| Level | Graduate (MSc and PhD) |
| Mode | Remote and asynchronous, self-paced within weekly windows |
| Duration | 14 weeks |
| Language | English |
| Instructor | Prof. Dr. Utku Kose, Department of Computer Engineering, Süleyman Demirel University |
| Additional affiliations | University of North Dakota (USA), Universidad Panamericana (Mexico City, Mexico), Vel Tech University (Chennai, India) |
| Contact | utkukose@sdu.edu.tr, utku.kose@und.edu, ukose@up.edu.mx, utkukose@gmail.com |
| Course site | https://utkukose.github.io/machine-ethics-ai-safety-NB-lecture/ |
| Updates | This course is updated in line with current developments in the field. First version: September 2026. Last update: October 2026. |

## Use in other courses

These materials were prepared for the graduate course 11118BLG001 Machine Ethics and Artificial Intelligence Safety at Süleyman Demirel University. They are openly available: Anyone may use and adapt them in courses of related scope, with attribution. Content is licensed under CC BY 4.0 and code under the MIT licence.

## Description

Artificial intelligence systems now recommend, rank, diagnose, write and act on behalf of people. This course examines two questions that follow from this shift. The first belongs to machine ethics: How can artificial agents represent and apply moral considerations when they act [1, 2]? The second belongs to AI safety: How can learning systems be kept from harmful behaviour when their objectives, data or operating conditions are imperfect [3, 4]? The course treats both questions together. It follows the argument that dystopic scenarios, moral dilemmas and technical failure modes concern the same practical question, namely whether intelligent systems will be safe enough [5]. Topics move from normative foundations and artificial moral agents, through fairness, specification, robustness, uncertainty and interpretability, to the alignment and security of large language models, advanced risks and governance.

## Learning outcomes

1. Explain the relationship between machine ethics, AI safety, AI security and AI alignment, and place a given system in Moor's typology of ethical agents.
2. Formalise consequentialist, deontological, virtue-based and contractualist reasoning as decision procedures and compare their verdicts on the same cases.
3. Evaluate top-down, bottom-up and hybrid implementations of artificial moral agents, including their failure modes.
4. Measure group fairness with standard metrics, interpret impossibility results and apply pre-, in- and post-processing mitigation.
5. Diagnose specification gaming, adversarial vulnerability, miscalibration and distribution shift in working code, and apply basic defences.
6. Analyse preference-based alignment of language models, prompt injection and advanced risks such as goal misgeneralization and deceptive behaviour.
7. Map a system to current governance instruments, including the EU AI Act and the NIST AI Risk Management Framework, and document it with a model card and a safety case.

## Weekly plan

| Week | Topic | Key readings |
|---|---|---|
| 01 | [Foundations of Machine Ethics and AI Safety](weeks/week-01/README.md) | Wiener (1960); Moor (2006); Anderson (2011); Amodei (2016) |
| 02 | [Normative Ethics as Decision Procedures](weeks/week-02/README.md) | Wallach (2009); Anderson (2011); Pavaloiu (2017); Mill (1863) |
| 03 | [Implementing Artificial Moral Agents](weeks/week-03/README.md) | Arkin (2009); Dennis (2016); Anderson (2006); Ross (1930) |
| 04 | [Moral Dilemmas, Pluralism and Social Choice](weeks/week-04/README.md) | Foot (1967); Thomson (1985); Vasant (2017); Bonnefon (2016) |
| 05 | [Algorithmic Fairness I: Harms, Metrics and Impossibility](weeks/week-05/README.md) | Suresh (2021); Mehrabi (2021); Angwin (2016); Obermeyer (2019) |
| 06 | [Algorithmic Fairness II: Mitigation and Representational Harms](weeks/week-06/README.md) | Kamiran (2012); Agarwal (2018); Hardt (2016); Weerts (2023) |
| 07 | [Specification Problems: Reward Hacking, Side Effects and Goodhart's Law](weeks/week-07/README.md) | Amodei (2016); Manheim (2018); Skalse (2022); Pan (2022) |
| 08 | [Robustness: Adversarial Examples, Poisoning and Backdoors](weeks/week-08/README.md) | Szegedy (2014); Goodfellow (2015); Madry (2018); Carlini (2017) |
| 09 | [Uncertainty, Calibration and Distribution Shift](weeks/week-09/README.md) | Guo (2017); Gal (2016); Lakshminarayanan (2017); Quiñonero-Candela (2009) |
| 10 | [Interpretability and Transparency for Safety](weeks/week-10/README.md) | Doshi-Velez (2017); Rudin (2019); Kose (2024); Ribeiro (2016) |
| 11 | [Aligning Language Models: Preferences, Feedback and Oversight](weeks/week-11/README.md) | Christiano (2017); Bradley (1952); Stiennon (2020); Ouyang (2022) |
| 12 | [Security of LLM Applications: Prompt Injection, Jailbreaks and Data Extraction](weeks/week-12/README.md) | Perez (2022); Greshake (2023); OWASP GenAI Security Project (2024); Kose (2017) |
| 13 | [Advanced Risks: Goal Misgeneralization, Power-Seeking and Deception](weeks/week-13/README.md) | Hubinger (2019); Langosco (2022); Shah (2022); Omohundro (2008) |
| 14 | [Governance, Standards and Auditing](weeks/week-14/README.md) | Jobin (2019); Floridi (2019); Mittelstadt (2019); European Parliament and Council of the European Union (2024) |

## Weekly workload

Each week asks for roughly six to eight hours of study. The work consists of reading the lecture, exploring the interactive lab and working through the Colab notebook. It ends with the self-assessment, the reflection and the weekly task.

## Assessment

Assessment combines formative and summative components. Each week offers a weekly task, an optional research and report assignment and a self-assessment in the interactive lab. The midterm capstone at the end of Week 7 and the final capstone at the end of Week 14 each consist of a coding application and a technical report. Students choose one of three advanced projects, extend its example Colab notebook and report the results. During active semesters, components and weights are announced by the instructor at the start of the semester in line with Süleyman Demirel University regulations. The self-assessments are formative and do not count towards the grade.

## Submission

The weekly task supports self-learning and builds a personal portfolio. In an active semester, students who follow the course with the instructor can send their work for evaluation to utkukose@sdu.edu.tr or utkukose@gmail.com. The e-mail contains the items that the task lists under What to submit. It also includes the learning log exported from the interactive lab (tab: Reflect and submit).

## Policies

Academic integrity: Submitted work must be the student's own, and all sources must be cited in square brackets with a reference list. Use of generative AI tools: Such tools may be used for brainstorming, language editing and coding support unless a task states otherwise. Every use must be disclosed in a short note that names the tool and describes what it was used for. Accessibility: All interactive labs support keyboard navigation and respect reduced-motion settings. Students who need adjustments should contact the instructor early in the semester. Communication: Questions are answered by e-mail or through the course discussion space announced at the start of each semester.

## Capstones

**Midterm Capstone: Ethics, Fairness and Specification in Practice** (end of Week 7): Coding application and technical report. See [exams/midterm/README.md](exams/midterm/README.md).

**Final Capstone: Building and Auditing a Safer AI System** (end of Week 14): Coding application and technical report. See [exams/final/README.md](exams/final/README.md).

Active-semester deadline: 23:53 (Türkiye time) on the Sunday that ends the capstone week, by e-mail to utkukose@sdu.edu.tr or utkukose@gmail.com.

## References cited in this syllabus

[1] Moor, J. H. (2006). The nature, importance, and difficulty of machine ethics. *IEEE Intelligent Systems*, 21(4), 18-21. <https://doi.org/10.1109/MIS.2006.80>

[2] Wallach, W., & Allen, C. (2009). *Moral Machines: Teaching Robots Right from Wrong*. Oxford University Press.

[3] Amodei, D., Olah, C., Steinhardt, J., Christiano, P., Schulman, J., & Mané, D. (2016). Concrete problems in AI safety. arXiv preprint arXiv:1606.06565. <https://arxiv.org/abs/1606.06565>

[4] Hendrycks, D., Carlini, N., Schulman, J., & Steinhardt, J. (2021). Unsolved problems in ML safety. arXiv preprint arXiv:2109.13916. <https://arxiv.org/abs/2109.13916>

[5] Kose, U. (2018). Are we safe enough in the future of artificial intelligence? A discussion on machine ethics and artificial intelligence safety. *BRAIN. Broad Research in Artificial Intelligence and Neuroscience*, 9(2), 184-197.
