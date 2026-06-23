# AI Tools Comparison Report: FoodFast Synthetic Dataset

**Report Date:** June 22, 2026  
**Analyzed Tools:** Claude, ChatGPT, Gemini, Grok, Copilot  
**Dataset Task:** Generate 200 rows of realistic food delivery order logs (CSV format)

---
#`# Prompts Used for Generation

To ensure a fair benchmark, the exact same prompt configuration was tested across all five AI models.

### 1. Bad Prompt
```
Generate a realistic synthetic dataset representing user order logs for an online food delivery platform named "FoodFast" format: csv, 200 row
```

### 2. Good Prompt
````
You are a senior data analyst. Your task is to generate a realistic synthetic dataset representing user order logs for an online food delivery platform named "FoodFast". Generate a CSV dataset with exactly the following 14 columns:
1. order_id (Format: FF-001 to FF-200)
2. customer_id (Unique identifier, some customers should appear multiple times)
3. item_name (Popular food)
4. item_category (Meals, Dessert, Drinks, Salads)
5. order_timestamp (Format: 2025-01-01 to 2026-06-01)
6. delivery_duration_mins (Integer between 12 to 90)
7. item_price_usd (Price per single item)
8. quantity (Integer)
9. total_amount_usd (Strictly calculated as item_price * quantity, rounded to 2 decimals)
10. payment_method (Credit Card, Cash on Delivery, Apple Pay, PayPal)
11. delivery_status (Delivered, Cancelled, In-Progress, Returned)
12. customer_rating (1.0 to 5.0, or null if not rated)
13. order_location (city name)
Rules & Business Logic
Encode realistic patterns: "Meals" and "Dessert" categories should have a higher average item_price_usd. 
Long delivery_duration_mins should loosely correlate with lower customer_rating.
Size
- Generate exactly 200 rows of data.
Format
- Return the output strictly as a downloadable CSV block with a header row. 
````

### Executive Scorecard

| Rank | Tool | Status | Key Issue |
| :--- | :--- | :--- | :--- |
| 1 | **Claude** | Excellent | High catalog diversity, but ratings are unrealistically limited to 4–5 stars. |
| 2 | **Grok** | Good | Cleanest data structure (only 9 nulls), but lower unique customer diversity. |
| 3 | **ChatGPT** | Acceptable | Severe geographic concentration bias (45% of orders packed in 3 cities). |
| 4 | **Gemini** | Acceptable | Best natural 1–5 star distribution, but contains high missing value counts. |
| 5 | **Copilot** | Failed | Critical failure: **generated only 17 rows instead of 200**. |

---

### Technical & Math Validation Insights

* **Mathematical Consistency:** 100% accurate across all of the models. The financial calculation constraint is verified perfectly: `total_amount_usd` = `item_price_usd` × `quantity`

* **Structural Match:** All three leading models perfectly adopted the specified multi-categorical schema (`Meals`, `Salads`, `Drinks`, `Dessert`).
* **The Shared Logic Flaw:** A systematic LLM behavior pattern was detected during validation. For orders flagged as `Cancelled` or `Returned`, ChatGPT (**29 instances**), Claude (**28 instances**), and Gemini (**24 instances**) incorrectly generated active durations inside `delivery_duration_mins` instead of setting them to `Null`/`NaN`.

---

### Final Recommendation Hierarchy


* **Avoid:** **Copilot** (unreliable for requested volumetric constraints).