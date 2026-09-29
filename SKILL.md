---
name: experiment-reflection
description: Analyze completed research experiments against the original idea, explain positive, negative, or unclear signals, diagnose errors and mechanisms, and design credible improvements. Use for post-experiment reflection, failure diagnosis, reanalysis, or connecting results to paper claims; not for routine job-status reporting.
---

# Experiment Reflection

Turn experimental outputs into evidence about the research idea. The objective is to develop the strongest credible support for the fixed research line: understand what happened, explain why, correct what went wrong, and identify the most useful next step. Finishing a run or reporting a metric does not complete this work. Reflection is complete only when the available results have been analyzed and connected back to the idea.

Use the user's language for deliverables. Work within the existing execution authorization, budget, and research stage; respect frozen or offline-only protocols. This skill guides analysis and development but does not authorize new spending, runs, or changes to an approved claim. It can be used independently or after `research-idea-audit`.

## 1. Recover the claim and the evidence

Read the current research dossier and experiment plan. Identify the original claim, proposed mechanism, necessary conditions, predicted observations, comparator, target population, primary metric, decision rules, and the precise purpose of this experiment. If a prediction was never specified, mark a reconstruction as retrospective; do not call it preregistered.

Inventory every run in the requested scope, including failed, incomplete, excluded, and repeated runs. Link results to data, code, model and prompt versions, configurations, seeds where relevant, evaluation outputs, and protocol deviations. Preserve original artifacts. If only a summary is available, analyze what it supports and name the missing records needed to resolve the rest.

Write the expected chain explicitly: **intervention → mechanism activation → intermediate change → outcome → contribution**. Locate which links the experiment actually observes or tests.

## 2. Classify validity and signal separately

First decide whether each comparison is valid, partially usable, or invalid for its intended claim. A broken evaluator, missing paired observations, or failed treatment delivery can make an effect unassessable. Missing or invalid results are not numeric zero effects.

For interpretable comparisons, classify the signal relative to the original prediction:

| Signal | Meaning | Required interpretation |
| --- | --- | --- |
| Positive | Evidence points in the predicted direction with meaningful magnitude and adequate credibility | State which prediction is supported and what remains unexplained |
| Negative | Evidence points against the prediction or shows meaningful harm | Identify the challenged assumption or link; investigate both defects and scientific explanations |
| No clear signal | Evidence is too weak, variable, small, or conflicting to resolve the prediction | Distinguish imprecision from evidence that the effect is too small to matter |

Report effect size, baseline, denominator, variation, and appropriate uncertainty. A favorable point estimate with large uncertainty is tentative. A nonsignificant result alone does not establish no effect. Keep mixed outcomes visible by claim, metric, or condition rather than forcing one favorable label onto the entire experiment.

## 3. Diagnose the result through concrete evidence

Investigate the layers relevant to this experiment and maintain a diagnosis ledger. Cover the whole path before claiming the diagnosis is complete; mark unexamined areas explicitly.

- **Implementation and delivery:** Did the intended code, prompt, treatment, routing, or training update actually execute? Check version drift, ignored settings, malformed outputs, parsing, retries, truncation, and failure handling against raw traces.
- **Data and task fit:** Do fields, labels, splits, difficulty, sample selection, and available information satisfy the experiment's assumptions? Check contamination, duplicate units, missing cases, ceiling or floor effects, and whether the mechanism has an opportunity to help.
- **Comparison and measurement:** Are controls comparable in information, resources, and evaluation? Check sample alignment, denominators, score direction, units, aggregation, evaluator correctness, and whether the metric measures the claimed benefit.
- **Design and inference:** Can this contrast identify the intended effect? Examine confounding, dependence, sample size and precision, repeated searching, unequal attrition, treatment strength, and sensitivity to a few observations.
- **Mechanism and assumptions:** Did the intervention activate the mechanism? Did the intermediate change occur? If it occurred without the predicted outcome, which downstream link failed? Consider tradeoffs, domain limits, and the possibility that the prediction is wrong under these conditions.

For each candidate cause, record an observed symptom, supporting and conflicting evidence, the expected causal path to the result, a discriminating check, and a status: **confirmed**, **plausible**, **ruled out**, or **not checked**. Link to actual records or code when available. Separate defects from scientific limitations and unresolved hypotheses. Avoid vague diagnoses such as "the prompt needs improvement" without evidence about what failed and why.

Check systematic patterns across comparable cases and inspect representative successes and failures. Explain how cases were selected. Examples can illustrate a mechanism; they do not establish how common it is. Rank causes by evidence and impact, including interactions when one defect masks another. Report all discovered issues and unresolved areas without claiming to have found every possible error.

## 4. For negative or unclear signals, build a credible recovery path

