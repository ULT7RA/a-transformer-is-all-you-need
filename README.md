# A Transformer Is All You Need

**Per-Weight, Per-Layer Causal Decision Attribution for Pretrained Transformers**

**Author:** Marc Lamoureux · Promethean Systems
**Contact:** prometheansystems@proton.me · +1 (720) 449-6984
**Published:** June 2026
**DOI:** [10.5281/zenodo.20906442](https://doi.org/10.5281/zenodo.20906442)
**Discussion:** [Hacker News](https://news.ycombinator.com/item?id=48683684)
**License:** [CC BY 4.0](LICENSE)

---

## Abstract

The unanswered question in mechanistic interpretability of pretrained transformers is plain: *for any prompt and any decoder-only transformer, which weights at which layers along which residual-stream dimensions produced the decision the model emitted?* Activation probing reports a per-depth accuracy curve. Sparse dictionaries decompose activations into monosemantic features. Logit and tuned lenses trace the trajectory of a prediction through the residual stream. None of these names the weight that did the work. The weights are the artifact training produced, the substrate every activation must traverse, the only object in the system that persists across forward passes; interpretability that treats them as a fixed backdrop describes what the model is doing right now, never *why this particular model with these particular weights had to do it*.

We close that gap with one primitive — the alignment of a residual-stream activation with the top singular directions of a weight matrix, scaled by the singular values — and a small cross-layer transformer (the **hybrid weight–activation probe**) that consumes the joint (activation, alignment) sequence and predicts the host model's next-token decision. As a byproduct of training, the probe exposes per-layer importance (the depth at which the host's decision crystallized) and per-layer alignment importance over the three weight families Q/K/V, attention output, and MLP up/gate (which family at each layer carried the decisional signal, and via the SVD along which singular directions). A separate gradient-attribution pass through the host model closes the causal loop, confirming the weights the probe identifies are the same weights whose perturbation moves the host's logit on that decision.

**The pipeline answers, for any prompt on any frozen pretrained decoder-only transformer, the question every prior interpretability tool has had to leave open: which weight, at which layer, along which dimensions, produced this token.**

## Demonstration

The pipeline is demonstrated on four structurally distinct decoder-only transformers spanning five years of architectural and training evolution:

| Host | Year | Params | Architecture |
| --- | --- | --- | --- |
| GPT-2 medium | 2019 | 355M | original GPT-2 (LayerNorm, MHA, GELU) |
| Pythia 2.8B | 2023 | 2.8B | the Pile, rotary, GELU |
| Mistral 7B v0.1 | 2023 | 7.3B | SwiGLU, RMSNorm, GQA, sliding-window |
| LLaMA 3 8B base | 2024 | 8B | SwiGLU, RMSNorm, GQA, 128K tiktoken, 15T tokens |

On all four hosts the probe converges well above the `1/1024 ≈ 0.001` random baseline. The per-weight-family attribution proportions on all four hosts lie within ℓ₁ distance **0.019** of the uniform `[1/3, 1/3, 1/3]` vertex of the 2-simplex, with a maximum pairwise ℓ₁ separation of **0.034**. This reproducibility observation is reported as a downstream finding of running the pipeline on the panel, not as the central claim.

## Nine capability families

From the single primitive of weight-level causal decision attribution follow:

1. **Visibility.** Per-prompt decision pathway, layer by layer; per-weight-family contribution breakdown; plain-language translation of internal state.
2. **Diagnostics.** Causal attribution from any activation back to the specific weights that produced it; decision-crystallization layer detection; cross-architecture invariants empirically measured; frozen-checkpoint analysis with no runtime required.
3. **Intervention.** Weight-level targeted editing. Behavior reinforcement, removal, suppression. No RLHF, no preference data, no reward model. Surgical, not behavioral.
4. **Capability operations.** Localization, extraction, transplantation, removal of specific capabilities at the structural substrate.
5. **Security and forensics.** Backdoor detection. Sleeper-agent detection at the weight level. Tampering and post-training-modification detection. Provenance and output forensics. Distillation-source detection.
6. **Safety-specific detection.** Deceptive alignment, sandbagging, hidden goals, evaluation awareness, sycophancy, pressure deception, reward-hacking circuits, specification gaming — all located in the structural substrate, not inferred from behavior.
7. **Training economics.** Cost compression by skipping training of weights not contributing to a target capability. Targeted fine-tuning. Capability-preserving compression.
8. **Cross-lab audit capability.** Audits any transformer family — GPT, Gemini, LLaMA, Mistral, Claude, any future architecture. Same method, no rebuild. Substrate for third-party audit by AISI, NIST, government procurement. Industry-wide safety-standard enforcement.
9. **Comparative analysis.** Model-to-model structural comparison. Architecture-family comparison. Training-method comparison. Checkpoint evolution. Fine-tune drift detection. Merge-component attribution.

## Citation

```bibtex
@misc{lamoureux2026transformer,
  author       = {Lamoureux, Marc},
  title        = {A Transformer Is All You Need: Per-Weight, Per-Layer Causal Decision Attribution for Pretrained Transformers},
  year         = {2026},
  month        = {June},
  publisher    = {Zenodo},
  doi          = {10.5281/zenodo.20906442},
  url          = {https://doi.org/10.5281/zenodo.20906442}
}
```

## Contents

- `TransformerIsAllYouNeed.pdf` — full manuscript
- `LICENSE` — Creative Commons Attribution 4.0 International (CC BY 4.0)

## Contact

For collaboration, audit engagements, or technical questions:
**prometheansystems@proton.me** · **+1 (720) 449-6984**

---

© 2026 Marc Lamoureux. Released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
