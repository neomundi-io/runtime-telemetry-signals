# Runtime Telemetry Signals

Public signal definitions and methodological guidance for governance-oriented AI runtime observability.

🇫🇷 French version: [README.fr.md](README.fr.md)

---

## What This Repository Explains

NeoMundi produces runtime telemetry signals that help organizations observe how an AI generation behaves while it is being produced.

These signals are designed to support governance decisions such as:

- continuing a generation;
- requesting factual verification;
- regenerating a response;
- routing the request to another model;
- escalating the output to human review;
- documenting a runtime event;
- applying a client-defined stopping policy.

NeoMundi signals do not make governance decisions on behalf of the organization.

They provide measurable information that can be interpreted within a governance policy defined by the system operator, integrator, or regulated organization.

In practical terms:

> NeoMundi measures the runtime behavior.  
> The organization defines the action.

---

## Repository Purpose

This repository documents the public conceptual structure of NeoMundi runtime telemetry signals, including:

- governance-oriented stability states;
- runtime variation signals;
- behavioral observability concepts;
- governance-oriented telemetry artifacts;
- multi-signal interpretation principles;
- possible governance uses;
- methodological and operational boundaries.

Its purpose is to clarify:

- what the signals are intended to represent;
- what they do not claim to represent;
- how signals may be interpreted together;
- how they may support observability and governance workflows;
- which limitations must be considered before defining an operational policy.

This repository does not disclose proprietary implementations, internal weights, inference mechanisms, or protected components of NeoMundi ControlTower.

---

## Core Signal Families

### G-score

**Governance-oriented normalized runtime stability state.**

The G-score represents a normalized condition associated with the stability, regularity, or behavioral coherence of an AI generation or execution state.

It should be interpreted as a runtime stability signal.

It is not proof that an answer is factually correct.

A high G-score may indicate that a generation is stable, regular, or coherent from a runtime perspective. However, a stable generation may still contain an incorrect answer.

This situation is referred to as:

**misleading stability**

Misleading stability occurs when an output appears stable from a runtime perspective but fails an external factual, scientific, legal, or domain-specific validation.

---

### ΔG

**Runtime variation signal associated with changes in generation stability over time.**

ΔG represents the evolution or variation of the runtime stability condition across the generation sequence or between measurement points.

It may contribute to:

- runtime observability;
- behavioral variation monitoring;
- detection of local ruptures;
- identification of transition zones;
- detection of instability or tension areas;
- governance telemetry;
- configurable intervention policies.

ΔG is not:

- a truth score;
- automatic proof of error;
- a reconstruction of the internal cognition of a model;
- a universal semantic validation mechanism;
- an automatic instruction to stop a generation.

A negative or strongly varying ΔG may indicate a degradation or transition in the observed runtime condition. Its operational meaning depends on the context, the associated signals, and the governance policy in place.

---

## Associated Signals and Artifacts

Depending on the campaign, API mode, and integration context, the following signals may be associated with G and ΔG.

### FLAG

A runtime attention signal indicating that an output or generation deserves additional verification, analysis, or escalation.

A FLAG does not automatically mean that an answer is false.

It should be interpreted as an attention signal, not as automatic rejection.

Possible uses include:

- reinforced verification;
- a second validation pass;
- regeneration;
- routing;
- escalation;
- incident documentation.

---

### ALLOW

A governance status indicating that no blocking condition was identified by the configured runtime policy.

ALLOW does not constitute factual certification.

An output may receive an ALLOW status while still requiring external factual, legal, scientific, security, or domain-specific validation.

---

### DROP

A runtime variation profile or event indicating a drop, rupture, strong variation, or tension zone in the observed signal.

A DROP profile should be interpreted together with:

- G-score;
- ΔG;
- FLAG or ALLOW;
- runtime regime;
- coherence signals;
- factual or benchmark validation where relevant.

DROP may support the identification of priority attention zones, but it does not by itself prove that an output is incorrect.

---

### FLAT

A variation profile indicating limited visible movement in the observed runtime stability signal.

A FLAT profile may correspond to regularity or signal saturation.

It should not be interpreted alone as proof of correctness, safety, or reliability.

