# Optimization Notes

## TODO

- [X] Comfort Score
- [ ] 3D Printing Criteria Optim
- [ ] Arrow Opt

## Bow Comfort Score: Mathematical Heuristics & Optimization

The **Comfort Score** evaluates how ergonomically suitable the bow is for the selected user profile based on four key components: **grip**, **thickness**, **stiffness**, and **curvature**.

### Comfort Score Formula

Each component score ranges from **0** to **1**, computed using rule-based ergonomic heuristics explained below:

```math
\text{Comfort Score} = 
(0.4 \cdot \text{Grip Score} + 
 0.3 \cdot \text{Thickness Score} + 
 0.2 \cdot \text{Stiffness Score} + 
 0.1 \cdot \text{Curvature Score}) \times 100
```

### Heuristics

| **Component**      | **Condition**                                            | **User Type**     | **Score** |
|--------------------|----------------------------------------------------------|-------------------|-----------|
| **Grip Score**     | Grip Ratio > 1.2                                         | Child             | 0.7       |
|                    | Grip Ratio > 1.2                                         | Adult/Professional| 0.9       |
|                    | Grip Ratio < 0.8                                         | Any               | 0.6       |
|                    | 0.8 ≤ Grip Ratio ≤ 1.2                                   | Any               | 1.0       |
| **Thickness Score**| Bow Thickness > 6.0 AND Palm Size < 75.0 mm             | Any               | 0.6       |
|                    | Bow Thickness < 4.5 AND Palm Size > 100.0 mm            | Any               | 0.8       |
|                    | Otherwise                                                | Any               | 1.0       |
| **Stiffness Score**| Limb Stiffness > 0.7                                     | Child             | 0.5       |
|                    | Limb Stiffness < 0.5                                     | Professional      | 0.7       |
|                    | Otherwise                                                | Any               | 1.0       |
| **Curvature Score**| 0.25 ≤ Bow Curvature ≤ 0.35                              | Any               | 1.0       |
|                    | Otherwise                                                | Any               | 0.8       |


## 3D Print Settings Heuristic Table

| **Parameter**    | **Heuristic Logic**                                                                                                                                         |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Material**     | - If `limb_stiffness > 0.7` → use **Nylon or PETG** (for strength)  <br> - If `bow_thickness < 5.0` → use **PETG** (adds rigidity) <br> - Otherwise → **PLA or TPU** |
| **Layer Height** | - If `bow_curvature > 0.33` or `limb_stiffness > 0.7` → **0.12mm** (finer detail) <br> - Otherwise → **0.16mm** or **0.2mm**                                |
| **Infill**       | - If `limb_stiffness > 0.7` or `arrow_weight > 2.2g` → **30–35%** <br> - Else if `bow_thickness > 5.5` → **25%** <br> - Otherwise → **20%**                   |
| **Supports**     | - **No** by default <br> - Use **Yes** if `bow_curvature > 0.36` or arrow tip is heavily scaled                                                              |
| **Instructions** | - If using **TPU** → *Print bow limbs with TPU for flexibility and safety* <br> - If `limb_stiffness > 0.7` → *Print at 45° for strength* <br> - Else → *Standard orientation* |


