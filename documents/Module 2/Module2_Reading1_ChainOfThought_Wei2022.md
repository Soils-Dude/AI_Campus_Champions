# Module2_Reading1_ChainOfThought_Wei2022

# Module 2 — Reading 1 Worksheet

## Guided reading questions

### Q1 — What exactly is added to a prompt to make it a "chain-of-thought" prompt? Reproduce the structure of Figure 1 in your own words.

In ordinary few-shot prompting, each worked example is just a *question → final answer* pair. To make it chain-of-thought, you insert a **rationale** between the question and the answer: a short series of natural-language intermediate steps that show how you get from one to the other. Each exemplar becomes *question → reasoning steps → answer*. The question itself is unchanged; what is added is the demonstrated "show your work" trace.

Figure 1 places the two side by side. In the **standard** column, the example answers a tennis-ball word problem with a bare "The answer is 11," and the model then answers a new cafeteria-apples question wrong ("The answer is 27"). In the **chain-of-thought** column, the same example spells out the steps ("Roger started with 5 balls; 2 cans × 3 = 6; 5 + 6 = 11; the answer is 11"), and the model imitates that pattern on the new question — "23 − 20 = 3; 3 + 6 = 9; the answer is 9" — and gets it right. The only new ingredient is the reasoning trace in the exemplar.

### Q2 — CoT benefits are "emergent" — they appear only in sufficiently large models. What does this imply for practitioners using smaller or older LLMs?

CoT only beats standard prompting once a model is large enough — roughly **100B parameters (\~10²³ training FLOPs)** in their experiments. Below that scale, adding step-by-step exemplars produces fluent-looking but frequently illogical chains and yields little or no accuracy gain — sometimes it even underperforms standard prompting. The practical implication: if you are using a small, distilled, on-device, or older model, you cannot assume CoT will rescue a hard multi-step task. Test it head-to-head rather than applying it as a ritual, and reserve CoT for the larger frontier models (which is exactly where Task 1's comparison and Task 2's lab used it). A flat or negative CoT result on a small model is expected behavior, not evidence that you "prompted it wrong."

### Q3 — The paper tests CoT on arithmetic, symbolic, and commonsense reasoning. Which is most analogous to tasks you perform professionally?

For my soil/agricultural field-research work, the closest analog is **arithmetic / symbolic reasoning** — the multi-step quantitative chains I run constantly: converting soil-test values into fertilizer or amendment rates, propagating units from a bulk-density measurement into a carbon-stock figure (SOC % → Mg C ha⁻¹ using depth and bulk density), computing a sodium adsorption ratio, or working through an experimental-design and statistical-power argument. Each has explicit intermediate steps where a single slip cascades into a wrong result — precisely the structure CoT targets. **Commonsense reasoning** maps better to the interpretive and writing side of my job (deciding what a result means for a grower, or drafting a recommendation), where laying out audience and purpose helps but the "correct answer" is fuzzier.

### Q4 — What is the key limitation of the few-shot CoT approach identified by the authors? Does it apply to your Task 2 use case?

The authors are explicit that **a chain of thought is no guarantee of correct reasoning**: the model can produce a confident, well-formed reasoning trace that still reaches a wrong answer, and they caution that CoT only *emulates* reasoning without establishing that the network is actually reasoning — improving the factual correctness of these generations is left as open work. (They also note hand-writing CoT exemplars is an annotation cost, and that the benefit only emerges at large scale.)

Yes, this applies directly to my Task 2 grant-aims use case. In V4 the model produced a tidy reasoning chain and still inserted an ungrounded "≥10%" effect size. The reasoning *looked* sound, but the number was fabricated — exactly the "fluent chain, unverified content" failure Wei et al. flag, and the hallucination problem covered in Reading 2. The lesson: use CoT to structure the work, but independently verify every factual claim the chain emits.

## Key terms — my own definitions

| Term                           | My definition (in my own words)                                                                                                                                                               |
| ------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Chain-of-thought prompting** | Showing the model worked examples that include the intermediate reasoning steps — not just the final answer — so it imitates that step-by-step pattern on a new problem.                      |
| **Zero-shot prompting**        | Asking the model to do a task with no worked examples at all — just the instruction or question (optionally "think step by step"), relying on what it already learned in training.            |
| **Few-shot prompting**         | Putting a handful of example input→output pairs in the prompt so the model infers the pattern and applies it to the new input, with no retraining.                                            |
| **Reasoning chain**            | The explicit sequence of intermediate steps (the rationale) that connects a question to its answer — the "show your work" trace the model is shown or generates.                              |
| **Emergent ability**           | A capability that is largely absent in small models and appears, often abruptly, only once the model passes a certain scale; CoT's reasoning benefit is one such ability (\~100B parameters). |
