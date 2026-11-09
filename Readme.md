# AtliQ Mart: Promotion Performance Analysis

An end-to-end Tableau analysis of the Diwali 2023 and Sankranti 2024 promotions run by AtliQ Mart, built for the Codebasics Resume 
Project Challenge (FMCG, Sales / Promotions).



## Problem Statement

AtliQ Mart is a retail chain with 50 supermarkets across southern India. During Diwali 2023 and Sankranti 2024, all 50 stores ran large promotions on AtliQ-branded products. The Sales Director wants to know **which promotions worked and which did not**, so the next promotional period can be planned with evidence.

As the data analyst, the task was to:

- Analyse the promotion data across stores, promotion types, products and categories.
- Build an easy-to-read dashboard with the key metrics.
- Turn the findings into actionable recommendations for the Sales Director.

---

## Dataset

| File | Rows | Description |
|---|---|---|
| `fact_events.csv` | 1,500 | One row per promotion event: store, campaign, product, base price, promo type, units sold before and after the promotion |
| `dim_stores.csv` | 50 | Store ID and city (10 cities) |
| `dim_products.csv` | 15 | Product code, name and category (5 categories) |
| `dim_campaigns.csv` | 2 | Diwali 2023 and Sankranti 2024 (names and dates) |

The data has no null values and no duplicate event IDs.

**Data model:** star schema, with `fact_events` joined to the three dimension tables on `store_id`, `product_code` and `campaign_id`.

---

## Metrics

| Metric | Definition |
|---|---|
| Revenue Before Promo | Base price × units sold before promo |
| Revenue After Promo | Promo price × units sold after promo (adjusted for BOGOF) |
| Incremental Revenue (IR) | Revenue after − Revenue before |
| Incremental Sold Units (ISU) | Units after (BOGOF adjusted) − Units before |
| IR % | IR / Revenue before |
| ISU % | ISU / Units before |

**Promo price rules**

| Promo type | Promo price |
|---|---|
| 25% OFF | Base price × 0.75 |
| 33% OFF | Base price × 0.67 |
| 50% OFF | Base price × 0.50 |
| 500 Cashback | Base price − 500 |
| BOGOF | Base price × 0.50, with units sold after promo counted twice (to include the free unit) |

---

## Dashboards

### 1. Store Performance
KPI cards: Revenue Before, Revenue After, Incremental Revenue, Incremental Units, IR %, ISU %

- Top 10 stores by Incremental Revenue
- Bottom 10 stores by Incremental Sold Units
- Incremental Revenue by city
- Store scatter: units vs revenue
- Campaign comparison: Diwali vs Sankranti

### 2. Promotion Type Analysis
KPI cards: Total Promo Events, Total Incremental Revenue, Promo Types Losing Revenue, BOGOF Unit Lift

- Top 2 promo types by Incremental Revenue
- Contribution to incremental units by promo type
- Event-level IR %: Discount vs BOGOF vs Cashback
- Unit lift vs revenue lift by promo type
- Incremental Revenue: promo type × campaign
- Average incremental units per event: Diwali vs Sankranti

### 3. Product & Category Analysis
KPI cards: Total Products, Total Categories, Products with Negative IR, Best Category by Unit Lift

- Unit lift (ISU %) by category
- Share of incremental units by category
- Top 5 products by Incremental Revenue
- Bottom 5 products by unit lift
- Incremental units by category and promo type
- Category × promo type: unit lift

---

## Key Findings

**Overall**
- Promotions grew revenue from 140.7M to 295.6M (+110%, Incremental Revenue of 154.9M) and units from 209K to 651K (+211%).

**Promotion types**
- Only BOGOF and Cashback (40% of events) created more than 100% of the gain, while the 900 percentage-discount events lost 5.5M.
- BOGOF delivers 84% of all incremental units (unit lift of 640%).
- Cashback contributes 58.8% of incremental revenue, but from a single product (the Home Essential Combo), which is a concentration risk.
- Like-for-like check: Chakki Atta and Sunflower Oil ran both 25% OFF and BOGOF. BOGOF added 27.7M, while 25% OFF lost 2.2M.
- 25% OFF is the weakest promotion and the only one that lost units.

**Products and categories**
- Home Appliances has the biggest unit lift (629%). Combo1 has the biggest revenue gain (91M).
- Personal Care is the only category that lost revenue (−0.85M), and 8 of 15 products lost revenue.
- BOGOF lifts units by roughly 610 to 650% in every category it ran in, so promo type matters more than category.

**Stores and cities**
- The top 10 stores deliver 29.2% of incremental revenue, mostly in Bengaluru, Chennai and Mysuru.
- Bengaluru, Chennai and Hyderabad together contribute 59.2% of incremental revenue.
- Top stores win through higher Cashback combo and BOGOF sales, not through more events (every store ran 30 events).
- The weakest stores are in Mangalore, Visakhapatnam, Trivandrum and Vijayawada.

**Campaigns**
- Diwali drove 57% of incremental revenue. Sankranti delivered the bigger unit lift (338% vs 97%).

---

## Recommendations

1. Replace percentage discounts with BOGOF on staples and home products.
2. Stop 25% OFF, and avoid discounts on Personal Care.
3. Test Cashback on more high-priced items, since it is a small effective discount on a large base price.
4. Use Diwali for revenue (Cashback) and Sankranti for volume (BOGOF).
5. Give weak-store cities the BOGOF and Cashback mix that top stores sold.

---

## Assumptions and Limitations

- Promo price rules above (especially for BOGOF and Cashback) are assumptions based on the challenge brief. Results for BOGOF depend on counting the free unit.
- Promo type is tied to product: each product ran only one or two promo types. Promo effect and product effect cannot be fully separated, except for Chakki Atta and Sunflower Oil, which ran both 25% OFF and BOGOF.
- The dataset has no cost or margin data, so IR % is used as a proxy for margin health.

---

## Tools

- Tableau Public (data model, calculated fields, dashboards)

---

## Repository Structure

```
.
├── README.md
├── data/
│   ├── fact_events.csv
│   ├── dim_stores.csv
│   ├── dim_products.csv
│   └── dim_campaigns.csv
├── dashboards/
│   ├── 1_store_performance.png
│   ├── 2_promotion_type.png
│   └── 3_product_category.png
└── AtliQ_Mart_Promotions.twbx
```

---

## Author

**`<Your Name>`**
LinkedIn: `<your profile link>`
