# Defense Aid

## Talk spine
- Main claim: under city-disjoint evaluation, geographic failure in end-to-end driving is strongly mediated by the visual representation.
- Main empirical result: frozen self-supervised backbones transfer more reliably across cities than supervised baselines when the planner and training city are controlled.
- Main mechanistic result: in matched settings, better transfer aligns with lower city-decodability and with preservation of feature rank under freezing.
- Main scope statement: this is not a claim that planner architecture never matters. It is a claim about the dominant effect seen in the completed studies.

## Timing
- Rehearsed target: 38 to 40 minutes.
- Introduction and setup: 6 to 7 minutes.
- Methodology and lightweight-head study: 6 to 7 minutes.
- Cross-city benchmark and DiffusionDrive: 15 to 17 minutes.
- Mechanistic analysis: 8 to 9 minutes.
- Discussion and conclusion: 4 to 5 minutes.

## Delivery rules
- State the result first, then explain how it was obtained.
- Do not lead with caveats on completed evidence.
- When a slide has a matrix, explain rows and columns before interpreting it.
- When a slide has a table, point to one row and one comparison only.
- Use exact numbers for the headline comparisons.
- If a question asks for the strongest evidence, answer with the completed TF and LatTF city-disjoint matrices plus the matched Boston mechanistic comparison.
- If a question asks for generative-planning evidence, answer with the pooled DiffusionDrive table and the matched Pittsburgh cross-city comparison.

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
  - frozen I-JEPA ViT-S/14 nuScenes rect L2 inflation: `1.20x`
  - collision inflation: `19.34x` to `0.75x`
- Lightweight-head city-disjoint mean:
  - ResNet-34: `57.5`
  - DINOv2: `56.4`
  - I-JEPA: `64.8`
  - MAE: `62.2`
- Matched Boston LatTF comparison:
  - ResNet-34 OOD loss: `16.1`
  - MAE ViT-B/16 frozen OOD loss: `13.2`
  - I-JEPA ViT-H/14 frozen OOD loss: `9.6`
  - DINOv2 ViT-S/14 frozen OOD loss: `6.3`
  - ResNet probe accuracy: `0.968`
  - DINOv2 probe accuracy: `0.812`
- Rank-collapse example:
  - all-city I-JEPA ViT-H/14 frozen rank: `36.6`
  - all-city I-JEPA ViT-H/14 trainable rank: `2.9`
  - corresponding probe accuracy: `0.94` to `0.38`
- DiffusionDrive matched Pittsburgh comparison:
  - in-distribution: `58.0` vs `57.8`
  - Singapore PDMS: `41.4` vs `43.2`
  - Pittsburgh to Singapore loss: `16.6` vs `14.6`
  - transfer ratio: `71.4%` vs `74.7%`
  - DAC on Singapore: `61.7` vs `64.1`

## Slide-by-slide notes

### 1. Title
- One sentence opener:
  This thesis studies cross-city generalization in end-to-end driving and asks whether geographic failure is primarily a representation problem once the planner is controlled.

### 2. Outline
- Say that the talk follows the thesis chapter structure.
- Tell them the center of gravity is the experiments section.

### 3. Motivation: pooled evaluation obscures geographic transfer
- Point out that pooled leaderboard numbers are high.
- Say clearly: these numbers measure interpolation within a known city mixture, not transfer to an unseen city.
- Close with the question on the slide.

### 4. Open-loop evidence of geographic transfer failure
- Explain the plot first: Boston-trained, tested on Singapore, same LAW planner, only the backbone changes.
- Headline:
  the representation alone changes L2 transfer inflation from `9.77x` to `1.20x`.
- Interpret:
  this is why the thesis does not treat backbone choice as a minor implementation detail.

### 5. Central claim
- Read the claim almost verbatim.
- Do not elaborate yet.
- Say:
  the rest of the talk shows this pattern under a minimal head, open-loop LAW, closed-loop TF and LatTF, and then interprets it mechanistically.

### 6. Thesis contributions and study assets
- Keep this brisk.
- Say:
  the external pieces are LAW and certain pretrained checkpoints; the evaluation design, NAVSIM experiments, DiffusionDrive integration, and mechanistic analysis are thesis contributions.
