# CM-22 Patient Volume and Throughput

**D&M Dimension:** [[OI - Organizational Impact]]

## Definition
Changes in the number of patients seen per unit time or changes in patient flow through clinical environments, a downstream efficiency outcome of reduced documentation burden. Includes ED metrics (door-to-doc, length of stay) and outpatient productivity (encounters per week).

## Measurement Methods
| Method | Description | Data Source |
|---|---|---|
| Patients seen per hour | Encounter throughput | Operational / scheduling |
| Encounters per week | Ambulatory visit volume per physician per week | Claims / EHR |
| Door-to-doc / door-to-room time (min) | ED patient flow metric | Operational |
| Length of stay (admitted / discharged, min) | ED throughput metric | Operational |
| Ability to add patient | % reporting ability to see additional patients | Survey |

## Aliases Used in Literature
- Patients Seen per Hour ([[Shuaib 2021 - Scribe Program Patient Throughput Physician Productivity|Shuaib 2021]]: +39%) *(moved from CM-18)*
- Encounters per Week ([[Holmgren 2026 - Ambient AI Scribes Physician Financial Productivity|Holmgren 2026]]: +0.80/week)
- Door-to-Doc Time ([[Shuaib 2021 - Scribe Program Patient Throughput Physician Productivity|Shuaib 2021]])
- Door-to-Room Time ([[Shuaib 2021 - Scribe Program Patient Throughput Physician Productivity|Shuaib 2021]])
- Length of Stay, Admitted / Discharged ([[Shuaib 2021 - Scribe Program Patient Throughput Physician Productivity|Shuaib 2021]])
- Patients Through ([[Shuaib 2021 - Scribe Program Patient Throughput Physician Productivity|Shuaib 2021]]) *(⚠️ Shuaib's "Productivity (%)" label is misleading, this is patient throughput, not physician productivity in a financial/RVU sense)*
- Ability to Add Patient ([[Albrecht 2025 - Ambient AI Clinical Documentation QI Survey|Albrecht 2025]])
- I Feel Able to See More Patients ([[Duggan 2025 - Clinician Experiences Ambient Scribe Documentation Burden|Duggan 2025]]) *(moved from CM-18)*

## ⚠️ Key Note
Only 6 papers measure throughput, and the strongest data is from Shuaib 2021 (human scribe, ED), a baseline comparator, not an ambient AI study. Holmgren 2026 found +0.80 encounters/week with ambient AI adoption (statistically significant). Note: increased patient volume may not be desirable if it increases workload without compensation.

**⚠️ "Patients seen" vs. "closed encounter count":** Suki's spreadsheet measures "total closed encounter count," which requires the note to be signed — stricter than a raw appointment count or check-in/check-out count. This is actually the more precise definition: an encounter is not complete until the chart is closed. When mapping Suki telemetry to this measure, confirm whether the source field reflects appointments scheduled, visits roomed, or notes signed. Unsigned notes can inflate counts; see the operational algorithm for guidance.

## Operational Algorithm

**Unit:** Completed encounters per provider per week  
**How it works:** Count the number of completed patient encounters per provider per week. Compare each provider's average weekly encounter count before Suki adoption to after adoption (excluding the onboarding ramp). Average across the provider cohort. `total_encounters` (monthly) or `encounters_per_day` (daily average) from the EHR data pull, converted to a weekly figure, are the preferred fields.  
**Delta interpretation:** More completed encounters per provider per week after adoption indicates providers have capacity to see additional patients, likely because Suki reduces per-encounter documentation time.  
**Watch out for:**
- Not all health systems want higher throughput — increased volume without adjusted staffing can raise workload
- Normalize for scheduled clinical hours; providers working more hours will naturally see more patients
- Exclude providers who changed specialty, site, or panel size during the measurement window
- Verify that encounter counts include only completed, signed encounters — unsigned notes can inflate the count

**Visual sketch:**
```
Completed encounters per provider per week

22 |                    . . . .
21 |            . . . .
20 |  . . . .
   |
   +---Pre adoption---+---Post adoption--->
```
*Encounters per week should trend up modestly. Holmgren 2026 found +0.80/week — a real but modest effect.*

---

## Papers Measuring This (7)
- [[Albrecht 2025 - Ambient AI Clinical Documentation QI Survey]]
- [[Boyter 2025 - Ambience Healthcare ROI Validations KLAS Report]]
- [[Bundy 2024 - Administrative Loads Physicians AI Documentation Qualitative]]
- [[Haberle 2024 - Impact Nuance DAX Ambient Listening AI Documentation]]
- [[Holmgren 2026 - Ambient AI Scribes Physician Financial Productivity]]
- [[Shuaib 2021 - Scribe Program Patient Throughput Physician Productivity]]
- [[Peterson Health Technology Institute 2025 - Adoption AI Healthcare Delivery Systems]]

---
*Canonical Measures | Suki Literature Review Vault | Derived 2026-03-25, updated 2026-04-15*
*Method: Bottom-up derivation from 494 raw measure rows across 54 papers*

## License

This file is part of the [ACI Structured Evidence Review](https://github.com/regenstrief/aci), licensed under [CC BY-SA 4.0](../LICENSE). If you extend this work, consider contributing back via a pull request.
