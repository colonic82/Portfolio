# 📊 Logistics & Warehouse Analytics Portfolio

**Giuseppe Iaccarino** · [LinkedIn](https://www.linkedin.com/in/giuseppe-iaccarino)

Python analytics portfolio built on real operational data from **Magazzino Badesse** (Monteriggioni, SI) — a regional distribution center serving 15 provinces in central Italy. All data anonymized. Analysis period: March–August 2022.

---

## Projects

### 1. 🗂️ [TablesCreator.ipynb](./TablesCreator.ipynb)
**Warehouse Reporting Automation**

Automated generation of 12 operational Excel reports from 7 WMS exports. Originally a monolithic script; refactored into modular functions with centralized anonymization and execution summary.

| Report | Description |
|---|---|
| STATO_E_CON_GIACENZA | Active articles with stock on hand |
| COPERTURA_OLTRE_8wk_NO_MKT | Overstocked articles (>8 weeks coverage, no promo) |
| PALLETTIZAZIONI_ERRATE | Articles with incorrect pallet configuration |
| STATO_H_NO_GIACENZA | Suspended articles with no stock |
| STATO_E_NO_GIACENZA | Active articles with zero stock |
| STATO_T_CON_GIACENZA | Transit articles with residual stock |
| STATO_T_CON_GIACENZA_E_PRESA | Transit articles still in active shelf slot |
| STATO_T_CON_GIACENZA_in_PRESA_o_SCORTA | Transit articles in pick or reserve locations |
| STATO_F | Final-status articles |
| CONSEGNA_NO_PRESA_NO_VOL | Incoming shipments with no pick slot or volume |
| STATO_O+S_NO_GIACENZA | On-order/seasonal articles with no stock |
| CONTROLLO_SOSTITUZIONI | Substitution consistency check |

**Input files required** (in `./INPUT/`): `Rotazioni.xlsx`, `Sostituzioni.xlsx`, `Ordini Fornitori.xlsx`, `Mappa Prese.xlsx`, `BuyerApprov.xlsx`, `Giacenza Corsie.xlsx`, `Controllo Anagrafica.xlsx`

---

### 2. 🚚 [LogisticsQueryTool.ipynb](./LogisticsQueryTool.ipynb)
**Route Cost & Saturation Analysis**

Interactive query tool to analyze transport route efficiency across provinces. Computes per-trip cost, vehicle saturation, and Colli/KM index. Includes a full case study on a structurally anomalous route.

**Three query functions:**

| Function | Usage | Output |
|---|---|---|
| `QueryViaggio('route')` | Analyze a single named route | PDV list, delivery frequency, weekday distribution |
| `VisualGite('MS', 'SP')` | Compare routes across 1–3 provinces | Saturation ranking, cost ranking, scatter plot |
| `GiteWeek('MS', 'SP')` | Weekly schedule view for 1–3 provinces | Routes per day barchart + saturation heatmap (day × route) |

**Vehicle rates:**

| Category | Rate (€/km) |
|---|---|
| Motrice 3 assi | 1.048 |
| Motrice 2 assi / Daily | 0.993 |
| Bilico / Bilichetto | 1.248 |

**Case Study — X: ORO DELLA TERRA**  
Fixed Mon/Wed/Fri specialty salumi route excluded from province saturation ranking (contractually defined low saturation). Analyzed independently with day-level PDV frequency matrix.

**Special routes excluded from saturation analysis:** Navettaggio, Transit Point, Vuoti, Taxi Merci — structural near-zero saturation, distort province averages.

**Input:** 7 SIGEP export files (`PIANSIGSIE*.xls`) in working directory.

---

### 3. 📦 [DataAnalysis_portfolio.ipynb](./DataAnalysis_portfolio.ipynb)
**Transport Efficiency KPI Dashboard**

End-to-end efficiency analysis across 4 provinces (MS, SP, RI, TR). Core KPI: **Colli/KM** (cases delivered per kilometer driven). Includes outlier detection, geographic mapping, weekday breakdown, and category-level analysis.

**Sections:**

| # | Section | Description |
|---|---|---|
| 1–2 | Load & Clean | SIGEP CSV ingestion, type normalization |
| 3 | Split by Province | MS · SP · RI · TR |
| 4 | Colli/KM per Route | Route-level efficiency index |
| 5 | Outlier Detection | ±3σ removal |
| 6 | Visualization | Per-province barplot with efficiency threshold |
| 7 | Cross-Province Comparison | Box plot + mean comparison |
| 8 | Action List | Routes below threshold (Colli/KM < 0.15) |
| 9 | Geographic Map | PDV scatter plot by GPS coordinates (matplotlib) |
| 10 | Efficiency by Weekday | Colli/KM broken down by delivery day per province |
| 11 | Efficiency by Day × Category | Merceologia dimension added to weekday analysis |
| 12 | Operational Recommendations | Auto-generated from data — consolidation candidates flagged |
| 13 | Executive Summary | Business-level synthesis of findings |

**Output charts:** `pdv_geographic_distribution.png` · `weekday_efficiency_by_province.png` · `merceologia_efficiency_by_day.png`

---

## Stack

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458)
![Seaborn](https://img.shields.io/badge/Seaborn-0.13-76b900)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.x-orange)
![NumPy](https://img.shields.io/badge/NumPy-1.x-013243)
![OpenPyXL](https://img.shields.io/badge/OpenPyXL-3.x-green)

---

## Background

All three projects were built during a logistics operations role at **Etruria Retail / Carrefour** (2022–2023), managing warehouse and transport reporting for a regional DC. The notebooks represent production-grade tools refactored for readability, modularity, and public portfolio use.

Data anonymized: supplier names, buyer names, and article descriptions are masked to the first 3 characters (`xxx`).

---

*Giuseppe Iaccarino — Siena, 2026*
