# Runtime Telemetry Signals

Public methodological notes and signal definitions for governance-oriented AI runtime observability.

🇫🇷 Version française disponible ici : [README.fr.md](README.fr.md)

---

## Repository Purpose

This repository documents the public conceptual structure of NeoMundi runtime telemetry signals, including:

* governance-oriented stability states;
* runtime variation signals;
* behavioral observability concepts;
* governance-oriented telemetry artifacts;
* methodological interpretation boundaries.

This repository does not disclose proprietary internal implementations, weights, or runtime inference mechanisms from NeoMundi ControlTower.

Its purpose is to clarify:

* what the signals are intended to represent;
* what they do not claim to represent;
* how they may be used within runtime observability and governance systems.

---

## Initial Signal Families

### G

**Governance-oriented normalized stability state.**

The G-score is designed to represent a normalized runtime stability, regularity, or behavioral coherence condition associated with an AI generation or execution state.

It should be read as a **runtime stability signal**, not as proof of factual truth.

A high G-score may indicate that a generation is stable, regular, or coherent from a runtime perspective. However, this stability may coexist with a factually incorrect answer.

This case is referred to as **misleading stability**.

### ΔG

**Runtime variation signal associated with temporal behavioral variation across execution windows.**

ΔG is intended for:

* runtime observability;
* behavioral variation monitoring;
* governance telemetry;
* surfacing instability zones or tension areas;
* identifying local ruptures or behavioral transitions.

ΔG is not:

* a truth signal;
* a cognition reconstruction mechanism;
* a semantic omniscience system;
* automatic proof of error.

---

## Associated Signals

Depending on campaigns and integration contexts, the following signals may be associated with G and ΔG.

### FLAG

Runtime alert signal indicating that an output deserves special attention, reinforced verification, or escalation.

A FLAG does not automatically mean that an answer is false.
It should be interpreted as an attention signal, not as systematic rejection.

### DROP

Profile or event indicating a rupture, drop, strong variation, or tension zone in the observed signal.

A DROP profile should be analyzed together with G, ΔG, FLAG, runtime regime, and, where relevant, an external factual layer.

### Runtime regime

Synthetic state describing the global runtime context of an observed output or sequence.

A `STABLE` regime is not sufficient to conclude that a system is safe, reliable, or factually correct.
The regime should always be crossed with other signals.

### Benchmark accuracy

External factual validation layer used in some analysis campaigns.

It helps distinguish between:

* stable and correct output;
* stable but incorrect output;
* unstable but potentially correct output;
* output requiring additional verification.

Benchmark accuracy is not an internal runtime signal.
It serves as an external comparison and factual validation layer.

---

## Operational Signal Reading

NeoMundi signals should be interpreted through a **multi-signal approach**.

No isolated signal is sufficient to characterize the risk of a generative output.

| Observed signal                     | Interpretation                                                | Main risk                                                      | Recommended action                                                         |
| ----------------------------------- | ------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------------------- |
| High G-score alone                  | Stable, regular, or runtime-coherent generation               | Possible confusion between stability and factual truth         | Do not use G alone to validate an answer; cross-check with a factual layer |
| High G-score + low factual accuracy | Misleading stability: stable but incorrect answer             | Apparent confidence despite factual error                      | Trigger external factual validation or reinforced review                   |
| Low or unstable G-score             | Runtime fragility, irregularity, or less stable behavior      | Output may be sensitive to context, model, or prompt           | Examine the question, provider, and associated variations                  |
| High ΔG or DROP profile             | Strong variation, local rupture, or tension zone              | Runtime transition, punctual instability, or local degradation | Classify as priority attention zone                                        |
| FLAG                                | Runtime alert indicating that an output deserves verification | Overinterpretation as automatic error                          | Use as escalation signal, not as systematic rejection                      |
| FLAG + DROP                         | Stronger runtime risk zone                                    | Increased risk of instability or problematic behavior          | Prioritize analysis; consider human review or second validation pass       |
| STABLE regime alone                 | Synthetic context indicating a globally stable state          | Limited discriminative power if STABLE dominates               | Never use regime alone; cross with G, ΔG, FLAG, and factual accuracy       |
| ALLOW + low factual accuracy        | Case not detected by runtime signal                           | Potential false negative in governance logic                   | Reinforce factual or benchmark layer                                       |
| Strong G-score saturation           | Score concentration around an observed ceiling                | Ambiguity between real stability and saturation effect         | Test robustness across providers, prompts, and repetitions                 |

---

## Actionable Interpretation Rules

These rules form a first exploratory grammar for runtime observability and governance.

They should not be understood as definitive thresholds.

