# Optimization Notes

## Bow Comfort Score: Mathematical Heuristics & Optimization

The **Comfort Score** evaluates how ergonomically suitable the bow is for the selected user profile based on four key components: **grip**, **thickness**, **stiffness**, and **curvature**.

---

### Comfort Score Formula

```math
\text{Comfort Score} = 
(0.4 \cdot \text{Grip Score} + 
 0.3 \cdot \text{Thickness Score} + 
 0.2 \cdot \text{Stiffness Score} + 
 0.1 \cdot \text{Curvature Score}) \times 100
```

Each component score ranges from **0** to **1**, computed using rule-based ergonomic heuristics explained below.

---

### Heuristic Scoring Criteria: Grip Score

Derived from the ratio of `Grip Width` to 27% of the user’s `Palm Size`.

```math
\text{Grip Ratio} = \frac{\text{Grip Width}}{0.27 \times \text{Palm Size}}
```

| Grip Ratio Condition | User Type   | Score |
|----------------------|-------------|-------|
| > 1.2                | Child       | 0.7   |
| > 1.2                | Adult/Pro   | 0.9   |
| < 0.8                | Any         | 0.6   |
| 0.8 ≤ Ratio ≤ 1.2    | Any         | 1.0   |

---

### Heuristic Scoring Criteria: Thickness Score

Comfort based on the relationship between bow thickness and palm size:

| Condition                                      | Score |
|-----------------------------------------------|-------|
| Bow Thickness > 6.0 AND Palm Size < 75.0 mm   | 0.6   |
| Bow Thickness < 4.5 AND Palm Size > 100.0 mm  | 0.8   |
| Otherwise                                      | 1.0   |

---

### Heuristic Scoring Criteria: Stiffness Score

Based on how easily the bow can be drawn by users of varying experience and strength:

| Condition                                       | Score |
|------------------------------------------------|-------|
| Limb Stiffness > 0.7 AND User = Child          | 0.5   |
| Limb Stiffness < 0.5 AND User = Professional   | 0.7   |
| Otherwise                                       | 1.0   |

---

### Heuristic Scoring Criteria: Curvature Score

Comfort is highest within an ideal ergonomic curvature range:

| Condition                       | Score |
|--------------------------------|-------|
| 0.25 ≤ Bow Curvature ≤ 0.35    | 1.0   |
| Otherwise                      | 0.8   |

---

### Other Details

- The total comfort score is **clipped to the range [0, 100]**.
- These rules are designed to reflect ergonomic suitability based on user age, skill level, and physical proportions.
- The full breakdown is logged to:

```
logs/comfort_score_debug.txt
```

This file includes:
- All bow parameters
- Palm size