Treat an unsuccessful development run as a reason to investigate. It may reflect a repairable implementation, poor measurement, an insensitive design, an unmet mechanism condition, or a limit of the idea. Do not abandon the idea solely because one implementation failed, and do not assume every unfavorable result must be an error.

Develop specific changes from the diagnosis:

- **Repair a confirmed defect:** State the violated specification, exact correction, smallest check that demonstrates the repair, and which historical results are affected. Retain the original run and version corrected outputs separately.
- **Improve the experiment:** Adjust treatment delivery, measurement, task difficulty, or precision when the diagnosis justifies it. Explain why the change tests the same mechanism and predict what should change if the diagnosis is correct. Keep a comparable control and change as few factors as needed to identify the cause.
- **Reanalyze existing data:** Consider justified pairing, corrected denominators, distributions, failure categories, intermediate outcomes, or mechanism-relevant conditions. Explain why each analysis answers the research question. A benefit in a defensible condition may support a conditional claim even when the aggregate is unclear; retain the aggregate and report the condition's coverage and limitations.

Label analyses or conditions discovered after seeing outcomes as exploratory. Record alternatives examined. Do not select only favorable observations, seeds, metrics, or cutoffs and present them as the original confirmatory result. Use independent data or a prospective controlled test when confirmation is needed. If a change alters the core claim or its approved scope, propose it explicitly as a new version for the user's review.

For every proposed fix, reanalysis, or run, give: **diagnosis → change → predicted observation → evidence gained for the idea → cost → continuation or stop rule**. Prefer existing evidence and cheap checks, then the smallest informative controlled run. Within the authorized budget, prioritize paths likely to produce credible positive evidence and resolve the most consequential uncertainty. Further analysis may also strengthen evidence against the idea; report that outcome accurately.

### Confirm each experiment and revalidate before scaling

Before launching any experiment, including a validation run, diagnostic pilot, rerun after a fix, or larger batch, present the complete resolved configuration and obtain the user's explicit confirmation. Include purpose, code/environment versions, data/split/sample selection and size, arms/baselines, models/providers, prompts, hyperparameters/seeds/repetitions, evaluator/metrics, concurrency/timeouts/retries, cost and stop limits, and output location. Show effective defaults and exclude secrets. Save the configuration and confirmation; approval applies only to the exact run or enumerated batch presented. A new launch or configuration change needs fresh confirmation, while internal steps of an already approved run do not.

Scale up only after minimal real end-to-end checks cover every planned arm, baseline, model/provider route, dataset format, and evaluation path. Verify both execution and correctness against the design through raw traces, effective settings, aligned inputs and labels, valid treatment/control behavior, independently checked representative scores, aggregation, and saved outputs. Record evidence and pass/fail/not-checked status for each required path; mock results or a successful exit alone do not pass this gate. Resolve all failed or unchecked paths and revalidate those affected by a fix. Present this evidence and obtain confirmation of the larger-run configuration before any increase in scale, even a modest one.

## 5. For positive signals, explain why the result is good

Apply the same validity and diagnosis checks to positive results. Investigate whether gains come from the proposed mechanism, extra resources or information, an easier comparison, evaluation artifacts, sample composition, or chance.

Trace the supported path from intervention to intermediate behavior to outcome. Identify which observations discriminate the proposed explanation from alternatives. Use existing traces, matched comparisons, informative ablations, or other appropriate evidence; propose an additional test only for a specific unresolved link. Correlated intermediate changes alone do not establish causation or mediation.

Explain where the benefit arises, who or what benefits, when it disappears, and any associated cost or harm. Describe the strongest supported explanation and the remaining hypotheses separately. Turn this into a paper contribution: the empirical finding, the mechanism insight, the scope of the claim, and the figure, table, or example that would communicate it accurately. A larger score needs an explanation of what was learned.

## 6. Synthesize the evidence and maintain the research record

Reconcile the current result with the other experiments in scope. Map each proposed contribution to supporting, contrary, and unresolved evidence. Investigate apparent conflicts rather than silently switching to the most favorable run. Lead the scientific narrative with the strongest credible evidence relevant to the idea, while keeping the scope and selection of that evidence explicit.

Update the maintained dossier with the result classification, diagnosis, corrected understanding, next-step decision, and consequences for the gap, mechanism, contribution, and experiment rationale. Record new background or related-work sources when they inform the explanation, including what was checked and when. Preserve earlier versions and user decisions.

Use the [reflection template](references/reflection-template.md) for the report. Every in-scope run must have an interpretation or an explicit unresolved status. End with a concrete answer: **Does the evidence support the original idea, through which logical links, within what limits, and what should happen next?** If the available evidence cannot determine the cause, identify the precise missing evidence instead of inventing an explanation or running an open-ended search for a favorable result.
