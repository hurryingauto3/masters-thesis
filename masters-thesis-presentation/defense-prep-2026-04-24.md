# Defense Aid

## One-sentence thesis
Under city-disjoint evaluation, end-to-end driving failure is strongly mediated by the visual representation, and in the evaluated settings frozen self-supervised backbones transfer more reliably across cities than supervised baselines.

## Talk order
1. Introduction
2. Background
3. Related work
4. Methodology
5. Experimental results
6. Discussion, industrial implications, and future work
7. Conclusion

## Timing
- Introduction: 5 to 6 minutes
- Background and related work: 4 to 5 minutes
- Methodology: 6 to 7 minutes
- Experimental results: 17 to 19 minutes
- Discussion, industrial implications, future work, and conclusion: 6 to 7 minutes
- Total rehearsed time: 38 to 40 minutes

## Delivery rules
- State the result before explaining the details.
- When showing a matrix, explain rows and columns first.
- When showing a table, point to one comparison only.
- Do not lead with caveats on completed evidence.
- Use caveats only when the contribution boundary or the completion status is directly relevant.
- If interrupted, answer directly, then return to the current slide with one sentence.

## Numbers to memorize
- Published pooled NAVSIM:
  - TransFuser: `83.9 ± 0.4`
  - Latent TransFuser: `83.5 ± 0.6`
  - DiffusionDrive: `88.1`
- Internal v1.1 validation:
  - TransFuser: `83.22`
  - Latent TransFuser: `83.18`
- LAW Boston to Singapore:
  - supervised Swin L2 inflation: `9.77x`
  - frozen I-JEPA ViT-S/14 nuScenes rectangular L2 inflation: `1.20x`
  - collision inflation: `19.34x` to `0.75x`
- Lightweight-head city-disjoint mean:
  - ResNet-34: `57.5`
  - DINOv2: `56.4`
  - I-JEPA: `64.8`
  - MAE: `62.2`
- Matched Boston Latent TransFuser comparison:
  - ResNet-34 probe: `0.968`
  - ResNet-34 OOD loss: `16.1`
  - MAE probe: `0.889`
  - MAE OOD loss: `13.2`
  - I-JEPA probe: `0.833`
  - I-JEPA OOD loss: `9.6`
  - DINOv2 probe: `0.812`
  - DINOv2 OOD loss: `6.3`
- Rank-collapse example:
  - frozen I-JEPA ViT-H/14 rank: `36.6`
  - trainable I-JEPA ViT-H/14 rank: `2.9`
  - probe: `0.94` to `0.38`
- DiffusionDrive matched Pittsburgh comparison:
  - Pittsburgh in-distribution: `58.0` vs `57.8`
  - Singapore PDMS: `41.4` vs `43.2`
  - Pittsburgh to Singapore loss: `16.6` vs `14.6`
  - transfer ratio: `71.4%` vs `74.7%`
  - DAC on Singapore: `61.7` vs `64.1`

## Slide cues

### Introduction

#### `Motivation: pooled evaluation obscures geographic transfer`
- Say: pooled leaderboard numbers are high, but they mix cities in both training and evaluation.
- Say: that measures interpolation inside a known city mixture, not transfer to an unseen city.
- End with the question on the slide.

#### `Open-loop evidence of geographic transfer failure`
- Explain the comparison first: same LAW planner, Boston-trained, tested on Singapore, only the backbone changes.
- Headline: the backbone alone changes L2 transfer inflation from `9.77x` to `1.20x`.
- Interpretation: the visual representation is not a minor implementation detail.

#### `Central claim`
- Read it nearly verbatim.
- Then say: the rest of the talk supports this claim under a minimal head, under open-loop LAW, under closed-loop TF and LatTF, under DiffusionDrive, and then with mechanism.

#### `Thesis contributions and study assets`
- Keep it short.
- Say: the thesis contribution is the evaluation program, the NAVSIM experiments, the DiffusionDrive integration, and the mechanistic analysis.
- Say: LAW and some pretrained checkpoints are external components, not the contribution.

### Background

