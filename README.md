# AI Tools Comparison Report: FoodFast Synthetic Dataset

**Report Date:** June 22, 2026  
**Analyzed Tools:** Claude, ChatGPT, Gemini, Grok, Copilot  
**Dataset Task:** Generate 200 rows of realistic food delivery order logs (CSV format)

---

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

* **Mathematical Consistency:** 100% accurate across all of the models. The financial calculation constraint is verified perfectly:  
  $$\text{total\_amount\_usd} = \text{item\_price\_usd} \times \text{quantity}$$
* **Structural Match:** All three leading models perfectly adopted the specified multi-categorical schema (`Meals`, `Salads`, `Drinks`, `Dessert`).
* **The Shared Logic Flaw:** A systematic LLM behavior pattern was detected during validation. For orders flagged as `Cancelled` or `Returned`, ChatGPT (**29 instances**), Claude (**28 instances**), and Gemini (**24 instances**) incorrectly generated active durations inside `delivery_duration_mins` instead of setting them to `Null`/`NaN`.

---

### Final Recommendation Hierarchy


* **Avoid:** **Copilot** (unreliable for requested volumetric constraints).