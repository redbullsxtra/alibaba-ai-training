# Lab 1 — QwenWork Capability Demo: Multi-Source → Analytics → Dashboard
**15-minute hands-on lab**

This lab is not about writing perfect code. It is about seeing what QwenWork can do in **one prompt** across three things that normally take a team a day:

| Capability | What you should see | Where in the output |
|---|---|---|
| **1. Multi-source understanding** | A scanned PDF and a raw CSV read together, with the report's themes *driving* which data columns get tested | Step 3 hypothesis table — every row must link a PDF threat to a real CSV column |
| **2. Research & analytics** | Real Python executed, not recited — cross-tabs with counts *and* rates, correlations, a trained Random Forest with metrics | Steps 4.1–4.3 |
| **3. Professional dashboard** | A single `.html` file that opens in a browser and looks board-ready | Step 5 |

If the final answer is a wall of text with no executed code and no working HTML file, the demo failed — regardless of how good the prose reads.

---

## Files in this folder

| File | Notes |
|---|---|
| `2025 banking industry outlook Deloitte Insights.pdf` | 26 pages, **image-only — no text layer.** The assistant must use vision/OCR. A summary that never describes a chart or figure is invented. |
| `Churn_Modelling.csv` | 10,000 customers × 14 columns. Target = `Exited`. |

Columns: `CreditScore, Geography, Gender, Age, Tenure, Balance, NumOfProducts, HasCrCard, IsActiveMember, EstimatedSalary, Exited` (+ ID columns).

---

## Run sheet (15 min)

| Time | Do this |
|---|---|
| **0:00–0:02** | New chat. Attach **both** files **in the same message** — confirm both attachment chips are visible. |
| **0:02–0:10** | Paste the prompt below verbatim. Send. Do not interrupt while it runs. |
| **0:10–0:12** | Open the generated HTML dashboard in your browser. Check it actually renders. |
| **0:12–0:14** | Run the two probes below. |
| **0:14–0:15** | Grade with the rubric. |

---

## The prompt (copy-paste)

```text
Act as a Chief Strategy Officer for a global bank, I have uploaded the '2025 Banking Industry Outlook' PDF and the 'Churn_Modelling.csv' dataset.
1) Read the PDF and summarize the top 3 macroeconomic or operational threats to retail banking in 2025–2026.
2) Based on those threats, hypothesize which customer segments in the uploaded CSV (e.g., by Geography, Age, or Balance) are most at risk of churning.
3) Output your hypotheses as a structured Markdown table linking the macro threat to the specific data columns we should investigate.
4) analyze the uploaded 'Churn_Modelling.csv' to test those hypotheses by:
4.1 Calculate the churn rate (Exited) grouped by Geography and Age brackets (e.g., <30, 30-50, >50).
4.2 Identify the top 3 features most correlated with churn.
4.3 Write and execute a quick Random Forest classifier to predict churn, and return the model's accuracy and feature importance scores.
5) Present the findings in a concise, executive-friendly summary and html analytic dashboard
```

Three things make this prompt work, and they are worth pointing out live:

- **Nested steps 4.1–4.3** prevent silent skipping.
- **"Write and execute"** forces computation instead of invented numbers.
- **Hypothesis (2–3) before model (4)** is the real analytical discipline — watch whether the output truly connects them back.

---

## Two probes (do both — 2 min)

1. **Did it really read the PDF?** Ask: *"Describe the most prominent chart on page 4, then show which of your three threats cites it."* If it can't, it summarized from the filename.
2. **Did it really run the model?** Ask: *"Print the row count for each age bracket and confirm they sum to 10,000. Then re-run the Random Forest with random_state=42 and tell me if accuracy moved."*

---

## 30-second sanity check

You don't need to verify every number — spot these and you can trust the rest:

| Check | Correct value |
|---|---|
| Overall churn | **20.4%** (2,037 / 10,000) |
| Highest-risk segment | **Germany, age > 50 — 59.8%** (≈ 3× baseline) |
| Germany overall | 32.4% (vs France 16.2%, Spain 16.7%) |
| Top 3 correlates | `Age` (+0.285), `IsActiveMember` (−0.156), `Balance` (+0.119) |
| Random Forest accuracy | **≈ 0.84–0.86** (imbalanced data — 85% is not as good as it sounds) |

Two things a strong answer should notice on its own:

- `NumOfProducts` looks harmless by linear correlation but is decisive non-linearly: 2 products = 7.6% churn, 3 products = 82.7%.
- `Surname` / `CustomerId` must be dropped. If an ID shows up as a top feature, the pipeline is broken.

---

## Grade it

| Band | Looks like |
|---|---|
| **Impressed** | All three capabilities visible, numbers match the check, dashboard renders, flags the class-imbalance caveat |
| **Good** | Correct analytics + working dashboard, but PDF summary is generic or the hypothesis table is decorative |
| **Weak** | Narrative only — no executed code, no file, no counts with rates |

---

## If it stalls (don't spend the clock debugging)

| Symptom | One-line fix |
|---|---|
| "I can't access the file" | Both files must be attached to the **same** message — re-attach |
| PDF summary is generic | *"Describe page 1's visuals to prove you read it"* |
| Numbers with no code | *"Show the Python you ran and its printed output"* |
| Dashboard won't open / blank | *"Make it one self-contained HTML file, inline CSS/JS, no external CDNs"* |
| Accuracy > 0.95 | *"Show your train/test split and confirm `Exited` is not a feature"* |

If it's still stuck at 10 minutes, restart the chat once with both files — cheaper than debugging.