#### `NAVSIM task and city-disjoint splits`
- Define PDMS in words:
  - NC and DAC are multiplicative safety gates.
  - EP, TTC, and Comfort are averaged.
- Define the four cities.
- Stress Singapore:
  - smallest source city
  - only left-hand-traffic city
  - hardest transfer target

#### `Mixed-city NAVSIM baselines and internal validation`
- This is your credibility slide.
- Say: my internal v1.1 TransFuser and Latent TransFuser runs fall inside the published ranges.
- Then say: that is why the v1.1 cross-city matrix is the canonical thesis record.

### Related Work

#### `Related work and motivating question`
- Keep this simple.
- Say: strong pooled planner results exist, SSL for driving is active, but controlled cross-city planner studies with mechanism are rare.
- End with: the open question is whether cross-city failure is mainly a representation issue once the planner and the source city are controlled.

#### `Drive-JEPA and the shift to geographic transfer`
- Say: the thesis began with pooled NAVSIM and a lightweight head.
- Say: Drive-JEPA showed that pooled NAVSIM is already very strong for JEPA-style models.
- Conclusion: city-disjoint transfer became the right setting for a representation thesis.

### Methodology

#### `Experimental design and transfer metrics`
- Say: the design principle is simple, hold the planner fixed and vary the image backbone.
- Define:
  - open-loop transfer ratio: cross-city error divided by in-distribution error
  - closed-loop OOD PDMS: average PDMS on held-out cities
- Stress: one source-city model is evaluated on every destination city without adaptation.

#### `Backbone families and planner families`
- Move quickly.
- Backbones: supervised, I-JEPA, DINOv2, MAE.
- Planners: LAW, TransFuser, Latent TransFuser, DiffusionDrive.
- Say: this tests the same backbone question under progressively stronger planner assumptions.

#### `Planner selection and comparative roles`
- Explain the sequence.
- Lightweight head:
  - minimal-capacity diagnostic
- TransFuser:
  - standard closed-loop multimodal anchor with a published baseline
- Latent TransFuser:
  - same family, but camera only, so the representation is more exposed
- DiffusionDrive:
  - stronger generative planner that should compress backbone differences

#### `Mechanistic evaluation protocol`
- Use plain definitions.
- Linear probe:
  - a logistic-regression classifier trained on frozen features to predict city identity
- Effective rank:
  - a one-number summary of how many useful directions remain in the feature covariance
- CKA:
  - similarity of covariance structure across feature sets
- MMD:
  - a kernel distance between feature distributions
- Say clearly: probe and rank are the primary evidence, CKA and MMD are supporting diagnostics.

### Experimental Results

#### `Study I: lightweight-head design`
- Say: this is the simplest planner in the thesis, so it is the cleanest way to see whether the backbone already matters.
- Do not oversell it.
- Phrase to use:
  this is a diagnostic study, not the main benchmark.

#### `Study I: pooled lightweight-head results`
- Headline: frozen I-JEPA ViT-H/14 leads at `79.7`.
- Then say: seven of nine frozen SSL variants exceed the supervised ResNet-34 baseline with the same head.

#### `Study I: city-disjoint lightweight-head results`
- Headline: I-JEPA leads every training-city row and the four-city mean at `64.8`, versus `57.5` for ResNet-34.
- Interpretation: the backbone effect is already visible before introducing a strong planner.

#### `Study II: cross-city benchmark design`
- Say: this is the main benchmark of the thesis.
- Two parts:
  - LAW for open-loop transfer ratios
  - TF and LatTF for full closed-loop `4x4` NAVSIM matrices
- Add: all thesis cross-city PDMS values come from the canonical v1.1 matrix.

#### `Study IIa: LAW transfer from Boston to Singapore`
- Headline: same planner, same source city, only the backbone changes, and the transfer inflation changes from `9.77x` to `1.20x`.
- Add the collision number.
- Stop there. Do not over-explain this slide.

