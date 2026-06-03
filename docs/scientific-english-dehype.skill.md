---
name: scientific-english-dehype
description: Edit English scientific manuscripts so that claims are supported by data rather than hype, LLM-style filler, or unsupported evaluative language. Use this when drafting, revising, or polishing abstracts, papers, grants, cover letters, and responses to reviewers.
---

# Scientific English De-Hype Skill

## Purpose

Write scientific English in which the claim is carried by the evidence, not by decorative adjectives. The goal is not to make prose flat; the goal is to make it precise, credible, and difficult for reviewers to dismiss as overclaiming or AI-polished.

## Background

Scientific writing has increasingly used promotional language. Vinkers, Tijdink, and Otte (BMJ, 2015) reported that the use of positive words in PubMed abstracts rose sharply between 1974 and 2014, with positive words increasing by about 880%. This pattern was interpreted as reflecting increasing rhetorical inflation rather than a simple increase in the quality of scientific findings.

LLM-assisted writing has introduced a second, newer signal: generic style words that sound polished but often add little scientific content. Kobak et al. (Science Advances, 2025; arXiv:2406.07016) analyzed more than 15 million PubMed abstracts from 2010–2024 and found abrupt post-ChatGPT increases in style words such as *delves*, *underscores*, *showcasing*, *potential*, *crucial*, and *pivotal*. Their excess-word analysis estimated that at least 13.5% of 2024 PubMed abstracts had been processed with LLMs. The estimate is a lower bound, because texts edited with LLMs may not contain the marker words used in the analysis.

## Core principle

> Data should do the persuasive work. Adjectives should not compensate for weak evidence.

When revising, match the strength of the wording to the strength of the evidence. A claim may be strong only when the design, sample size, statistics, replication, or mechanistic evidence supports it.

## Red-flag vocabulary

These words are not banned. They are prompts to check whether the sentence is relying on tone instead of evidence.

### Hype or promotional words

Avoid or justify words such as:

- *outstanding*
- *excellent*
- *remarkable*
- *unprecedented*
- *groundbreaking*
- *innovative*
- *novel*
- *robust*
- *compelling*
- *promising*
- *significant* when used casually rather than statistically

Use these only when the sentence states the basis for the evaluation. For example, *novel* is acceptable when the exact novelty is identified; *robust* is acceptable when robustness analyses, sensitivity analyses, or replication results are reported.

### LLM-style filler or ornamental words

Treat the following as signals to revise:

- *delve*, *delves*, *delving*, *delved*
- *pivotal*
- *intricate*
- *meticulous*, *meticulously*
- *showcase*, *showcases*, *showcasing*
- *underscore*, *underscores*
- *crucial*
- *comprehensive*
- *notably*
- *insights*
- *realm*
- *landscape*
- *multifaceted*
- *nuanced*
- *seamless*
- *harness*
- *leverage*

These words often make a sentence sound fluent while leaving the scientific content unchanged.

## Revision test

For every evaluative adjective, adverb, or ornamental verb, ask:

1. If I delete this word, does the scientific information change?
2. If information is lost, can I replace the word with a measurement, comparison, method, or result?
3. If no information is lost, should I remove the word?
4. Does the strength of the wording match the strength of the evidence?

A useful rule:

> If deleting the adjective removes no data, the adjective was probably decoration.

## Preferred replacements

Replace praise with measurable claims.

| Avoid | Prefer |
|---|---|
| *outstanding performance* | *accuracy increased from 71% to 83%* |
| *remarkable improvement* | *the error rate decreased by 18%* |
| *robust results* | *the association remained after adjustment for age, sex, and baseline severity* |
| *novel method* | *a method that combines X with Y; previous approaches used X alone* |
| *pivotal role* | *blocking X reduced Y by 42%, suggesting that X contributes to Y* |
| *meticulously delves into* | *examines* or *tests* |
| *showcasing the effectiveness of* | *showing that* / *we found that* |
| *intricate interplay* | *interaction* / *association* / *mechanism*, depending on the evidence |

## Editing workflow

### 1. Identify the claim

Find the main claim of each sentence or paragraph. Ask what the reader must believe after reading it.

### 2. Identify the evidence

Attach the claim to specific evidence: effect size, confidence interval, p value, sample size, experimental design, validation set, replication, negative control, sensitivity analysis, or qualitative observation.

### 3. Remove decorative wording

Delete hype words and LLM-style filler unless they contribute precise meaning. Replace vague praise with concrete information.

### 4. Calibrate the claim

Use cautious language when evidence is limited.

- Use *suggests*, *is consistent with*, or *may indicate* for observational, exploratory, or underpowered results.
- Use *shows*, *demonstrates*, or *establishes* only when the design supports a strong inference.
- Avoid causal verbs such as *drives*, *prevents*, or *leads to* unless the study design supports causality.

### 5. Prefer simple verbs

Scientific prose usually improves when ornamental verbs are replaced with direct verbs.

| Ornamental | Direct |
|---|---|
| *delve into* | *examine*, *analyze*, *test* |
| *showcase* | *show*, *report* |
| *underscore* | *show*, *support*, *highlight* |
| *leverage* | *use* |
| *facilitate* | *enable*, *help*, *allow* |
| *elucidate* | *clarify*, *identify*, *test* |

### 6. Final human pass after AI drafting

AI can be used to generate or revise a draft, but the final version should be checked by the author. Remove unsupported evaluation, verify factual claims, check citations, and ensure that numerical results rather than tone carry the argument.

## Examples

### Example 1

Before:

> Our novel model achieved outstanding performance and provides remarkable insights into disease progression.

After:

> Our model increased AUROC from 0.74 to 0.82 on the external validation set and identified age, baseline severity, and biomarker X as the strongest predictors of progression.

### Example 2

Before:

> This comprehensive study meticulously delves into the intricate relationship between inflammation and cognition.

After:

> This study tested the association between inflammatory markers and cognitive scores in 1,240 participants.

### Example 3

Before:

> These findings underscore the pivotal role of pathway X in tumor growth.

After:

> Inhibition of pathway X reduced tumor volume by 31% in the xenograft model, supporting a role for pathway X in tumor growth.

### Example 4

Before:

> The results demonstrate that treatment A prevents relapse.

After, if the study is observational:

> Treatment A was associated with a lower relapse rate after adjustment for baseline severity and prior treatment history.

After, if the study is a well-powered randomized trial:

> Treatment A reduced relapse risk compared with placebo over 12 months.

## Checklist before submission

- Every strong claim is paired with data.
- Every use of *novel*, *robust*, *remarkable*, *unprecedented*, or *significant* is justified or removed.
- LLM-style filler such as *delve*, *pivotal*, *intricate*, *meticulous*, and *showcasing* has been removed or replaced with precise wording.
- Causal language is used only when supported by the study design.
- The abstract reports concrete results rather than promotional interpretation.
- The final text sounds like the author’s scientific judgment, not generic AI-polished prose.

## References

- Vinkers CH, Tijdink JK, Otte WM. *Use of positive and negative words in scientific PubMed abstracts between 1974 and 2014: retrospective analysis.* BMJ. 2015;351:h6467. doi:10.1136/bmj.h6467.
- Kobak D, González-Márquez R, Horvát E-A, Lause J. *Delving into LLM-assisted writing in biomedical publications through excess vocabulary.* Science Advances. 2025;11(27):eadt3813. Preprint: arXiv:2406.07016.