---

### V_SHAPE

A variation profile indicating an observed drop followed by a partial or more substantial recovery.

This profile may reflect a temporary runtime tension, transition, or recovery pattern.

Its interpretation depends on the amplitude, timing, associated decision, and other available signals.

---

### Runtime regime

A synthetic state describing the broader runtime context of an observed output or execution sequence.

Examples may include stable, transitional, or unstable regimes.

A `STABLE` regime is not sufficient to conclude that a system is:

- safe;
- reliable;
- factually correct;
- compliant;
- ready for automatic execution.

The runtime regime should always be crossed with other signals.

---

### Benchmark accuracy

An external factual validation layer used in selected analysis campaigns.

Benchmark accuracy helps distinguish between situations such as:

- stable and factually correct;
- stable but factually incorrect;
- unstable but potentially correct;
- not detected by runtime telemetry but factually weak;
- requiring reinforced external validation.

Benchmark accuracy is not an internal NeoMundi runtime signal.

It is an external comparison or factual validation layer.

---

### Coherence and factual-risk signals

Depending on the implementation or campaign, runtime observations may also include signals related to:

- semantic coherence;
- factual-risk indicators;
- hallucination-related indicators;
- information density;
- latency;
- token usage;
- energy or cost estimates.

These associated signals provide additional context but should remain interpreted within their measurement boundaries.

---

## From Runtime Signals to Governance Actions

NeoMundi signals are designed to make runtime behavior interpretable within a governance system.

They do not impose a universal decision.

The same signal may lead to different actions depending on:

- the use case;
- the organization’s risk policy;
- the domain;
- the criticality of the output;
- applicable legal or compliance requirements;
- the availability of human review;
- the presence of external factual or retrieval layers.

The following table presents possible governance interpretations.

It is not an automatic decision table and does not define universal production thresholds.

| Observed signals | Possible interpretation | Main risk or limitation | Possible governance action |
| --- | --- | --- | --- |
| High G-score alone | Stable, regular, or runtime-coherent generation | Stability may be confused with factual truth | Cross-check with a factual or domain-specific layer |
| High G-score + high factual accuracy | Stable and externally validated within the tested context | Validation may remain limited to the benchmark or domain tested | Continue according to the applicable policy |
| High G-score + low factual accuracy | Misleading stability: stable but factually incorrect output | Apparent reliability despite factual weakness | Trigger factual verification, grounding, or reinforced review |
| Low or unstable G-score | Runtime fragility, irregularity, or lower stability | Sensitivity to prompt, provider, model, or context | Investigate, regenerate, or apply a second validation pass |
| High ΔG | Strong runtime variation or transition | Local degradation may be overinterpreted as an error | Examine associated G, profile, decision, and context |
| DROP profile | Drop, rupture, or persistent tension zone | DROP alone does not prove factual failure | Classify as a priority attention zone |
| FLAG | Output requires additional attention | FLAG may be mistaken for automatic rejection | Verify, regenerate, reroute, or escalate according to policy |
| FLAG + DROP | Stronger runtime attention zone | Higher probability of unstable or problematic behavior | Prioritize analysis, human review, or configurable intervention |
| FLAG + factually correct output | Attention signal without demonstrated factual error | False assumption that every FLAG is an incorrect answer | Treat as attention, not rejection |
| ALLOW + low factual accuracy | Runtime policy did not identify the factual weakness | Potential false negative if runtime signals are used alone | Reinforce external factual validation |
| STABLE regime alone | Globally stable synthetic runtime context | Limited discriminative value when used alone | Cross with G, ΔG, FLAG, coherence, and factual validation |
| Strong G-score saturation | Concentration near an observed score ceiling | Ambiguity between genuine stability and saturation effect | Test across prompts, providers, repetitions, and configurations |
| Early runtime variation signal | Intervention may be technically possible before completion | The correct action is not determined by the signal alone | Continue, verify, regenerate, reroute, escalate, or stop according to policy |

---

## Exploratory Interpretation Rules

The following rules form a first public grammar for runtime observability and governance.

They should not be understood as:

- definitive production thresholds;
- universal risk classifications;
- automatic enforcement instructions;
- certification rules.

