# Review Notes — Data Quality Profiling

**Reference document:** Data Quality Profiling – Sprint 1 (Deepika Gupta)
**Reviewed by:** Linda Chidiebube
**Sprint:** 1 — Data Foundation & Exploration

## Summary

Cross-checked Deepika's 12-section Data Quality Profiling report against my own independent verification of the same checks, done separately for learning purposes. Most findings matched exactly: missing values, 0 exact duplicate rows, referential integrity, date logic checks, and calculation checks. Below are additional findings from further investigation, plus items sent to Deepika for review, still awaiting her response as of this submission.

## 1. `current_stock` anomaly — not cross-referenced in her report

My own Requirement 4 findings (see `week1_findings.md`) show that `inventory_master.current_stock` is inflated 100 to 850 times realistic warehouse capacity, tracing exactly to `stock_ledger.running_balance`. This is not mentioned anywhere in Deepika's profiling doc. Flagging it here so it is not missed by anyone reading her report on its own.

## 2. Duplicate `invoice_id` / `payment_id` — deeper issue than reported

Deepika's report correctly flags 196 duplicate `invoice_id` groups (393 rows) and 201 duplicate `payment_id` groups (403 rows) as "High priority." Further investigation found the following:

- The row-to-group math does not divide evenly: 196 × 2 = 392, not 393; 201 × 2 = 402, not 403 — indicating at least one group in each case has 3 rows, not 2.
- Confirmed: `INV-341709` and `PAY-361416` are each genuine ID collisions — three completely unrelated transactions (different customers, branches, dates, and amounts) sharing the same ID.
- This means `invoice_id` and `payment_id` cannot be trusted as standalone unique keys for joins or aggregations — a real integrity risk beyond simple duplication.

## 3. Denominators added for context

- Unpaid invoices: 1,837 = 10.2% of 18,033 total invoices.
- Late payments: 8,200 = 42.6% of 19,257 total payments — a substantial finding and a strong candidate for its own KPI.

## 4. 208 early-payment records — clustering check

Checked whether the 208 "payment before invoice date" records cluster by branch or customer. Found they are scattered fairly evenly across all 6 branches (CHN001: 52, KOL001: 41, PUN001: 39, AHM001: 30, DEL001: 27, HYD001: 19), with no customer concentration (top customer: 4 occurrences). This looks like data-entry noise rather than a systemic issue — recommend excluding these records from date-sensitive analysis rather than building a KPI around them.

## Questions sent to Deepika — response pending

- Current_stock cross-reference heads-up.
- Whether she had identified the 3+ duplicate groups (triplets).
- Denominators for unpaid invoices and late payment context.
- Whether the 208 early payments cluster or scatter.

## Status as of this submission

No response received yet. The findings above were independently verified using pandas in Google Colab and stand regardless of her reply. This file will be updated if her response adds new information.
