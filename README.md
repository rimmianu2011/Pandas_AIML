# Pandas Lab — FAANG-Level Hands-On

**Goal:** Build strong intuition for Pandas transformations used in real ML pipelines (feature engineering, joins, groupby, leakage-safe logic).

**Outcome:** Students can write correct, efficient Pandas code, explain tradeoffs, and avoid common interview/production gotchas.

---

# How to Start

1. **Fork** this repository.  
2. Open `pandas_student_lab.ipynb` in **Google Colab**.  
3. Complete all **TODO** sections.  
4. **Restart runtime → Run All** cells.  
5. Push changes and submit a **Pull Request**.  

⚠️ **Do NOT edit notebooks directly on GitHub.**

---

## Lab Rules (FAANG Style)

- ❌ Avoid `.apply` unless explicitly required
- ✅ Prefer vectorized Pandas/NumPy operations
- ✅ Always reason about join cardinality (1:1, 1:n, n:n)
- ✅ Always check for leakage (time-aware features)
- ✅ Provide scaling intuition: what breaks at 100M rows?

---

# Out of Scope

- Model training
- AutoML

---

# Notebook Rules

- Do **NOT** rename the notebook  
- Do **NOT** delete TODOs  
- Do **NOT** hardcode outputs  
- Notebook must run **top-to-bottom**  

---

# Dataset

- Synthetic event + order tables inside the notebook

## Why?

- Keeps focus on joins/groupbys and feature logic
- Mirrors ML feature engineering interviews

---

## Section 1 — DataFrame Fundamentals

### Task 1.1: Filtering + datetime features

- Extract `purchase` events
- Add `event_day` from timestamp

**Checkpoint Questions:**

- Why prefer `datetime64` over Python `date` objects?
- When do you need `.copy()` to avoid `SettingWithCopyWarning`?

---

## Section 2 — GroupBy (Core for Features)

### Task 2.1: Per-user aggregates

- `n_events`
- `n_purchases`
- `total_revenue`

**Interview Angle:**

- Conditional aggregation best practices
- Counting purchases via `event == 'purchase'` vs `amount > 0`

---

### Task 2.2: GroupBy transform (row-level feature)

- Add per-row `user_event_count`

**Checkpoint Questions:**

- `transform` vs `agg`: what shape do you get back?

---

## Section 3 — Joins & Merge (Feature Table Building)

### Task 3.1: Join features to user table

- Left join user features to users
- Fill missing values correctly

**FAANG Gotcha:**

- How to detect many-to-many join explosion early (rowcount checks, key uniqueness)

---

### Task 3.2: Join explosion debugging (mini)

- Construct an n:n join that multiplies rows
- Fix by deduping or pre-aggregating

**Checkpoint Questions:**

- When do you dedupe vs aggregate?

---

## Section 4 — Time-based Features & Leakage

### Task 4.1: Leakage-safe cumulative feature

- Compute `purchases_before` per event row

**FAANG Gotcha:**

- Why `cumsum` without `shift` leaks labels on purchase rows

---

## Section 5 — Apply vs Vectorization

### Task 5.1: Replace `.apply` with vectorized operations

**Interview Angle:**

- Why `.apply` is usually slow (Python calls per row)

---

## Submission Expectations

Students must submit:

- Clean notebook (runs top-to-bottom)
- Answers to all **Explain/Checkpoint** prompts
- Correctness checks passing

---

## FAANG Interview Evaluation Rubric

| Skill                         | Evaluated |
|------------------------------|-----------|
| Correctness                   | ✅        |
| Join intuition (cardinality)  | ✅        |
| Groupby mastery               | ✅        |
| Leakage awareness             | ✅        |
| Code clarity                  | ✅        |

---

## Stretch Problems (Optional)

- Implement time-aware rolling features per user (7d/30d)
- Build a feature table at “user-day” grain
- Optimize a slow query: `.groupby().apply()` → vectorized