| Rule | Condition                             | Interpretation                        | Recommended action                           |
| ---- | ------------------------------------- | ------------------------------------- | -------------------------------------------- |
| R1   | High G + low factual accuracy         | Misleading stability                  | Add external factual validation              |
| R2   | High G alone                          | Runtime stability, not proof of truth | Never use G alone to validate                |
| R3   | FLAG + DROP                           | Priority runtime risk zone            | Escalation or human review                   |
| R4   | Low G + high ΔG                       | Potential rupture or tension          | Investigate as transition zone               |
| R5   | FLAG + correct answer                 | Alert without direct factual error    | Read as attention, not rejection             |
| R6   | STABLE regime alone                   | Insufficient synthetic signal         | Cross with G, ΔG, FLAG, and factual accuracy |
| R7   | Stable G + low FLAG + low accuracy    | Stable but factually weak profile     | Add factual layer                            |
| R8   | Strong G saturation                   | Strong stability or ceiling effect    | Analyze variability, ΔG, FLAG, and DROP      |
| R9   | Strong G variability across providers | Model or context sensitivity          | Use as priority test case                    |
| R10  | Single signal used alone              | Insufficient decision basis           | Use a multi-signal reading                   |

---

## OBS/GOV-ready Classification

For a first external integration, signals should be consumed according to their role in an observability or governance architecture.

| Signal             | Category         | Recommended use                                                      |
| ------------------ | ---------------- | -------------------------------------------------------------------- |
| G-score            | Required         | Central runtime stability signal, to be crossed with a factual layer |
| ΔG / dg_variation  | Required         | Detection of rupture, tension, or local transition                   |
| FLAG / FLAG rate   | Required         | Alert, escalation, or reinforced verification signal                 |
| Benchmark accuracy | Required offline | External factual validation layer                                    |
| Regime             | Recommended      | Synthetic reading of runtime context, not sufficient alone           |
| dg_profile         | Recommended      | Simplified variation profile, useful for interpretable rules         |
| G-score alone      | Avoid alone      | Risk of confusion between stability and factuality                   |
| Regime alone       | Avoid alone      | Too synthetic to be used as an isolated trigger                      |

---

## Multi-signal Reading Examples

A simple integration may read the signals as follows:

```text
Case 1:
High G-score
Low ΔG
No FLAG
STABLE regime
High benchmark accuracy

Reading:
stable, coherent, and factually validated output within the benchmark context.
```

```text
Case 2:
High G-score
Low ΔG
No FLAG
STABLE regime
Low benchmark accuracy

Reading:
misleading stability.
The output appears stable from a runtime perspective, but fails factual validation.
Recommended action: external validation, reinforced review, or grounding layer.
```

```text
Case 3:
Low G-score
High ΔG
FLAG present
DROP profile
Unstable or transitional regime

Reading:
runtime tension zone.
Recommended action: escalation, human review, second validation pass, or routing to a control mechanism.
```

---

## Methodological Position

NeoMundi runtime telemetry signals are **governance-oriented observability artifacts**.

They are designed to support:

* runtime supervision;
* governance workflows;
* auditability;
* telemetry analysis;
* orchestration systems;
* detection of tension zones, ruptures, or misleading stability.

They are not intended to:

* exhaustively reconstruct the internal cognition of a model;
* establish universal semantic truth;
* automatically certify an answer;
* replace domain-specific, legal, scientific, or factual validation.

The minimum recommended reading combines at least:

* G-score;
* ΔG or dg_variation;
* FLAG;
* regime;
* factual layer or external benchmark when required by the use case.

---

## Interpretation Boundaries

A high G-score does not mean that an answer is true.

A FLAG does not automatically mean that an answer is false.

A STABLE regime is not sufficient to conclude that a system is safe.

A high ΔG does not prove an error, but signals a variation or tension that deserves attention.

Signals must be interpreted together, within their usage context, with the available data and the limits of the measurement protocol.

---

## Integration into Governance Systems

In an observability architecture, the signals may be used to:

* trace generative outputs;
* compare behaviors across providers or models;
* identify tension zones;
* produce audit artifacts;
* monitor runtime variations;
* feed governance dashboards.

In a more advanced governance architecture, they may contribute to configurable decisions, for example:

* allow an output;
* trigger factual verification;
* request regeneration;
* route to another model;
* escalate to human review;
* document a critical event.

These uses should remain configurable, contextualized, and adapted to the risk level of the relevant domain.

---

## External Exploratory Review

An initial external exploratory review of NeoMundi runtime signals was conducted by Pape Malick DIOP, Data Scientist / ML Researcher.

The review analyzes:

* G-score;
* ΔG;
* FLAG;
* runtime regime;
* benchmark accuracy;
* misleading stability;
* OBS/GOV-ready interpretation.

This review is exploratory.
It is neither a definitive mathematical validation nor a product certification.
It proposes a first interpretation grammar and actionable rules for external integration.

Related contributor analysis:

* [Runtime signals, misleading stability and the importance of multi-signal reading](https://neomundi.org/observatoire-ia/signaux-temps-reel-stabilite-trompeuse-et-importance-lecture-multi-signaux)

---

## License

This repository is published under the Apache-2.0 license.

---

## About

Public runtime telemetry signal definitions and methodological notes for governance-oriented AI observability.
