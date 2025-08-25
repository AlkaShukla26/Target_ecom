# Target_ecom
 Analyzed Target’s retail transaction data using SQL to uncover customer purchase patterns and key business insights.   Queries focused on customer segmentation, sales performance, and data-driven recommendations.

# 🛒 Target E-commerce Case Study (SQL-only)

## 📌 Overview
End-to-end analysis of Brazilian e-commerce (2016–2018) using **only SQL** in BigQuery.  
Focus: dataset profiling, trends, geography, pricing & freight, delivery performance, and payments — with actionable business recommendations.

---

## 🔍 What I Did (SQL)
- **Profiling:** `INFORMATION_SCHEMA.COLUMNS` to audit column types; verified clean structure.
- **Time Range:** `MIN/MAX(order_purchase_timestamp)` → **2016 to 2018**.
- **Coverage:** Distinct **cities & states** of ordering customers.
- **Trends:** Yearly/monthly order counts with **window functions** (`LAG`) for % change.
- **Seasonality & Hours:** Monthly pattern; **time-of-day** bucketing (dawn/morning/afternoon/night).
- **Geo Join:** Orders ↔ customers to get **month-by-state** volumes.
- **Economics:** Payments join to compute **value growth** and statewise **price/freight**.
- **Delivery KPIs:** `time_to_deliver` and `diff_estimated_delivery` via `DATE_DIFF`.
- **Payments:** MoM payment_type usage; installments distribution.

---

## 📊 Key Findings
**Trend & Seasonality**
- Strong growth **2016→2017**; slower **2017→2018**.
- **Monthly:** steady rise **Jan–May** (peak at **May**), **June −10.98%**, recovery in Jul–Aug, **September −60.3%**, **October +15.19%** vs Sep.
- **Time of day:** **Afternoon (13–18h)** has the most orders.

**Geography**
- Customer base concentrated in major states (e.g., **SP**).  
- States **PB, AP, AC** show **higher purchasing capacity** (higher average order price & total spend).

**Economics**
- **Order cost (payment_value) up ~137%** in **Jan–Aug 2018 vs Jan–Aug 2017**.
- **Freight:** large state variance; **RR** has **highest average freight**.

**Delivery**
- `time_to_deliver` varies by state; **RR** shows the **highest average delivery time**.  
- “Faster-than-estimate” leaderboard (by negative `actual−estimated`) includes **AC, RO, AP, AM** (per your query); reconcile with absolute delays when prioritizing ops.

**Payments**
- **Credit Card** dominates; **UPI adoption rises in 2017**; **vouchers/debit** are niche.
- **Installments (≥1)** are common, aligning with local payment behavior.

---

## ✅ Recommendations (Data-Driven)
1. **Fix slow lanes:** Prioritize logistics in **RR** (highest freight & delivery time); benchmark practices from **AC/RO/AP/AM**.
2. **Freight optimization:** Audit carrier mix and routing in high-cost states (e.g., RR); set **SLA-based contracts**.
3. **Monetize high-value states:** Target **PB/AP/AC** with premium SKUs & exclusive bundles.
4. **Inventory planning by seasonality:** Build stock ahead of **Apr–May**; mitigate **September** slump with promos and demand gen.
5. **Payments strategy:** Promote **UPI** & **Credit Card/EMI** with cashback; **rethink vouchers** (bundle with seasonal offers).
6. **Delivery monitoring:** Track SKUs with chronic delays; adjust sourcing/FC placement to cut `time_to_deliver`.

---

## 🧰 SQL Techniques Used
CTEs, multi-table joins, `EXTRACT` (year/month/hour), `DATE_DIFF`, window functions (`LAG`), `CASE` bucketing, `COUNT DISTINCT`, and `INFORMATION_SCHEMA` introspection.

---

## 📈 Outcome
Converted raw e-commerce data into **clear operational levers** (logistics, freight, inventory, payments) and **market actions** (state targeting), using **SQL only** .
