# CM-19 Clinical Patient Safety

**D&M Dimension:** [[OI - Organizational Impact]]

## Definition
Actual or potential patient harm associated with ambient AI documentation, including documentation errors that affect clinical decisions, adverse events, harm scores, and gaps between documented symptoms and clinical action.

## Measurement Methods
| Method | Description | Data Source |
|---|---|---|
| [AHRQ Harm Score](https://journals.lww.com/journalpatientsafety/abstract/2015/03000/the_reliability_of_ahrq_common_format_harm_scales.8.aspx) | Validated harm classification for medical errors | EHR / expert review |
| Adverse events / patient safety events | Formal incident reporting or EHR-identified events | EHR / administrative |
| Likelihood of psychiatric intervention (aOR) | Association between AI scribe use and clinical action | EHR data (observational) |
| Patient safety survey items | Provider-reported safety concerns | Survey |

## Aliases Used in Literature
- AHRQ Harm Score ([[Anderson 2025 - Quality Safety Ambient Digital Scribe Platforms Simulation|Anderson 2025]]: mean 3.0 errors/case with potential for moderate-to-severe harm, AHRQ ≥2)
- Patient Safety Events ([[Anderson 2025 - Quality Safety Ambient Digital Scribe Platforms Simulation|Anderson 2025]]; [[Suhail 2026 - Metrics for Ambient Clinical Documentation Scoping Review|Suhail 2026]])
- Adverse Events ([[Lukac 2025 - RCT Two Ambient AI Scribes Documentation Efficiency Burnout|Lukac 2025]]: one Grade 1 mild event across study period; no serious events)
- Patient safety event tracking ([[Haberle 2024 - Impact Nuance DAX Ambient Listening AI Documentation|Haberle 2024]]: no safety events attributable to DAX)
- Likelihood of Psychiatric Intervention ([[Castro 2025 - Psychiatric Documentation Treatment Primary Care AI Scribe|Castro 2025]]: aOR 0.83, p=.005) *(a documented-symptoms-to-clinical-action gap: retained under the harm definition)*
- Patient Safety (survey) ([[Guo 2026 - Evaluating Ambient AI Documentation UCI Health Mixed Methods|Guo 2026]]: pre 3.72 → post 4.03, p=.027) *(perception-based, not event-based)*

## ⚠️ Key Note
**Castro 2025 is the landmark paper here:** More psychiatric symptom *documentation* but significantly *less* psychiatric *intervention* (aOR 0.83) with ambient scribe use, preprint only, but the only paper measuring what happens to patients clinically. This is a potential unintended consequence with serious safety implications. Only 6 papers touch this dimension under the strict-harm scope, and most use simulated or survey data rather than real patient outcomes.

**Scope narrowed (2026-07):** Definition now requires actual or potential patient harm. Error-severity measures without a demonstrated patient outcome were reclassified to CM-09 (Bracken 2025, Moramarco 2022, Wang 2021 removed from this list; Biro 2025 and Bundy 2024 alias rows relocated). Castro 2025's RDoC and PHQ-9 documentation measures moved to CM-08; its psychiatric-intervention measure remains here as a documented-symptoms-to-clinical-action gap. Guo 2026's survey measure is retained but flagged as perception-based.

## Papers Measuring This (6)
- [[Anderson 2025 - Quality Safety Ambient Digital Scribe Platforms Simulation]]
- [[Castro 2025 - Psychiatric Documentation Treatment Primary Care AI Scribe]]
- [[Guo 2026 - Evaluating Ambient AI Documentation UCI Health Mixed Methods]]
- [[Haberle 2024 - Impact Nuance DAX Ambient Listening AI Documentation]]
- [[Lukac 2025 - RCT Two Ambient AI Scribes Documentation Efficiency Burnout]]
- [[Suhail 2026 - Metrics for Ambient Clinical Documentation Scoping Review]]

---
*Canonical Measures | Suki Literature Review Vault | Derived 2026-03-25, updated 2026-04-15*
*Method: Bottom-up derivation from 494 raw measure rows across 54 papers*

## License

This file is part of the [ACI Structured Evidence Review](https://github.com/pbiondich/aci), licensed under [CC BY-SA 4.0](../LICENSE). If you extend this work, consider contributing back via a pull request.
