<img src="assets/Apoth3osis.webp" alt="Apoth3osis — Formal Mathematics and Verified Software" width="140"/>

<sub><strong>Our tech stack is ontological:</strong><br>
<strong>Hardware — Physics</strong><br>
<strong>Software — Mathematics</strong><br><br>
<strong>Our engineering workflow is simple:</strong> discover, build, grow, learn & teach</sub>

---

<sub>
<strong>Acknowledgment</strong><br>
We humbly thank the collective intelligence of humanity for providing the technology and culture we cherish. We do our best to properly reference the authors of the works utilized herein, though we may occasionally fall short. Our formalization acts as a reciprocal validation—confirming the structural integrity of their original insights while securing the foundation upon which we build. In truth, all creative work is derivative; we stand on the shoulders of those who came before, and our contributions are simply the next link in an unbroken chain of human ingenuity.
</sub>

---

[![License: Apoth3osis License Stack v1](https://img.shields.io/badge/License-Apoth3osis%20License%20Stack%20v1-blue.svg)](LICENSE.md)

# Stack Theory (Bennett 2026) — Delegation Bounds Verified in Lean 4

Lean 4 formalization of Bennett's Stack Theory proving hard combinatorial bounds on delegation in multi-layer intelligence architectures, with bridge theorems connecting weakness ordering to Heyting nucleus fixed-point algebras.

## What This Proves

This formalization machine-checks three central results from Bennett's "Are Biological Systems More Intelligent Than Artificial Intelligence?" (in press, Phil. Trans. B, [arXiv:2405.02325v7](https://arxiv.org/abs/2405.02325)):

1. **Law of the Stack (Theorem 5.1):** Adaptability at layer *i+1* is bounded by 2^|Ext(πᵢ)|. The proof composes a 4-lemma ESM chain: language ≤ pow, ext ⊆ language, utility ≤ language, abstractor ≤ ext.

2. **W-maxing = Free Energy Minimization (Corollary 5.1):** Ordering policies by log-viability-width is equivalent to ordering them by counting free energy. We additionally proved that on dyadic continuation counts (powers of 2), the discrete-log ordering is *exact* — a tightness result not in the original paper.

3. **Cancer-Analogue Splintering (Proposition 6.1):** Over-constraining boundary conditions on a collective causes loss of collective policy — the group fragments into splinters. Every locally feasible policy is forced onto a proper subset of the collective's parts.

### Bridge Theorems (Bennett ↔ Heyting Nucleus)

Six results connect Bennett's combinatorial framework to Heyting algebra nucleus theory. Two are substantive bridge theorems requiring genuine algebraic reasoning; four are infrastructure lemmas (one-line consequences of definitions) that support the bridge.

**Substantive bridge theorems:**

| Theorem | Lean Name | Content |
|---------|-----------|---------|
| **Collective ↔ nontrivial meet** | `collective_identity_yields_nontrivial_meet_in_fixed_locus` | **Central result:** collective identity in Bennett's sense implies nontrivial meet in the Heyting fixed-point algebra Ω_R. ~15-line proof with genuine algebraic witness construction. |
| Abstractor through nucleus | `abstractorThroughNucleus_eq_abstractor_of_fixed` | Nucleus-mediated abstractor collapses to ordinary abstractor when truth sets are already fixed points. |

**Infrastructure lemmas (one-line, definitional):**

| Lemma | Lean Name | Content |
|-------|-----------|---------|
| Weakness monotone on Ω_R | `weakness_monotone_on_fixed_points` | Cardinality monotonicity given a contravariant encoding (1 line: `Finset.card_le_card`) |
| Fixed-policy contravariance | `fixedPolicyEncoding_contravariant` | Extension antitonicity through the fixed-locus encoding (1 line: `ext_mono` application) |
| Weakness on fixed policies | `weakness_monotone_on_fixed_policies` | Combines the above two (1 line: `Finset.card_le_card` on the contravariant encoding) |
| Stable policy inf-closure | `stable_policy_closed_inf` | Fixed-locus closed under intersection via nucleus meet-preservation (1 line: definitional rewrite) |

## Why It Matters

**For AI architecture:** The Law of the Stack imposes combinatorial upper bounds on what multi-layer delegation can achieve. The bound (2^|Ext(πᵢ)|) is exponential in the extension set size — a genuine ceiling, though in practice it may be very loose for concrete architectures. This is not a conjecture — it is a theorem with a machine-checked proof.

**For alignment (hypothesis):** The cancer-analogue splintering theorem proves that over-constraining *abstract* agent objectives causes structural fragmentation within the formalism. This is *analogous* to phenomena observed in RLHF-trained systems (reward hacking, specification gaming), but the formal connection between Bennett's abstract framework and concrete neural architectures is not established by this formalization. Whether real AI systems are instances of Bennett's model is an empirical question, not a proved theorem.

**For mathematics:** The central bridge theorem demonstrates that Bennett's sociological concept of "collective identity" has a precise algebraic characterization as nontrivial meet in a Heyting fixed-point algebra. This connects the sociology of multi-agent systems to abstract algebra in a way that is now machine-verified.

## Formalization Stats

| Metric | Value |
|--------|-------|
| Lean source files | 15 |
| Theorems | 36 |
| Definitions | 38 |
| Lines of Lean | 861 |
| `sorry` count | **0** |
| Bridge theorems (substantive) | 2 |
| Bridge infrastructure lemmas | 4 |
| Core dependencies | 2 (Nucleus.lean, HeytingAlgebra.lean) |

## Build Instructions

Requires Lean 4 v4.24.0 and internet access (pulls Mathlib).

```bash
cd lean
lake build
```

To run sanity checks on all key theorems:

```bash
cd lean
lake build HeytingLean.Tests.StackTheory.AllSanity
```

## Module Map

### Primitives (`StackTheory/Primitives/`)

| File | Contents |
|------|----------|
| `Environment.lean` | `Program`, `Vocabulary`, `truthSet`, `truthSet_union`, `truthSet_empty` |
| `Language.lean` | `Statement`, `language`, `language_card_le_pow` (ESM Lemma 1) |
| `Extension.lean` | `isCompletion`, `extension`, `weakness`, `ext_mono` (contravariance), `ext_subset_language` (ESM Lemma 2) |
| `Task.lean` | `VTask`, `correctPolicies`, `utility`, `utility_le_language` (ESM Lemma 3) |

### Stack (`StackTheory/Stack/`)

| File | Contents |
|------|----------|
| `Abstractor.lean` | `abstractor`, `abstractor_card_le_ext` (ESM Lemma 4), `UninstantiatedTask` |
| `MLA.lean` | `Stack` structure (multi-layer architecture), `isViable` |
| `LawOfTheStack.lean` | `law_of_the_stack` (Theorem 5.1) — 4-lemma calc chain |
| `FreeEnergy.lean` | `ViabilityTask`, `freeEnergy`, `wmaxing_eq_fe_min` (Corollary 5.1), `log_two_order_exact_on_powers_of_two`, `delegation_bottleneck_fe` |

### Collective (`StackTheory/Collective/`)

| File | Contents |
|------|----------|
| `Identity.lean` | `collectivePolicies`, `hasCollectiveIdentity` |
| `BoundaryConditions.lean` | `BoundaryConditions`, `restrictedCollective`, `isOverConstrained`, `feasibleParts`, `isSplinter` |
| `CancerAnalogue.lean` | `overconstraint_implies_splintering` (Proposition 6.1), `overconstraint_yields_splinter` |

### Bridge (`StackTheory/Bridge/`) — 2 Novel Theorems + 4 Infrastructure Lemmas

| File | Contents |
|------|----------|
| `NucleusWeakness.lean` | `weakness_monotone_on_fixed_points`, `FixedPolicies`, `fixedPolicyEncoding_contravariant`, `weakness_monotone_on_fixed_policies`, `StableCollectivePolicy`, `collective_identity_yields_nontrivial_meet_in_fixed_locus`, `stable_policy_closed_inf` |
| `DelegationNucleus.lean` | `abstractorThroughNucleus`, `abstractorThroughNucleus_card_le_extension`, `abstractorThroughNucleus_eq_abstractor_of_fixed` |

### Applications (`StackTheory/Applications/`)

| File | Contents |
|------|----------|
| `AgentHALO.lean` | Concrete 2-layer stack (`haloStack`), `halo_viable`, `halo_agent_bound` |
| `WeakBoundaryDesign.lean` | `weak_boundary_exhibits_global_policy`, `weak_boundary_excludes_splintering`, `overconstrained_design_fragments_local_policy` |

## Import Graph

```
Environment ← Language ← Extension ← Task ← Abstractor ← MLA ← LawOfTheStack
                                       ↑                              ↑
                                  FreeEnergy                   Identity ← BoundaryConditions ← CancerAnalogue
                                                                   ↑
Core.HeytingAlgebra ← NucleusWeakness (bridge: Identity + Task)
Core.Nucleus ← DelegationNucleus (bridge: MLA)
AgentHALO (application: LawOfTheStack + CancerAnalogue)
WeakBoundaryDesign (application: CancerAnalogue)
```

## Full Theorem Inventory

| Paper Reference | Lean Name | File |
|-----------------|-----------|------|
| ESM Lemma 1 | `language_card_le_pow` | `Primitives/Language.lean` |
| ESM Lemma 2 | `ext_subset_language` | `Primitives/Extension.lean` |
| ESM Lemma 3 | `utility_le_language` | `Primitives/Task.lean` |
| ESM Lemma 4 | `abstractor_card_le_ext` | `Stack/Abstractor.lean` |
| Theorem 5.1 (Law of the Stack) | `law_of_the_stack` | `Stack/LawOfTheStack.lean` |
| Corollary 5.1 (w-maxing = FE min) | `wmaxing_eq_fe_min` | `Stack/FreeEnergy.lean` |
| Corollary 5.1 (dyadic exactness) | `wmaxing_eq_fe_min_of_power_of_two` | `Stack/FreeEnergy.lean` |
| Corollary 5.1 (delegation bound) | `delegation_bottleneck_fe` | `Stack/FreeEnergy.lean` |
| Proposition 6.1 (splintering) | `overconstraint_implies_splintering` | `Collective/CancerAnalogue.lean` |
| Proposition 6.1 (splinter construction) | `overconstraint_yields_splinter` | `Collective/CancerAnalogue.lean` |
| Bridge infra: weakness monotonicity | `weakness_monotone_on_fixed_points` | `Bridge/NucleusWeakness.lean` |
| Bridge infra: fixed-policy encoding | `fixedPolicyEncoding_contravariant` | `Bridge/NucleusWeakness.lean` |
| Bridge infra: weakness on fixed policies | `weakness_monotone_on_fixed_policies` | `Bridge/NucleusWeakness.lean` |
| Novel: collective ↔ Ω_R meet | `collective_identity_yields_nontrivial_meet_in_fixed_locus` | `Bridge/NucleusWeakness.lean` |
| Bridge infra: stable policy inf-closure | `stable_policy_closed_inf` | `Bridge/NucleusWeakness.lean` |
| Novel: abstractor through nucleus | `abstractorThroughNucleus_eq_abstractor_of_fixed` | `Bridge/DelegationNucleus.lean` |
| Application: HALO viable | `halo_viable` | `Applications/AgentHALO.lean` |
| Application: HALO agent bound | `halo_agent_bound` | `Applications/AgentHALO.lean` |
| Application: weak boundary global | `weak_boundary_exhibits_global_policy` | `Applications/WeakBoundaryDesign.lean` |
| Application: weak boundary no splinter | `weak_boundary_excludes_splintering` | `Applications/WeakBoundaryDesign.lean` |
| Application: over-constraint fragments | `overconstrained_design_fragments_local_policy` | `Applications/WeakBoundaryDesign.lean` |

## How to Extend

**Adding a new layer type or task variant:**
1. Define the new task structure extending `VTask` in a new file under `Stack/` or `Collective/`.
2. Show it satisfies `correctPolicies` for the relevant vocabulary.
3. Instantiate `Stack` with the new task family (follow `AgentHALO.lean` pattern).

**Adding a new bridge theorem:**
1. Place in `Bridge/` and import `Core.Nucleus` or `Core.HeytingAlgebra` directly.
2. Do NOT define parallel nucleus structure — use the existing `Core.Nucleus` bundle.
3. If encoding policies into a lattice, prove the encoding is contravariant for extensions (follow `fixedPolicyEncoding_contravariant` pattern).

**Adding a new application:**
1. Place in `Applications/` and import the relevant core theorem.
2. Every theorem must do genuine domain reasoning — no re-exports of core theorems with identical hypotheses.

## Source

Bennett, M.T. "Are Biological Systems More Intelligent Than Artificial Intelligence?"
In press, Phil. Trans. B (Royal Society), [arXiv:2405.02325v7](https://arxiv.org/abs/2405.02325), Feb 2026.

## License

[Apoth3osis License Stack v1](LICENSE.md)
