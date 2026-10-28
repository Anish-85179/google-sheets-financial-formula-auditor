# Enterprise Financial Formula Auditor & Dynamic Error Repair Engine (Google Sheets Edition)

An enterprise-grade financial formula auditing, automated error-trapping, and subledger reconciliation pipeline built natively in **Google Sheets**. This project establishes robust data hygiene frameworks to sanitize corrupted general ledger records, resolve formula calculation errors (`#N/A`, `#DIV/0!`, `#VALUE!`), execute precise variance reconciliation against subledger balances under a strict **$0.04 materiality tolerance threshold**, and drive executive visibility through a real-time KPI console.

---

## 🏗️ Architectural Overview & Structure

The workbook is structured into **4 sequential operational sheets** designed to ingest raw messy accounting data, sanitize financial calculations, verify ledger-to-subledger alignment, and present executive metrics:

1. **`General_Ledger_Data`** — Ingestion layer containing 100 raw transaction records with deliberate enterprise anomalies, text-formatting corruptions, invalid vendor IDs, and broken calculations.
2. **`Formula_Repair_Engine`** — Transformation layer utilizing advanced cloud-native error-trapping and cleaning formulas (`VALUE`, `TRIM`, `REGEXREPLACE`, `TO_TEXT`) to normalize vendor codes, parse quantities, and calculate clean extended costs.
3. **`Reconciliation_Matrix`** — Variance detection engine comparing repaired extended costs against target subledger balances using a strict **$0.04 tolerance threshold**, automatically flagging matched records versus required manual reviews.
4. **`Executive_Dashboard`** — Executive KPI dashboard tracking total audits, trapped errors, reconciliation variances, and system health stability scores in real time.

---

## 🛠️ Core Technical Implementation & Formulas

### 1. Data Cleaning & Error-Trapping (`Formula_Repair_Engine`)
To resolve text-string price formats and formula errors (`#DIV/0!`, `#VALUE!`), cloud-compatible sanitization formulas are applied:
* **Vendor Sanitization:**
  ```excel
  =IF(OR(ISBLANK(General_Ledger_Data!D2), General_Ledger_Data!D2="#N/A"), "VEND-UNKNOWN", General_Ledger_Data!D2)
