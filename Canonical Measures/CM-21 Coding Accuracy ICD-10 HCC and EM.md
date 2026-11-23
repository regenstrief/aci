# CM-21 Coding Accuracy ICD-10 HCC and EM

**D&M Dimension:** [[OI - Organizational Impact]]

## Definition
The correctness and completeness of diagnostic and billing codes generated or supported by ambient AI documentation, ICD-10 diagnosis codes, HCC (Hierarchical Condition Category) capture for risk adjustment, and E/M (Evaluation & Management) coding level.

## Measurement Methods
| Method | Description | Data Source |
|---|---|---|
| ICD-10 coding compliance (certified coder review) | Expert coders assess code-documentation alignment; standardized rubric | Claims / expert review |
| HCC capture rate | Average HCCs per encounter; ICD-10 → HCC v28 mapping; normalized | Claims / EHR |
| E/M level change (weighted average) | CPT E/M levels 1–5; normalized for case mix; pre vs. post | Claims |
| Real-time ICD-10 accuracy monitoring | Tracking coding accuracy over implementation period | EHR telemetry |
| Claim denial rate | % of encounters with payer denial | Claims |

## Aliases Used in Literature
- ICD-10 Coding Accuracy ([[Afshar 2025 - Novel Playbook for Pragmatic Trial Operations|Afshar 2025]], [[Afshar 2025b - Pragmatic RCT Ambient AI Health Practitioner Wellbeing|Afshar 2025b]]: p<0.001 improvement)
- Diagnostic Billing Compliance ([[Afshar 2025b - Pragmatic RCT Ambient AI Health Practitioner Wellbeing|Afshar 2025b]])
- HCC Capture per Encounter ([[Boyter 2025 - Ambience Healthcare ROI Validations KLAS Report|Boyter 2025]]) *(⚠️ the dollar value of HCC capture (+$9,685/year) is a revenue/financial impact, that financial quantity belongs in CM-20; the capture rate itself may remain here as a coding accuracy metric)*
- E/M Coding Level ([[Boyter 2025 - Ambience Healthcare ROI Validations KLAS Report|Boyter 2025]]) *(⚠️ the dollar value of E/M level change (+$1,907/year) is a revenue/financial impact, belongs in CM-20; the coding level itself may remain here)*
- Claim Denial Rate ([[Holmgren 2026 - Ambient AI Scribes Physician Financial Productivity|Holmgren 2026]]: null, no increase in denials)
- Coding Accuracy ([[Peterson Health Technology Institute 2025 - Adoption AI Healthcare Delivery Systems|Peterson Health Technology Institute 2025]], [[Afshar 2025 - Novel Playbook for Pragmatic Trial Operations|Afshar 2025]])
- Coding Improvement *(⚠️ verify source)*

## ⚠️ Key Note
**Coding improvement is one of the most consistent findings** : appearing in Afshar 2025b (RCT, p<0.001), Boyter/KLAS 2025, and Holmgren 2026. Critically, Holmgren 2026 shows NO increase in denial rate, suggesting coding improvement is legitimate (better documentation of existing complexity, not upcoding). However, PHTI 2025 flags the population-level cost concern regardless.

Bridges IQ (note quality sufficient for accurate coding) and NB (coding accuracy drives revenue and population health metrics).

## Operational Algorithm

### CM-21a — ICD-10 Coding Depth

**Unit:** ICD-10 diagnosis codes per encounter  
**How it works:** Count the number of distinct ICD-10 codes assigned per completed encounter. Average across all encounters in the period. Compare the pre-adoption average to the post-adoption average across the provider cohort. `icd10_codes_per_enc` from Suki's EHR data pull is the preferred field.  
**Delta interpretation:** More ICD-10 codes per encounter after adoption indicates documentation is capturing more diagnoses per visit — a proxy for completeness, not direct accuracy.  
**Watch out for:**
- More codes is not always better — very high counts may indicate overcoding; pair with CM-21c (denial rate) to confirm additional codes are accepted
- Case mix shifts can independently raise diagnosis counts — normalize for specialty or use within-provider comparisons

