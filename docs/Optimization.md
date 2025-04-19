# Bow & Arrow Optimization: Heuristics & Process Overview

This system adaptively optimizes a **toy bow and arrow design** using physical heuristics, user ergonomics, and performance constraints. It dynamically updates the 3D model, provides print-ready recommendations, and simulates performance metrics like speed, force, and safety.

## Optimization Summary

- [x] **Comfort Score** — Rule-based ergonomic heuristics.
- [x] **Performance Optimization** — Launch speed & draw force matching.
- [x] **Arrow Auto-Adjustment** — Based on bow parameters.
- [x] **3D Printing Settings** — Smart print recommendations.

## Comfort Score: Ergonomic Suitability

The comfort score evaluates how well the bow suits the user's **hand size** and profile preferences.

### Formula

```
Comfort Score = 
(0.4 × Grip Score + 
 0.3 × Thickness Score + 
 0.2 × Stiffness Score + 
 0.1 × Curvature Score) × 100
```

### Rule Summary

| Factor          | Logic                                                                 |
|----------------|-----------------------------------------------------------------------|
| **Grip Score**  | 1.0 if grip is proportional to palm size (0.8–1.2 ratio), else lower |
| **Thickness**   | Penalizes thick bows for small palms, thin bows for large palms      |
| **Stiffness**   | Penalizes stiff bows for children, soft bows for pros                |
| **Curvature**   | Optimal range is 0.25–0.35 for most users                             |

## 3D Print Settings (Dynamic Heuristics)

| Setting         | Logic                                                                                              |
|----------------|----------------------------------------------------------------------------------------------------|
| **Material**    | - `Nylon/PETG` for high stiffness <br> - `PETG` for thin bows <br> - `TPU` for child safety |
| **Layer Height**| Finer layers (0.12mm) for high curvature/stiffness; otherwise 0.16–0.2mm                         |
| **Infill**      | More infill (30%) for heavier arrows/stiffer bows; else 20–25%                                   |
| **Supports**    | Needed if `curvature > 0.36`                                                                      |
| **Instructions**| TPU → flexibility; 45° angle for strong prints; else standard orientation                         |

## Arrow Adaptation Logic

Arrows are **automatically optimized** based on bow geometry and user type — no manual tweaking needed.

| Parameter        | Adaptation Logic                                                                                   |
|------------------|----------------------------------------------------------------------------------------------------|
| **Length**        | Depends on bow thickness, curvature, stiffness, and grip width. Clamped to 45–80mm range.         |
| **Weight**        | Heavier if the bow is powerful (stiff, long, large grip); scaled for balance and control          |
| **Tip Diameter**  | Safer (larger) tips for kids; sharper, smaller tips for pros; scaled for stiffness and grip width |

### Profile Modifiers

| User Type    | Arrow Length Factor | Tip Safety Factor |
|--------------|---------------------|-------------------|
| **Child**     | 0.9                 | 1.3 (larger tip)  |
| **Adult**     | 1.0                 | 1.0               |
| **Professional**| 1.1               | 0.85 (sharper)    |

## Performance-Based Optimization

You can **optimize the bow design for a target speed and draw force**, with the ability to **lock either constraint** for strict tuning. The system finds the best combination of bow parameters using heuristic penalty scoring and SciPy's `L-BFGS-B` optimization.
