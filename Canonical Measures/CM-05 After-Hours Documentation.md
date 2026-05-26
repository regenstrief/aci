# CM-05 After-Hours Documentation

**D&M Dimension:** [[II - Individual Impact]]

## Definition
Time spent on clinical documentation outside of scheduled working hours, 'pajama time', 'after-hours EHR', or 'work outside work.' Distinct from total documentation time (CM-04) because it captures work-life boundary effects specifically. One of the most clinically meaningful outcomes because it directly affects physician well-being.

## Measurement Methods
| Method | Description | Data Source |
|---|---|---|
| EHR audit-log (Epic Signal / UAL) | Objective after-hours documenting time; normalized to scheduled hours | EHR telemetry |
| Work Outside Work (WoW) | Hours/day documenting outside scheduled hours (Afshar 2025b) | EHR telemetry |
| Self-report (survey) | Clinician-estimated reduction in after-hours documentation | Survey |
| After appointment date | % notes completed on a date after the appointment date | EHR telemetry |
| After-hours EHR time (% change) | Change in after-hours time as % of baseline | EHR telemetry |

## Aliases Used in Literature
- After-Hours EHR Time ([[Haberle 2024 - Impact Nuance DAX Ambient Listening AI Documentation|Haberle 2024]], [[Cao 2024 - Artificial Intelligence-Driven Digital Scribes Dermatology|Cao 2024]], [[Peterson Health Technology Institute 2025 - Adoption AI Healthcare Delivery Systems|Peterson Health Technology Institute 2025]], [[Ma 2025 - Ambient AI Scribes Utilization Documentation Time Stanford|Ma 2025]])
- Pajama Time ([[Peterson Health Technology Institute 2025 - Adoption AI Healthcare Delivery Systems|Peterson Health Technology Institute 2025]])
- Work Outside Work / WoW ([[Afshar 2025b - Pragmatic RCT Ambient AI Health Practitioner Wellbeing|Afshar 2025b]])
- After-Hours Documentation ([[Boyter 2025 - Ambience Healthcare ROI Validations KLAS Report|Boyter 2025]], [[AAFP 2021 - Using AI Assistant Reduce Documentation Burden Family Medicine|AAFP 2021]], [[Albrecht 2025 - Ambient AI Clinical Documentation QI Survey|Albrecht 2025]], [[Duggan 2025 - Clinician Experiences Ambient Scribe Documentation Burden|Duggan 2025]])
- After Hours Time Spent Documenting per Appointment ([[Stults 2025 - Evaluation Ambient AI Documentation Platform Clinicians|Stults 2025]])
- Time After Appointment Date ([[Boyter 2025 - Ambience Healthcare ROI Validations KLAS Report|Boyter 2025]])
- Decreased After-Hours Documentation ([[Albrecht 2025 - Ambient AI Clinical Documentation QI Survey|Albrecht 2025]])
- After-Hours Note Writing ([[Albrecht 2025 - Ambient AI Clinical Documentation QI Survey|Albrecht 2025]])
- Out-of-Hours EHR Documentation Time ([[Suhail 2026 - Metrics for Ambient Clinical Documentation Scoping Review|Suhail 2026]])
- Decreased EHR Time at Home ([[Stults 2025 - Evaluation Ambient AI Documentation Platform Clinicians|Stults 2025]])
- Off-Hours EHR Activity ([[Stults 2025 - Evaluation Ambient AI Documentation Platform Clinicians|Stults 2025]])

## ⚠️ Key Note
**Consistent null pattern in objective data:** After-hours time does NOT improve significantly in EHR telemetry across most corpus papers (Pearlman 2025, Stults 2025). Self-report shows improvement. Exceptions: Duggan 2025 (−16.9%), Boyter/KLAS 2025 (−39% UAL), Afshar 2025b (−0.50 hrs/day, but fragile: disappears after removing top 3% outliers). **Tierney 2025** adds one of the strongest objective signals in the corpus: DiD reduction in pajama time (−1.03 min, p=0.02) and time outside 7am–7pm (−1.83 min, p<0.001). This self-report/objective divergence remains one of the most reproducible findings.

## Operational Algorithm

**Unit:** Minutes per provider per month (after-hours EHR time)  
**How it works:** Sum all EHR activity for each provider that falls outside scheduled working hours each month. Compare each provider's average monthly after-hours total before Suki adoption to after adoption. Average across the provider cohort. `after_hours_min` from Epic Signal/UAL is the preferred field.  
**Delta interpretation:** Lower after-hours minutes per month after adoption indicates providers are completing notes during clinic hours rather than at home or after the workday.  
**Watch out for:**
- Objective EHR telemetry shows smaller and less consistent improvements than self-report — do not conflate the two
- The effect is highly sensitive to outliers: Afshar 2025b's result disappears after removing the top 3% of high-time users
- Ensure equal numbers of working days in pre and post windows when using monthly totals
- Some after-hours activity is non-documentation (inbox, orders) and may not respond to Suki

**Visual sketch:**
```
After-hours EHR time (min/month)

200 |  . . .
150 |        . .
100 |            . .
 50 |                . .
    |
    +---Pre adoption---+---Post adoption--->
```
*After-hours time should trend down — but the effect is smaller and noisier than CM-04.*

---

## Papers Measuring This (19)
- [[AAFP 2021 - Using AI Assistant Reduce Documentation Burden Family Medicine]]
- [[Afshar 2025 - Novel Playbook for Pragmatic Trial Operations]]
- [[Afshar 2025b - Pragmatic RCT Ambient AI Health Practitioner Wellbeing]]
- [[Albrecht 2025 - Ambient AI Clinical Documentation QI Survey]]
- [[Billings 2025a - Ambient AI Assistant Transforms Primary Care Experience]]
- [[Boyter 2025 - Ambience Healthcare ROI Validations KLAS Report]]
- [[Cao 2024 - Artificial Intelligence-Driven Digital Scribes Dermatology]]
- [[Duggan 2025 - Clinician Experiences Ambient Scribe Documentation Burden]]
- [[Evans 2025 - AI Scribe Allied Health Private Practice Australia]]
- [[Haberle 2024 - Impact Nuance DAX Ambient Listening AI Documentation]]
- [[Karavassilis 2025 - Ambient Voice Technology Same Day Emergency Care SDEC]]
- [[Liu 2024 - AI Powered Clinical Documentation Clinicians EHR Experience]]
- [[Ma 2025 - Ambient AI Scribes Utilization Documentation Time Stanford]]
- [[Pearlman 2025 - AI Scribe EHR Efficiency]]
- [[Peterson Health Technology Institute 2025 - Adoption AI Healthcare Delivery Systems]]
- [[Stults 2025 - Evaluation Ambient AI Documentation Platform Clinicians]]
- [[Suhail 2026 - Metrics for Ambient Clinical Documentation Scoping Review]]
- [[Tierney 2025 - Ambient AI Scribes Learnings 1 Year 2.5 Million Uses]]
- [[Billings 2025b - Practicing Value-Based Care with AI]]

---
*Canonical Measures | Suki Literature Review Vault | Derived 2026-03-25, updated 2026-04-15*
*Method: Bottom-up derivation from 494 raw measure rows across 54 papers*

## License

This file is part of the [ACI Structured Evidence Review](https://github.com/pbiondich/aci), licensed under [CC BY-SA 4.0](../LICENSE). If you extend this work, consider contributing back via a pull request.