- Then move on. Do not dwell here.

### 7. Background divider
- Transition only.
- Say:
  I will define the benchmark and the controls before showing the main studies.

### 8. NAVSIM task and city-disjoint splits
- Define PDMS in words:
  safety and drivable-area compliance enter multiplicatively, while progress, TTC, and comfort are averaged.
- Explain the four cities.
- Emphasize Singapore:
  smallest source city, only left-hand-traffic domain, hardest transfer target.

### 9. Mixed-city NAVSIM baselines and internal validation
- Use this as a credibility slide.
- Say:
  my internal v1.1 TF and LatTF reruns preserve the paper ordering and land inside the reported ranges.
- Then say:
  that is why the v1.1 cross-city matrix is the canonical record for the thesis.

### 10. Related Work divider
- Transition only.

### 11. Related work and motivating gap
- Keep it short.
- Say:
  pooled planner benchmarks are strong, SSL is widely used, but controlled cross-city planner studies with mechanism are rare.
- End with:
  the gap is not whether planners can score well, but why transfer fails once the city changes.

### 12. Methodology divider
- Transition only.

### 13. Experimental design and transfer metrics
- This is the control slide.
- Say:
  I hold the planner fixed and vary the image backbone.
- Define:
  open-loop error ratio and closed-loop OOD PDMS.
- Stress:
  one source-city model is evaluated on every destination city without adaptation.

### 14. Backbone families and planner families
- Move quickly.
- Backbones:
  supervised ResNet or Swin, plus I-JEPA, DINOv2, and MAE.
- Planners:
  LAW, TransFuser, Latent TransFuser, DiffusionDrive.
- Say:
  this lets me test the same backbone question under increasingly strong planner priors.

### 15. Experiments divider
- Transition only.

### 16. Study I: lightweight-head design
- Explain why this exists:
  minimal planner capacity makes representation differences visible without a strong planner masking them.
- Say:
  this is a diagnostic study, not the main benchmark.

### 17. Study I: pooled lightweight-head results
- Headline:
  frozen I-JEPA ViT-H/14 leads at `79.7`.
- Then:
  seven of nine frozen SSL variants exceed the supervised ResNet-34 baseline.
- Use this as the first evidence that the ranking exists before the planner becomes sophisticated.

### 18. Study I: city-disjoint lightweight-head results
- Headline:
  I-JEPA leads every training-city row and the four-city mean by `7.3` points over ResNet-34.
- Explain that Singapore compresses all methods downward.
- Say:
  the representation pattern is already visible under a very weak head.

### 19. Study II: cross-city benchmark design
- This is the core setup slide.
- Say:
  Study II has an open-loop LAW view and a closed-loop NAVSIM view.
- Emphasize:
  full `4x4` city matrices for TF and LatTF under v1.1.

### 20. Study IIa: LAW transfer from Boston to Singapore
- Headline:
  with the planner fixed, the representation alone changes transfer inflation from `9.77x` to `1.20x`.
- Add the collision figure:
  `19.34x` to `0.75x`.
- Interpretation:
  the representation effect is not subtle in open-loop transfer.

### 21. Study IIb: TransFuser cross-city transfer
- Explain how to read the heatmap.
- Point out:
  diagonals are in-distribution, off-diagonals are transfer, Singapore column is darkest.
- Say:
  frozen SSL rows stabilize the off-diagonal entries.

### 22. Study IIc: Latent TransFuser cross-city transfer
- Say:
  this removes the LiDAR shortcut and leaves the visual representation more directly exposed.
- Headline:
  the same cross-city structure remains visible without the LiDAR branch.

### 23. Cross-city NAVSIM: in-distribution and OOD performance
- Explain the diagonal line once.
- Headline:
  supervised rows fall furthest below the diagonal, strongest frozen SSL rows remain closer.
- Say:
  this compresses the whole benchmark into one picture.

### 24. Cross-city NAVSIM: source-city effects
- Headline:
  Boston and Las Vegas are the strongest source cities; Singapore is the weakest.
