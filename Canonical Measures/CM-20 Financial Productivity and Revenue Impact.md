# CM-20 Financial Productivity and Revenue Impact

**D&M Dimension:** [[OI - Organizational Impact]]

## Definition
Revenue generated through healthcare operations associated with ambient AI scribe use, measured as RVU changes, revenue per clinician per year, or ROI.

## Measurement Methods
| Method | Description | Data Source |
|---|---|---|
| RVUs per encounter / per week | Relative value units billed; standard productivity measure | Claims / EHR |
| Work Relative Value Units (wRVUs) per hour | Hourly productivity in wRVUs | Claims / EHR |
| Additional revenue per clinician per year | Dollar value of RVU increase at Medicare rates | Financial |
| ROI (return on investment) | Net financial benefit relative to tool cost | Financial |
| Cost comparison | Ambient AI cost vs. human scribe or alternative | Financial |

## Aliases Used in Literature
- RVUs per Encounter / per Week ([[Holmgren 2026 - Ambient AI Scribes Physician Financial Productivity|Holmgren 2026]]: +0.04/encounter, +1.81/week, ≈$3,044/year)
- Work Relative Value Units ([[Haberle 2024 - Impact Nuance DAX Ambient Listening AI Documentation|Haberle 2024]])
- Physician Productivity (billing) *(⚠️ verify source)*
- Financial Viability (Combined) ([[Boyter 2025 - Ambience Healthcare ROI Validations KLAS Report|Boyter 2025]]: +$13,049/year)
- Financial Benefit *(⚠️ verify source)*
- ROI ([[Boyter 2025 - Ambience Healthcare ROI Validations KLAS Report|Boyter 2025]])
- Cost Comparison ([[Cao 2024 - Artificial Intelligence-Driven Digital Scribes Dermatology|Cao 2024]])
- Additional Yearly Revenue ([[Boyter 2025 - Ambience Healthcare ROI Validations KLAS Report|Boyter 2025]])
- Revenue Impact of HCC Capture ([[Boyter 2025 - Ambience Healthcare ROI Validations KLAS Report|Boyter 2025]]: +$9,685/year) *(moved from CM-21, dollar value of coding inaccuracy/improvement is financial impact)*
- Revenue Impact of E/M Level Improvement ([[Boyter 2025 - Ambience Healthcare ROI Validations KLAS Report|Boyter 2025]]: +$1,907/year) *(moved from CM-21, dollar value is financial impact)*
- VBC-Attributed Panel Size ([[Haberle 2024 - Impact Nuance DAX Ambient Listening AI Documentation|Haberle 2024]])

## ⚠️ Key Note
Three independent papers show financial productivity improvement: Holmgren 2026 (+$3,044/year RVU, UCSF, no denial increase), Boyter/KLAS 2025 (+$13,049/year mostly from HCC, Ambience). PHTI 2025 raises the population-level concern: even *accurate* higher coding increases healthcare system spending. The individual health system ROI may conflict with payer/societal interests.

## Operational Algorithm

### CM-20a — wRVU Output

**Unit:** wRVUs per provider per week  
**How it works:** For each provider, multiply each billed CPT code by its CMS wRVU weight and sum across all encounters in the week. Compare each provider's average weekly wRVU total before Suki adoption to after adoption (excluding the onboarding ramp). Average across the provider cohort. `wrvu_total` from the EHR data pull, aggregated to a weekly figure, is the preferred field.  
**Delta interpretation:** Higher wRVUs per provider per week after adoption indicates Suki is supporting more complete coding of encounter complexity.  
**Watch out for:**
- Exclude the onboarding ramp (first ~4 weeks of Suki use)
- Use the same-period prior year as the pre window to control for seasonal variation
- Exclude providers who changed specialty, site, or employment status during the window
- Normalize for scheduled clinical hours when part-time providers are included

**Visual sketch:**
```
wRVUs per provider per week

45 |                    . . . .
43 |            . . . .
41 |  . . . .
   |
   +---Pre adoption---+---Post adoption--->
```
*wRVUs per week should trend up. Holmgren 2026 found +1.81 wRVUs/week (~$3,044/provider/year) at UCSF.*