| Rule | Condition | Exploratory interpretation | Possible governance response |
| --- | --- | --- | --- |
| R1 | High G + low factual accuracy | Misleading stability | Add external factual validation |
| R2 | High G alone | Runtime stability, not proof of truth | Never use G alone to validate |
| R3 | FLAG + DROP | Priority runtime attention zone | Escalation, rerouting, or human review |
| R4 | Low G + high ΔG | Potential rupture or transition | Investigate the local runtime sequence |
| R5 | FLAG + correct answer | Alert without demonstrated factual error | Treat as attention, not automatic rejection |
| R6 | STABLE regime alone | Insufficient synthetic signal | Cross with G, ΔG, FLAG, and factual evidence |
| R7 | Stable G + low factual accuracy | Stable but factually weak profile | Add factual or retrieval-based validation |
| R8 | Strong G saturation | Genuine stability or possible ceiling effect | Analyze variability, repetitions, and associated signals |
| R9 | Strong variation across providers | Provider, model, or context sensitivity | Use as a priority comparative test case |
| R10 | One isolated signal | Insufficient decision basis | Apply a multi-signal reading |
| R11 | Early ΔG degradation | Potential intervention point | Apply a client-defined policy, not an automatic universal stop |
| R12 | High FLAG rate in one campaign | Corpus- or configuration-dependent result | Do not generalize without replication |

---

## OBS/GOV-ready Classification

For external integration, signals may be consumed according to their role in an observability or governance architecture.

| Signal or artifact | Suggested category | Recommended use |
| --- | --- | --- |
| G-score | Core runtime signal | Central stability signal, to be interpreted with other signals |
| ΔG / dg_variation | Core runtime signal | Detection of local variation, rupture, or transition |
| FLAG / FLAG rate | Core governance signal | Attention, escalation, reinforced verification, or intervention input |
| ALLOW | Governance status | Indicates no blocking condition under the configured policy, not factual certification |
| Benchmark accuracy | External offline layer | Factual validation or comparative benchmark |
| Runtime regime | Contextual signal | Synthetic reading of runtime context |
| dg_profile | Contextual signal | Interpretable summary of the ΔG evolution pattern |
| Coherence score | Associated signal | Contextualize semantic regularity or degradation |
| Factual-risk indicator | Associated signal | Support reinforced factual review |
| Token position | Operational telemetry | Identify when a runtime event occurs during generation |
| G-score alone | Avoid alone | Risk of confusing stability with factuality |
| Regime alone | Avoid alone | Too synthetic to drive isolated governance decisions |
| FLAG rate alone | Avoid alone | Strong dependence on corpus and experimental conditions |

---

## Multi-signal Reading Examples

### Case 1 — Stable and externally validated

```text
High G-score
Low ΔG
No FLAG
STABLE regime
High benchmark accuracy
```

Possible reading:

The output appears stable and coherent from a runtime perspective and is factually validated within the tested benchmark context.

Possible governance response:

Continue according to the organization’s applicable policy.

---

### Case 2 — Misleading stability

```text
High G-score
Low ΔG
No FLAG
STABLE regime
Low benchmark accuracy
```

Possible reading:

The output appears stable from a runtime perspective but fails external factual validation.

Possible governance response:

Trigger external verification, grounding, retrieval, or reinforced review.

---

### Case 3 — Runtime tension zone

```text
Low G-score
High ΔG
FLAG present
DROP profile
Transitional or unstable regime
```

Possible reading:

The output is associated with a runtime tension, rupture, or transition zone.

Possible governance response:

Regenerate, reroute, escalate to human review, apply a second validation pass, or invoke a configured control mechanism.

---

### Case 4 — Attention signal without factual failure

```text
FLAG present
DROP or V_SHAPE profile
Externally validated correct answer
```

Possible reading:

The runtime signal identified a variation or attention zone, but no direct factual error was demonstrated.

Possible governance response:

Document the event, inspect the runtime sequence, and avoid treating the FLAG as automatic rejection.

---

### Case 5 — Runtime signal not sufficient to detect factual weakness

```text
ALLOW
High G-score
STABLE regime
Low factual accuracy
```