- This is useful for committee questions about data scale and city structure.

### 25. Cross-city NAVSIM: directional asymmetry
- Headline:
  transfer is directional, not symmetric.
- Say:
  Boston to Singapore is harder than Singapore to Boston.
- Interpret:
  cross-city failure is not explained by a single scalar notion of distance.

### 26. All-city training attenuates backbone differences
- Headline:
  pooled all-city training compresses the backbone spread.
- Interpretation:
  this is why the thesis centers city-disjoint evaluation rather than mixed-city ranking.

### 27. Study III: pooled DiffusionDrive results
- Headline:
  under pooled evaluation, the generative planner compresses backbone differences and SSL stays within about `1` to `2` points of the supervised baseline.
- Use this as the setup for the cross-city generative test.

### 28. Study III: cross-city DiffusionDrive transfer
- Be precise:
  the current thesis record includes three fully evaluated training rows.
- Headline:
  even with this partial matrix, Singapore is again the weakest destination.
- Do not apologize for partial coverage. Just state the available evidence and move on.

### 29. Study III: matched Pittsburgh comparison
- This is the one DiffusionDrive slide to narrate carefully.
- Say:
  in-distribution performance is nearly matched, `58.0` versus `57.8`.
- Then say:
  under Pittsburgh to Singapore transfer, frozen I-JEPA reaches `43.2` versus `41.4`, which reduces the loss from `16.6` to `14.6`.
- Close with:
  the gain is concentrated in DAC, `61.7` to `64.1`, while NC and TTC remain comparable.

### 30. Study IV: mechanistic analysis protocol
- Say:
  this section asks not only whether SSL transfers better, but what property of the learned representation is changing.
- Define the primary tools:
  probe accuracy and effective rank.
- Define the auxiliary tools:
  CKA and MMD.

### 31. Mechanistic evidence: probe accuracy and OOD loss by training city
- This is your answer to “why only Boston?”
- Say:
  Boston, Pittsburgh, and Las Vegas show the expected trend; Singapore is the exception.
- Interpret:
  training city is a confounder, so the correct read is stratified rather than pooled.

### 32. Mechanistic evidence: summary across the analysed roster
- Explain the table structure:
  family, frozen or trainable status, probe, rank, OOD loss.
- Headline:
  trainable supervised rows sit at the high-probe, large-loss corner; frozen MAE and DINOv2 occupy the lower-loss side.
- Use this slide when asked whether the mechanism generalizes beyond one matched example.

### 33. Mechanistic evidence: matched Boston comparison
- This is the cleanest matched causal read.
- Headline:
  the ordering of probe accuracy matches the ordering of OOD loss.
- Exact statement:
  ResNet has probe `0.968` and loss `16.1`, DINOv2 has probe `0.812` and loss `6.3`.

### 34. Feature-rank collapse under fine-tuning
- Headline:
  fine-tuning can destroy the structure that makes SSL useful for transfer.
- Exact statement:
  rank drops from `36.6` to `2.9`, and probe accuracy drops from `0.94` to `0.38`.
- Interpretation:
  freezing is not only a training convenience, it is an empirical regularizer.

### 35. Discussion divider
- Transition only.

### 36. Integrated interpretation
- Summarize the chain:
  minimal head, LAW, TF, LatTF, DiffusionDrive, mechanism.
- Say:
  the same result appears under progressively stronger planners, then the mechanistic section explains why frozen SSL remains more stable.

### 37. Contributions and scope of the claim
- Keep this calm and exact.
- Say:
  the thesis contributes the city-disjoint evaluation program, the planner integrations, and the mechanistic analysis.
- Then say:
  the claim is about representation-mediated transfer, not about planner irrelevance.

### 38. Synthesis of the evidence
- This is your closing evidence slide.
- Speak it as four sentences, not as a list.
- End with:
  the strongest completed evidence is the TF and LatTF city-disjoint matrix together with the mechanistic matched comparison.

### 39. Conclusion
- Read the closing claim almost verbatim.
- Stop after that.

## Concepts to define clearly if asked
- Pooled evaluation:
  training and evaluation use the same city mixture, so it measures interpolation inside the benchmark mixture.