#### `Study IIb: TransFuser cross-city transfer`
- Explain the heatmap first.
- Rows are training cities.
- Columns are evaluation cities.
- Diagonal is in-distribution. Off-diagonals are transfer.
- Headline: Singapore is the hardest destination, and frozen SSL stabilizes the off-diagonal cells.

#### `Study IIc: Latent TransFuser cross-city transfer`
- Say: this removes the LiDAR branch, so the image representation is more exposed.
- Headline: the same cross-city structure remains visible in the camera-only planner.

#### `Cross-city NAVSIM: in-distribution and OOD performance`
- Headline: supervised rows fall furthest below the diagonal, while frozen SSL rows stay closer to it.
- This is the compact visual summary of the benchmark.

#### `Cross-city NAVSIM: source-city effects`
- Headline: Boston and Las Vegas are the best source cities, Singapore is the worst.
- Use this when asked whether the result is just a data-volume effect.
- Answer: data volume matters, but it is not the whole story because directional asymmetry also matters.

#### `Cross-city NAVSIM: directional asymmetry`
- Headline: transfer is directional, not symmetric.
- Use Boston to Singapore versus Singapore to Boston as the example.
- Interpretation: there is no single scalar notion of distance that explains all transfer difficulty.

#### `All-city training attenuates backbone differences`
- Headline: pooled training compresses the spread between backbones.
- This is why the thesis does not rely on pooled leaderboard ranking.

#### `Study III: pooled DiffusionDrive results`
- Headline: the generative planner compresses backbone differences, but SSL remains competitive.
- Say: this is the starting point for the generative cross-city test, not the main result by itself.

#### `Study III: cross-city DiffusionDrive transfer`
- State the completion status plainly:
  the thesis currently has three complete training rows.
- Do not apologize.
- Headline: even under this partial record, Singapore is again the weakest destination.

#### `Study III: matched Pittsburgh cross-city comparison`
- This is the slide to narrate carefully.
- Say:
  the Pittsburgh in-distribution scores are essentially matched, `58.0` versus `57.8`.
- Then say:
  under Pittsburgh to Singapore transfer, frozen I-JEPA reaches `43.2` versus `41.4`, so the loss is `14.6` instead of `16.6`.
- End with:
  the gain is concentrated in drivable-area compliance, `61.7` to `64.1`.

#### `Study IV: mechanistic analysis protocol`
- Say: this section asks why the transfer ranking looks the way it does.
- Make the hierarchy explicit:
  - primary: probe and rank
  - supporting: CKA and MMD

#### `Mechanistic evidence: probe accuracy and OOD loss by training city`
- This is your answer to “why are you not just using Boston?”
- Say: Boston, Pittsburgh, and Las Vegas show the expected trend, while Singapore is the exception.
- Interpretation: the mechanism must be read in a training-city-stratified way, not only as one pooled scatter.

#### `Mechanistic evidence: summary across the analysed roster`
- Explain the table once:
  family, status, probe, rank, OOD loss
- Headline:
  the roster-level view supports the same story, but the cleanest causal read still comes from matched comparisons.

#### `Mechanistic evidence: matched Boston comparison`
- This is the clean matched demonstration.
- Say:
  ResNet has probe `0.968` and OOD loss `16.1`.
- Then:
  DINOv2 has probe `0.812` and OOD loss `6.3`.
- Close with:
  within this matched setting, lower city-decodability aligns with better transfer.

#### `What effective rank actually measures`
- Explain this in plain language:
  effective rank measures how spread the feature variance is across directions.
- If the variance lives on only a few directions, the representation has collapsed.
- If it is spread broadly, the representation retains richer structure.

#### `Feature-rank collapse under fine-tuning`
- Headline: fine-tuning can destroy the structure that made SSL useful for transfer.
- Exact statement:
  effective rank drops from `36.6` to `2.9`, and the city probe drops from `0.94` to `0.38`.
- Interpretation:
  freezing is not only a convenience. In this thesis it acts as an empirical regularizer.

### Discussion and Conclusion

#### `Integrated interpretation`
- Summarize the chain:
  lightweight head, LAW, TF, LatTF, DiffusionDrive, mechanism.
