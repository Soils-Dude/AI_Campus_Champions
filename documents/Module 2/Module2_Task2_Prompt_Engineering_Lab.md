# Module2_Task2_Prompt_Engineering_Lab

# Module 2: Generative AI — Task 2: Prompt Engineering Lab (Four-Iteration Refinement)

## My target task (specific)

> Draft the \~150-word "Specific Aims" paragraph for a USDA-NIFA grant proposal investigating how winter cover-crop mixtures affect soil organic carbon (SOC) and water-holding capacity in irrigated, arid-land cropping systems in Arizona. **Audience:** a USDA-NIFA review panel (soil scientists + program officers). **Purpose:** convince reviewers the aims are significant, measurable, and fundable.

## Version 1 — Zero-shot

**Prompt (verbatim):**

> Write a Specific Aims paragraph for a grant proposal about cover crops and soil health.

**Output (summary):** "Cover crops are an important practice for improving soil health. This project will study how cover crops affect the soil and benefit farmers. We will plant cover crops and measure changes in the soil over time, such as organic matter and structure. The goal is to help growers adopt practices that make soils healthier and more sustainable…"

**Quality: 2/5.** Two weaknesses: (1) no operationalized, measurable aims or hypothesis — nothing a reviewer could score or fund; (2) no system specificity (crop, region, soil property, timeframe) — it could describe any project anywhere, and leans on filler ("important," "such as").

## Version 2 — + Role specification

**Prompt (verbatim):**

> You are a soil scientist and funded USDA-NIFA principal investigator who specializes in soil organic carbon dynamics in irrigated, arid-land cropping systems. Write a Specific Aims paragraph for a grant proposal about cover crops and soil health.

**Output (summary):** "Cover cropping is a promising strategy for enhancing soil organic carbon (SOC) and soil function in irrigated arid-land systems, where low baseline organic matter limits productivity. This project will evaluate how winter cover-crop mixtures influence SOC accrual, aggregate stability, and water-holding capacity in irrigated desert cropping systems…"

**Quality: 3/5.** What improved vs. V1: discipline-appropriate vocabulary (SOC fractions, aggregate stability, water-holding capacity) and an arid-system framing; the generic hedging is gone. Still missing: numbered, measurable aims and a testable hypothesis.

## Version 3 — + Few-shot example

**Prompt (verbatim):**

> You are a soil scientist and funded USDA-NIFA principal investigator who specializes in soil organic carbon dynamics in irrigated, arid-land cropping systems.
> 
> Here is an example of the quality and structure I want, from a previously funded proposal:
> 
> "Example — Specific Aims: Salinity threatens 20% of irrigated cropland in the desert Southwest. We propose to (1) quantify how gypsum amendment rate alters the sodium adsorption ratio across three soil textures, (2) test whether amendment improves infiltration using tension-infiltrometer measurements, and (3) model the economic break-even point for growers. We hypothesize that gypsum at 4 t/ha will reduce SAR below 6 within two irrigation seasons. Outcomes will give Arizona growers a decision tool grounded in field-measured data."
> 
> Now, in that style, write a Specific Aims paragraph for a grant proposal about cover crops and soil health.

**Output (summary):** "Irrigated cropping in the arid Southwest is carbon-poor, limiting water retention and resilience. We propose to (1) quantify SOC accrual — total, particulate, and mineral-associated fractions — under three winter cover-crop mixtures versus fallow across two soil textures; (2) test whether cover cropping increases field water-holding capacity using in-situ sensors and laboratory water-release curves; and (3) determine the irrigation-water-savings break-even point for growers. We hypothesize that a legume–grass–brassica mixture will raise mineral-associated carbon by ≥10% within three seasons. Outcomes give Arizona growers a field-validated decision tool."

**Quality: 4/5.** What improved vs. V2: the example imported a concrete structure — numbered, measurable aims, an explicit quantitative hypothesis, and active voice — plus specific methods (MAOC fractionation, sensors, water-release curves). **This was the single biggest jump.**

## Version 4 — + Chain-of-thought

**Prompt (verbatim):**

> \[All of the Version 3 prompt above\] — then append:
> 
> Before writing, think step by step through: (1) Who is the audience? (2) What is the single most important point? (3) What tone is appropriate? Then produce the output.

**Output — the visible reasoning chain is diagnostically useful:**

> "Reasoning: (1) Audience — a USDA-NIFA panel of soil scientists and program officers who reward measurable aims, intellectual merit, and grower impact. (2) Most important point — that cover crops can build durable, mineral-associated carbon AND improve water-holding capacity under arid irrigated conditions, where this is not yet demonstrated. (3) Tone — confident, technical, hypothesis-driven."
> 
> "Specific Aims: Irrigated cropping in the arid Southwest is carbon-poor, constraining water retention and climate resilience, and whether winter cover crops can build durable soil carbon under high-evaporation desert conditions remains unresolved. We will (1) quantify SOC accrual by fraction (total, particulate, mineral-associated) under three cover-crop mixtures versus fallow across two textures; (2) measure resulting gains in water-holding capacity via in-situ sensors and laboratory water-release curves; and (3) identify the irrigation-water-savings break-even point for growers. We hypothesize a legume–grass–brassica mixture will increase mineral-associated carbon ≥10% within three seasons while improving plant-available water. Deliverables include a field-validated decision tool for Arizona producers."

**Quality: 5/5 (marginal gain over V3).** What improved vs. V3: the explicit audience step foregrounded reviewer priorities and added a crisp knowledge-gap sentence; prose tightened. The gain is real but small — evidence that technique is calibration, not accumulation.

## Iteration summary

| Version | Technique added       | Quality | Single biggest change                                           |
| ------- | --------------------- | ------- | --------------------------------------------------------------- |
| V1      | Zero-shot             | 2 / 5   | Baseline: vague, unmeasurable, generic.                         |
| V2      | \+ Role specification | 3 / 5   | Upgraded vocabulary; removed hedging.                           |
| V3      | \+ Few-shot example   | 4 / 5   | Imported numbered, measurable aims + hypothesis (biggest jump). |
| V4      | \+ Chain-of-thought   | 5 / 5   | Audience-targeted framing; tighter prose (marginal gain).       |

## 150-word reflective note

The few-shot example (V3) produced the single biggest improvement. Adding a role (V2) changed the register — it swapped generic phrasing for domain vocabulary like "mineral-associated carbon" and "aggregate stability" — but it did not change the structure, which stayed a shapeless paragraph. The example did: it imported a numbered, three-aim skeleton with measurable endpoints and an explicit quantitative hypothesis, transforming an essay into a reviewable proposal. Chain-of-thought (V4) added a smaller, qualitative gain — the visible reasoning step made the model foreground the USDA panel's priorities and add a knowledge-gap sentence — consistent with Wei et al. (2022): CoT helps multi-step reasoning, but aims-writing is partly templating, which the example already supplied. What remains unresolved: every version invented a plausible but ungrounded "≥10%" effect size. Prompt engineering did not fix that hallucination risk; only substituting my real pilot data will.

> **Cross-link to Task 3.** The "≥10%" figure is an *extrinsic hallucination* — fluent, specific, and unverifiable. No prompt technique removed it; factual grounding has to come from real data. This is the discipline the hallucination audit builds.