- City-disjoint evaluation:
  a model is trained on one city or one source set and evaluated on a different city without adaptation.
- PDMS:
  a rule-based rollout score combining safety, drivable-area compliance, progress, TTC, and comfort, with NC and DAC entering multiplicatively.
- Open-loop transfer ratio:
  transfer error divided by in-domain error.
- OOD PDMS loss:
  in-distribution PDMS minus the mean held-out-city PDMS.
- Linear probe:
  a multinomial logistic-regression classifier applied to frozen features.
- Effective rank:
  the entropy-based rank of the feature covariance, used to measure collapse onto a small subspace.
- CKA:
  a similarity measure for covariance structure across feature sets.
- MMD:
  a kernel-based distance between feature distributions.

## Questions Anna Choromanska may ask
- Why is this a representation claim instead of an optimization claim?
  Because the planner, training recipe, and evaluation protocol are held fixed while the backbone changes. The ranking then repeats across several planners and is interpreted with matched mechanistic comparisons.
- Why is freezing important?
  The rank-collapse slide shows that full fine-tuning can compress the feature space and remove useful pretrained structure. Freezing preserves the geometry that transfers.
- Why does the mechanism section matter?
  It turns the thesis from a benchmark comparison into an explanation. The matched Boston table and the rank-collapse evidence show why some frozen SSL models degrade more gracefully.

## Questions Ludovic Righetti may ask
- Why should PDMS be trusted?
  I use PDMS as a reproducible benchmark proxy, not as a deployment guarantee. It is standard in NAVSIM and is paired here with open-loop LAW ratios that point in the same direction.
- Why should the DiffusionDrive result matter if the effect is smaller?
  Because DiffusionDrive has a stronger planner prior and compresses backbone differences. Seeing the same directional pattern there makes the representation argument more robust.
- What exactly goes wrong in Singapore?
  The most visible degradation is in drivable-area compliance and ego progress, while NC and TTC remain comparatively stable.

## Questions David Fouhey may ask
- Why is Boston still used in the matched table?
  Because it is the cleanest matched comparison. But it is no longer the only evidence: the main mechanistic plot is stratified by training city and the roster summary covers the full analysed set.
- Why is probe accuracy the main mechanistic variable?
  Within matched settings, it tracks OOD loss directly. I do not claim that it is a universal predictor once city, backbone scale, and pretraining source all vary together.
- Why is MAE an exception?
  MAE suggests that the objective matters beyond city-decodability alone. It can remain relatively city-decodable while still transferring well.

## If challenged on incomplete DiffusionDrive coverage
- Say:
  the thesis claim does not depend on a fully populated cross-city DiffusionDrive matrix.
- Then say:
  the completed TF and LatTF matrices already establish the main result, and DiffusionDrive is used as an additional generative-planner test.
- If pushed:
  the current available rows are still informative because they include a matched Pittsburgh comparison under the same planner and training city.

## If challenged on causal language
- Use this phrasing:
  I am making a bounded causal claim only in matched settings where the planner and training city are fixed and the backbone is the controlled variable.
- Do not say:
  planner architecture does not matter.

## If asked why v1.1 is canonical
- Say:
  the internal v1.1 TF and LatTF reruns fall inside the published ranges, so v1.1 is the validated baseline used for the cross-city matrix.
- If needed:
  the v2.2 shift is systematic across both architectures and does not change the ordering.

## Appendix map
- A1 and A2:
  training recipe and freeze or fine-tune details.
- A3:
  DiffusionDrive OOD bars.
- A4:
  full lightweight-head pooled tables.
- A5:
  why PDMS is still informative.
- A6:
  v1.1 baseline validation.
- A7:
  additional Boston-only LatTF rows.
- A8:
  exact linear-probe protocol.
- A9:
  why CKA and MMD are auxiliary.
- A10:
  confounders.
- A11:
  collaboration and provenance.

## Final reminders
- Speak like the thesis is finished, because the defended story is finished.
- The main evidence is already enough without the full DiffusionDrive matrix.
- Do not oversell. Exact, bounded, completed evidence is stronger than broad claims.
