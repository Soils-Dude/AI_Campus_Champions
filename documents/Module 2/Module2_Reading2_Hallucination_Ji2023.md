# Module2_Reading2_Hallucination_Ji2023

# Module 2 — Reading 2 

## Guided reading questions

### Q1 — How does Ji et al. formally define hallucination in NLG? What is the relationship between "faithfulness" and "factuality"?

Ji et al. define hallucination as generated content that is **nonsensical or unfaithful to the provided source content** — text the model produces that isn't grounded in (or that contradicts) its input. They then separate two yardsticks. **Faithfulness** is consistency with the given source/input: a faithfulness hallucination is any output that breaks that consistency, regardless of whether it happens to be true. **Factuality** is correspondence to real-world knowledge: a factuality hallucination is any output that makes a false claim, regardless of the input.

The two can come apart. An output can be **faithful but not factual** (it accurately reflects a source that is itself wrong) or **factual but not faithful** (a true statement the source never actually supported). Much of the NLG literature surveyed frames hallucination primarily as a *faithfulness* problem (stay consistent with the source), while *factuality* is the stricter real-world-truth criterion that matters most when there is no single authoritative source. In my work both apply: a literature summary must be faithful to the cited paper **and** factual about the underlying science.

### Q2 — Difference between intrinsic and extrinsic hallucination? Give one example of each that could occur in an academic document.

**Intrinsic hallucination** = output that directly **contradicts** the source. **Extrinsic hallucination** = output that **cannot be verified** from the source — neither supported nor contradicted, just ungrounded extra content.

  - *Intrinsic example:* I ask the model to summarize a field-trial paper that reported a 5% yield **increase**, and the summary states the treatment **decreased** yield. It contradicts the source.
  - *Extrinsic example:* In a grant background section the model adds, "a 2019 USDA report found cover crops raise soil organic carbon by 0.3% annually" — a specific, plausible claim that appears in none of my sources and can't be traced. (This is the same failure as the fabricated "2019 WWF report" I flagged in Task 3.)

Extrinsic hallucination is usually the **more dangerous** in professional documents: it is fluent and cannot be caught by checking the text against its own source, so it slips past a reader who isn't independently verifying. Intrinsic errors are at least anchored — you can catch them by comparing output to source.

### Q3 — The paper identifies several causes of hallucination in the training process. Which is hardest to mitigate through prompt engineering alone?

Ji et al. trace hallucination to **data causes** — chiefly *source-reference divergence*, where the training data itself pairs a source with a reference containing unsupported information (often a by-product of heuristic or noisy data collection) — and **modeling/inference causes** — imperfect source encoding, erroneous decoding, exposure bias, and the model's *parametric knowledge* overriding the actual input.

The hardest to fix with prompting alone is the **data / parametric** cause: these divergences and false associations are baked into the model's weights during pretraining, and no wording of a prompt removes knowledge the model lacks or un-learns a bias it absorbed. Prompting can nudge decoding behavior (ask for sources, lower the temperature, instruct "use only the provided text"), but closing the underlying knowledge/divergence gap requires **grounding** — retrieval-augmented generation, supplying the source text directly, or fine-tuning on cleaner data. This is exactly why Task 2's chain-of-thought could not remove the invented effect size.

### Q4 — Based on the §2 taxonomy, what type of hallucination would you most need to guard against in your professional tasks?

**Extrinsic factual hallucination** is my top risk. The documents I produce — grant narratives, research summaries for growers and Extension, methods write-ups, and student/staff feedback — are precisely where a model will "helpfully" insert a confident, specific, source-less claim: a fabricated citation, an invented effect size or p-value, a made-up agency report, or a plausible-but-wrong soil threshold. These are fluent and domain-adjacent, so they pass a casual read — the dominant failure mode the module stresses. My routine defense is the Task 3 discipline: extract every named source, number, and causal claim, and treat each as guilty until independently verified — plus grounding the model in real data rather than asking it to recall from memory.

## Key terms — my own definitions

| Term                        | My definition (in my own words)                                                                                                                                                                                                |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Hallucinations (NLG)**    | Text a language model generates that is nonsensical or not grounded in / faithful to its input — confident output that isn't actually supported by the provided material (or by reality).                                      |
| **Intrinsic hallucination** | Generated content that directly contradicts the source it was given (e.g., flips a study's finding from "increase" to "decrease").                                                                                             |
| **Extrinsic hallucination** | Generated content the source neither supports nor contradicts — unverifiable extra information the model added on its own (e.g., a citation or statistic that is in no source).                                                |
| **Faithfulness**            | How well the output stays consistent with the given source/input; a faithful summary says only what the source supports, whether or not it's true in the wider world.                                                          |
| **Factual grounding**       | Tying output to verifiable real-world knowledge (or supplied evidence) so claims can be checked and are actually true — the condition that techniques like RAG aim to provide, and the opposite of a factuality hallucination. |