- Say:
  the same representation effect survives stronger planners, and the mechanistic section explains why frozen SSL remains more stable.

#### `Industrial implications`
- Lead with:
  this is a deployment problem, not only a benchmark problem.
- Then say:
  if a fleet expands city by city, pooled benchmark strength is not enough.
- Then:
  a frozen SSL backbone is a practical trade-off because it gives up little in distribution and loses less under geographic shift.
- Then:
  the camera-only DiffusionDrive result says stronger vision helps lower-cost stacks, but does not replace geometry.

#### `Contributions and scope of the claim`
- Keep this precise.
- Say:
  the thesis contributes the city-disjoint evaluation program, the planner integrations, and the mechanistic analysis.
- Then say:
  the claim is about representation-mediated transfer, not about planner irrelevance.

#### `Synthesis of the evidence`
- Speak this slide as four sentences, not as a bullet list.
- End with:
  the strongest completed evidence is the TF and LatTF city-disjoint matrix together with the mechanistic matched comparison.

#### `Future work`
- Keep this short.
- Mention:
  video SSL, full DiffusionDrive matrix, interactive simulation, more cities and larger-scale driving pretraining.

#### `Conclusion`
- Read the conclusion almost verbatim.
- Stop after the last sentence.

## Concepts you must be able to explain

### Pooled evaluation
Training and evaluation both use the same city mixture, so the model is interpolating inside a known geographic distribution.

### City-disjoint evaluation
The model is trained on one city and evaluated on a different city without adaptation. This tests transfer to a new operating environment.

### PDMS
PDMS is a rule-based driving score that combines:
- no-fault collisions
- drivable-area compliance
- ego progress
- time to collision
- comfort

NC and DAC are multiplicative, which means severe violations can zero the scenario. That is why PDMS is stricter than plain displacement error.

### Open-loop transfer ratio
Cross-city error divided by in-distribution error. A ratio near `1` means the model retains performance when moved to the new city.

### OOD loss
In-distribution PDMS minus the mean PDMS on held-out cities. Larger loss means worse transfer.

### Linear probe
A simple classifier trained on frozen features. If it can predict the city easily, city identity is strongly encoded in the representation.

### Effective rank
A one-number summary of how many directions carry meaningful variance in the feature covariance. Low rank means collapse onto a small subspace.

### CKA
A similarity measure for covariance structure. It tells you whether two feature sets organize variance similarly, not whether they transfer equally well.

### MMD
A kernel distance between feature distributions. In this thesis it is a diagnostic, not the main mechanistic evidence.

## Design choices you must be able to justify

### Why start with the lightweight head?
Because it is the cleanest way to isolate the representation from planner capacity. If backbone differences are already visible there, the later planner results are easier to interpret.

### Why does Drive-JEPA matter?
Because it showed that pooled NAVSIM performance is already very strong for JEPA-style models. That made pooled PDMS a weak discriminator for a representation thesis and pushed the project toward geographic transfer.

### Why choose TransFuser and Latent TransFuser?
They are strong, recognizable closed-loop baselines. TransFuser is multimodal and published on NAVSIM. Latent TransFuser removes the LiDAR branch, so it exposes the image representation more directly. Together they show that the result is not tied to one exact head.

### Why choose DiffusionDrive?
Because it is a generative planner with stronger built-in priors. If the representation effect survives there, the thesis claim is more robust than if it only held for regression-style planners.

### Why use NAVSIM v1.1 as canonical?
Because the internal v1.1 TF and LatTF reruns land inside the published ranges, so v1.1 is the validated baseline for the thesis matrix.

### Why keep v2.2 at all?
Only for validation context. The same checkpoints shift upward by about two points under v2.2, which indicates a systematic devkit offset rather than a planner-specific error.

### Why use LAW if it is not your method?
Because it is a stable open-loop planner that lets the backbone question be tested cleanly under a fixed planning head.

### Why use these mechanistic tools?
- Linear probe asks whether city identity is explicitly decodable.
- Effective rank asks whether the feature space has collapsed.
- CKA asks whether covariance structure is aligned across cities.
- MMD asks how far the feature distributions move across cities.