---

### CM-20b — Billing Revenue

**Unit:** Paid revenue per provider per month ($)  
**How it works:** Sum total adjusted net revenue per provider per month from EHR or claims data. Compare the pre-adoption monthly average to the post-adoption monthly average per provider, then average across the cohort. For an annualized figure: wRVU delta × 52 weeks × Medicare conversion factor (~$33.29/wRVU in 2026). `revenue_paid` (adjusted net) is the preferred field.  
**Delta interpretation:** Higher revenue per provider per month after adoption indicates that more complete documentation is translating into collected revenue, through higher wRVUs, better E/M coding, or reduced denials.  
**Watch out for:**
- Use adjusted net revenue (collected), not gross charges — gross misleads if payer mix shifts
- Revenue responds to payer mix, contract rate changes, and denial patterns independently of Suki
- Pair with CM-20a to show the wRVU mechanism behind any revenue shift
- Dollar figures vary substantially by specialty; report within-specialty when possible

**Visual sketch:**
```
Revenue per provider per month ($)

$22k |                    . . . .
$20k |            . . . .
$18k |  . . . .
     |
     +---Pre adoption---+---Post adoption--->
```
*Revenue should trend up. Boyter/KLAS 2025 found +$13,049/provider/year, heavily driven by HCC capture.*

---

### CM-20c — E/M Level Improvement

**Unit:** Percentage of encounters billed at Level 4 or 5  
**How it works:** Divide the count of Level 4 and Level 5 E/M encounters (99214/99215 established; 99204/99205 new) by total E/M visits. Compare this share before and after Suki adoption. Full per-level counts (Levels 1–5, new and established) are needed to compute the denominator accurately. `em_new_level4_count`, `em_est_level4_count`, `em_new_level5_count`, `em_est_level5_count`, and `em_total_count` are the preferred fields.  
**Delta interpretation:** A higher share of Level 4–5 encounters after adoption indicates documentation is capturing visit complexity more completely and supporting higher billing levels.  
**Watch out for:**
- Read alongside CM-21c (denial rate) — rising E/M levels with rising denials suggests overcoding, not legitimate complexity capture
- Case mix must be stable or normalized — a shift toward more complex patients raises E/M levels independently of Suki
- New vs. established patient mix affects the baseline distribution; track separately or normalize

**Visual sketch:**
```
% encounters billed at Level 4-5

65% |                    . . . .
60% |            . . . .
55% |  . . . .
    |
    +---Pre adoption---+---Post adoption--->
```
*Level 4–5 share should trend up. Boyter/KLAS 2025 found +$1,907/provider/year from E/M level gains — watch denial rate in parallel.*

---

## Papers Measuring This (8)
- [[Boyter 2025 - Ambience Healthcare ROI Validations KLAS Report]]
- [[Cao 2024 - Artificial Intelligence-Driven Digital Scribes Dermatology]]
- [[Haberle 2024 - Impact Nuance DAX Ambient Listening AI Documentation]]
- [[Holmgren 2026 - Ambient AI Scribes Physician Financial Productivity]]
- [[Kanaparthy 2025 - Real-World Evidence Digital Scribes Rapid Review]]
- [[Shuaib 2021 - Scribe Program Patient Throughput Physician Productivity]]
- [[Suhail 2026 - Metrics for Ambient Clinical Documentation Scoping Review]]
- [[Galloway 2024 - Impact Artificial Intelligence Based Solution Clinicians Clinical Documentation]]

---
*Canonical Measures | Suki Literature Review Vault | Derived 2026-03-25, updated 2026-04-15*
*Method: Bottom-up derivation from 494 raw measure rows across 54 papers*

## License

This file is part of the [ACI Structured Evidence Review](https://github.com/pbiondich/aci), licensed under [CC BY-SA 4.0](../LICENSE). If you extend this work, consider contributing back via a pull request.