**Visual sketch:**
```
ICD-10 codes per encounter

4.5 |                    . . . .
4.0 |            . . . .
3.5 |  . . . .
    |
    +---Pre adoption---+---Post adoption--->
```
*Coding depth should trend up slightly — CM-21b and CM-21c are needed to confirm the additional codes are accurate.*

---

### CM-21b — ICD-10 Suggestion Match Rate

**Unit:** Percentage of Suki-suggested ICD-10 codes that appear in final billed codes  
**How it works:** For each completed encounter, retrieve the ICD-10 codes Suki generated (from the `structured-data` API endpoint) and compare them to the final billed ICD-10 codes from the EHR claim record. Divide the count of codes appearing in both lists by the total billed codes. Average across all encounters in the period. This measure requires dedicated pipeline linkage between Suki's API and EHR claim records.  
**Delta interpretation:** A higher match rate indicates Suki's code suggestions are accurate and align with what clinicians ultimately bill.  
**Watch out for:**
- Requires encounter-to-claim linkage not in the standard Suki EHR data pull — confirm pipeline availability with Amita
- Suki may return IMO codes rather than ICD-10 directly; an IMO → ICD-10 mapping step is needed before comparison
- Some code discrepancies are intentional: physicians or billing staff may legitimately add or remove codes during final review

**Visual sketch:**
```
Suki ICD-10 suggestion match rate (%)

90% |                    . . . .
80% |            . . . .
70% |  . . . .
    |
    +---Early use------+---Mature use------>
```
*Match rate should improve as clinicians and Suki align. Target ~85–90% at maturity.*

---

### CM-21c — Claim Denial Rate

**Unit:** Percentage of Level 4–5 claims denied  
**How it works:** Divide the number of denied Level 4–5 claims by total Level 4–5 claims submitted in the period. Track this rate before and after Suki adoption. Focus on Level 4–5 because these are the high-complexity encounters where documentation quality most influences coding accuracy and denial risk. `denial_l45_count` and `total_l45_submitted` are the preferred fields.  
**Delta interpretation:** A stable or declining denial rate alongside rising E/M levels (CM-20c) indicates that higher coding is legitimate — better documentation is supporting the billing, not inflating it.  
**Watch out for:**
- Distinguish coding-related denials from other denial types (authorization, eligibility) — denial reason codes are required
- A rising denial rate alongside rising E/M levels is a warning sign worth investigating
- Small sample sizes produce unstable rates; use rolling windows or quarterly aggregation

**Visual sketch:**
```
Denial rate (% of Level 4-5 claims)

 8% |  . .
 6% |        . . .
 5% |                . . . .
    |
    +---Pre adoption---+---Post adoption--->
```
*Denial rate should stay flat or trend down. Holmgren 2026 found no increase in denials — the key no-upcoding validation.*

---

## Papers Measuring This (6)
- [[Afshar 2025 - Novel Playbook for Pragmatic Trial Operations]]
- [[Afshar 2025b - Pragmatic RCT Ambient AI Health Practitioner Wellbeing]]
- [[Boyter 2025 - Ambience Healthcare ROI Validations KLAS Report]]
- [[Holmgren 2026 - Ambient AI Scribes Physician Financial Productivity]]
- [[Peterson Health Technology Institute 2025 - Adoption AI Healthcare Delivery Systems]]
- [[Billings 2025b - Practicing Value-Based Care with AI]]

---
*Canonical Measures | Suki Literature Review Vault | Derived 2026-03-25, updated 2026-04-15*
*Method: Bottom-up derivation from 494 raw measure rows across 54 papers*

## License

This file is part of the [ACI Structured Evidence Review](https://github.com/regenstrief/aci), licensed under [CC BY-SA 4.0](../LICENSE). If you extend this work, consider contributing back via a pull request.