Only the first two are load-bearing in the thesis claim.

## Likely questions and short answers

### Anna Choromanska
- Why is this a representation claim rather than an optimization claim?
  Because within the matched studies the planner, training recipe, and evaluation protocol are fixed while the backbone changes. The same ranking then reappears across planners.

- Why does freezing help?
  The rank-collapse result shows that full fine-tuning can compress the feature space and destroy useful pretrained structure. Freezing preserves that structure while still allowing the adapter and planner to learn.

- Why is the mechanistic section important?
  It turns the thesis from a benchmark comparison into an explanation. The matched probe ordering and the rank-collapse evidence explain why some frozen SSL models transfer more gracefully.

### Ludovic Righetti
- Why should PDMS be trusted?
  I use PDMS as a reproducible benchmark proxy, not as a complete deployment guarantee. It is standard in NAVSIM and is paired here with LAW transfer ratios that point in the same direction.

- Why does the DiffusionDrive result matter if the gain is smaller?
  Because DiffusionDrive compresses backbone differences by design. Seeing the same directional result there strengthens the representation argument.

- What exactly fails in Singapore?
  The clearest degradation is in drivable-area compliance and ego progress. NC and TTC remain comparatively stable.

- Why do you say planner choice is secondary?
  Only in the bounded sense supported by the completed studies. The same backbone-dependent ranking appears under LAW, TF, and LatTF, and the available DiffusionDrive rows are consistent with it.

### David Fouhey
- Why use Boston in the matched mechanistic table?
  Because it is the cleanest matched comparison. It is not the only evidence. The full roster table and the training-city-stratified plots use all analysed checkpoints.

- Why is probe accuracy your primary mechanistic variable?
  Because in matched settings it tracks OOD loss directly. I do not claim it is a universal pooled predictor once training city, pretraining source, and backbone scale all vary together.

- Why is MAE somewhat exceptional?
  Because the objective matters beyond city-decodability alone. MAE can remain relatively city-decodable while still transferring well, which is why the thesis does not reduce the mechanism to one scalar.

## If challenged on incomplete DiffusionDrive coverage
- Say:
  the thesis claim does not depend on a fully completed cross-city DiffusionDrive matrix.
- Then say:
  the completed TF and LatTF matrices already establish the main result, and DiffusionDrive is used as an additional planner-family check.
- If pushed further:
  the available rows are still informative because they include a matched Pittsburgh comparison under the same planner and training city.

## If challenged on causal language
- Use this phrasing:
  I am making a bounded causal claim only in matched settings where the planner and the training city are fixed and the backbone is the controlled variable.
- Do not say:
  planner architecture does not matter.

## Emergency fallback answers

### If you forget what CKA is
CKA is a similarity measure for covariance structure. In this thesis it is descriptive, not the main mechanistic proof.

### If you forget what MMD is
MMD is a kernel distance between feature distributions. Here it is a supporting check on cross-city distribution shift.

### If you forget what effective rank is
It is an entropy-based one-number summary of how many directions in feature space are still active.

### If you are asked for the single strongest result
The strongest completed evidence is the TF and LatTF city-disjoint matrix together with the matched Boston mechanistic comparison.

## Appendix map
- `A1` Training recipes
- `A2` Freeze and fine-tune details
- `A3` DiffusionDrive OOD comparison
- `A4` Full exploratory tables
- `A5` Why PDMS remains informative
- `A6` Baseline validation under NAVSIM v1.1
- `A7` Additional Boston-only closed-loop rows
- `A8` Linear probe protocol
- `A9` CKA and MMD diagnostics
- `A10` Confounders
- `A11` Collaboration and provenance
- `A12` ViT primer
- `A13` I-JEPA objective
- `A14` Planner schematics
- `A15` Exploratory experiment matrix

## Final reminders
- The thesis is finished enough to defend on its completed evidence.
- Your main job is to make the structure obvious and the claim precise.
- Results first, mechanism second, caveats only when needed.