Possible reading:

The runtime signals did not identify the factual weakness.

Possible governance response:

Maintain an external factual, scientific, legal, or domain-specific validation layer.

---

## Actionability of Runtime Signals

A runtime signal is actionable when it is available early enough and consistently enough to support a possible intervention before or immediately after generation.

Possible interventions include:

- continuing generation;
- stopping generation;
- requesting regeneration;
- rerouting to another model;
- triggering factual verification;
- escalating to human review;
- recording an incident or audit artifact.

An exploratory study by Fatima Ezzahrae Gouarab examined whether the first observed negative ΔG point could support a client-side early-stopping policy.

Under the specific conditions studied, the signal was detected before generation completion in most cases, suggesting that runtime intervention may be technically feasible.

However:

- the detection criterion used in the study was exploratory;
- `ΔG < 0` is not an official universal NeoMundi threshold;
- theoretically avoidable tokens are not equivalent to validated cost savings;
- the study did not establish that the response was incomplete, unusable, or incorrect at the detection point;
- the study does not establish that stopping is always the appropriate action.

The main conclusion is therefore:

> Runtime signals may make intervention technically possible.  
> They do not determine which intervention is appropriate.

The consuming organization remains responsible for defining the applicable governance policy.

Exploratory actionability note:

- [Actionability of the NeoMundi ControlTower Runtime Signal](https://doi.org/10.5281/zenodo.21499295)

---

## Reproducibility and Context Dependence

Actionability only has operational value if the underlying signal is sufficiently characterized across repeated and varied conditions.

An exploratory replication study evaluated NeoMundi signals across:

- several execution campaigns;
- multiple providers;
- different generation temperatures;
- classic prompt corpora;
- targeted stress-test corpora;
- expanded prompt categories.

The study found that the observed frequency of FLAG decisions varied substantially depending on the experimental corpus and, to some extent, the provider.

Classic corpora produced low FLAG rates across the tested configurations.

Targeted stress-test corpora produced higher FLAG rates, with differences between providers.

Under the conditions studied, temperature did not appear to be the main determining factor.

The study also reported a consistent relationship between DROP profiles and FLAG decisions across the tested configurations.

These observations support an important distinction:

### Signal prevalence

How frequently a signal appears in a given campaign.

### Signal consistency

Whether associated signals and decisions maintain a coherent relationship across tested configurations.

A signal may remain internally coherent even when its observed prevalence changes across corpora or providers.

Exploratory replication note:

- [Stability and Reproducibility of the NeoMundi ControlTower Runtime Signal](https://doi.org/10.5281/zenodo.21499715)

---

## Context and Reproducibility Boundary

The observed frequency of a runtime signal may depend on:

- the composition of the prompt corpus;
- the nature of the tested situations;
- the provider;
- the model version;
- generation parameters;
- the execution period;
- the measurement protocol;
- the selected detection or aggregation criteria.

A FLAG rate observed in one experimental campaign must not be interpreted as:

- a universal failure rate;
- a general model safety score;
- a provider-wide reliability level;
- a population-level incident rate;
- a direct production-risk estimate.

Stress-test results must be interpreted as measurements obtained under deliberately challenging conditions.

Production policies should be calibrated using:

- representative use cases;
- repeated execution windows;
- known positive and negative controls;
- relevant domain conditions;
- provider and model version tracking;
- external factual or expert validation where necessary.

---

## Actionability Boundary

Runtime detection may make intervention technically possible before generation is complete.

It does not automatically determine whether the system should:

- stop;
- continue;
- regenerate;
- reroute;
- verify;
- escalate;
- document the event.

These actions remain configurable governance choices.

A production intervention policy should consider:

- the criticality of the use case;
- the cost of false positives;
- the cost of false negatives;
- response completeness;
- domain requirements;
- latency constraints;
- human-review availability;
- fallback models or systems;
- evidence-retention requirements.

A signal can therefore be technically actionable without the associated intervention policy being universally validated.

---

## Methodological Position

NeoMundi runtime telemetry signals are governance-oriented observability artifacts.

They are designed to support:

- runtime supervision;
- behavioral observability;
- governance workflows;
- auditability;
- telemetry analysis;
- orchestration systems;
- comparative model analysis;
- detection of tension zones;
- detection of local ruptures;
- detection of misleading stability;
- configurable client-side intervention policies.

They are not intended to:

- reconstruct the internal cognition of a model;
- establish universal semantic truth;
- automatically certify an answer;
- replace legal, medical, scientific, security, or domain expertise;
- produce a universal model ranking;
- define a universal stopping threshold;
- automatically enforce a governance action.

The minimum recommended interpretation combines, where available:

- G-score;
- ΔG or dg_variation;
- FLAG or ALLOW;
- runtime regime;
- ΔG profile;
- coherence or factual-risk indicators;
- an external factual or domain-specific layer when required.

---

## Interpretation Boundaries

A high G-score does not mean that an answer is true.

A low G-score does not automatically mean that an answer is false.

A FLAG does not automatically mean that an answer is false or unusable.

An ALLOW status does not constitute factual certification.

A STABLE regime is not sufficient to conclude that a system is safe or reliable.

A high ΔG does not prove an error.

A DROP profile does not automatically justify blocking an output.

A negative ΔG point is not, by itself, a universal stopping threshold.

A FLAG rate measured in one campaign must not be generalized without replication.

No isolated signal is sufficient to characterize the full risk of a generative output.

Signals must be interpreted together:

- within their usage context;
- with the available evidence;
- under a documented policy;
- with knowledge of the measurement protocol;
- with appropriate domain validation.

---

## Integration into Governance Systems

In an observability architecture, NeoMundi signals may be used to:

- trace generative executions;
- compare behaviors across providers or models;
- identify runtime tension zones;
- monitor behavioral variations;
- detect changes across execution windows;
- produce audit artifacts;
- feed governance dashboards;
- document critical events.

In a governance architecture, they may contribute to configurable decisions such as:

- allow an output;
- request factual verification;
- request regeneration;
- route to another model;
- apply an early-stopping policy;
- escalate to human review;
- open an anomaly or incident;
- preserve evidence for audit;
- initiate a replay or retest workflow.

NeoMundi supplies the measurement and telemetry layer.

The consuming organization defines:

- the applicable thresholds;
- the decision rules;
- the risk policy;
- the intervention strategy;
- the authorization boundary;
- the final operational action.

---

## External Exploratory Studies

The public interpretation of NeoMundi runtime signals has been informed by external exploratory contributor studies.

These studies are methodological contributions.

They do not constitute:

- definitive mathematical validation;
- product certification;
- universal performance claims;
- regulatory approval;
- proof of suitability for every production environment.

### Multi-signal interpretation

An initial external exploratory review was conducted by Pape Malick Diop, Data Scientist and ML Researcher.

The review examined:

- G-score;
- ΔG;
- FLAG;
- runtime regime;
- benchmark accuracy;
- misleading stability;
- multi-signal interpretation;
- OBS/GOV-ready integration.

Related analysis:

- [Runtime signals, misleading stability and the importance of multi-signal reading](https://neomundi.org/observatoire-ia/signaux-temps-reel-stabilite-trompeuse-et-importance-lecture-multi-signaux)

### Signal actionability

Fatima Ezzahrae Gouarab evaluated the exploratory technical feasibility of using NeoMundi runtime signals as inputs to a client-side governance policy during generation.

Study:

- [Actionability of the NeoMundi ControlTower Runtime Signal](https://doi.org/10.5281/zenodo.21499295)

### Signal reproducibility

Fatima Ezzahrae Gouarab also conducted a comparative multi-provider, multi-corpus, and multi-configuration replication study.

Study:

- [Stability and Reproducibility of the NeoMundi ControlTower Runtime Signal](https://doi.org/10.5281/zenodo.21499715)

Together, these contributions document three complementary dimensions:

1. how the signals may be interpreted;
2. how they may support governance actions;
3. under which methodological conditions their interpretation should be replicated and contextualized.

---

## License

This repository is published under the Apache-2.0 license.

---

## About

Public runtime telemetry signal definitions and methodological guidance for governance-oriented AI observability and configurable runtime governance.
