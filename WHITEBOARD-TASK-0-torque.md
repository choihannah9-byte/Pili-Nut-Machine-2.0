# WHITEBOARD TASK 0 — Nip Draw-In & Peak Torque Re-Derivation

**Status: TOP OF THE WHITEBOARD LIST. Blocks: motor/reducer confirmation, chain tension check, shaft design, Stage 2 speed levels.**
**Rule: this task follows the re-derivation protocol — nothing below enters the thesis until a team member reproduces it from scratch and signs it.**

---

## Why this is Task 0

The independent panel review could not reproduce the briefing's peak-torque figure (~58 N·m), and the naive bound computed from the same inputs *exceeds* the motor's available torque. Every drivetrain number downstream (motor adequacy, chain tension ≈ 1.8 kN, shaft sizing) inherits from this one figure. It must be re-derived before anything is sized from it.

One correction to the review itself, for honesty: the review's 19°/μ ≥ 0.35 used **mid-grade** nuts. Re-checking the **worst in-grade case** (largest nut at the smallest per-grade gap, w = 36 mm at g = 21 mm) gives α = 23.2°, μ ≥ 0.43 — **the briefing's ~23°/0.42 was right, and the worst case is the correct design case.** The draw-in requirement stands as stated. The torque figure is the open item.

---

## Part 1 — Draw-in condition (re-derive, then sign)

Geometry: contact angle α when a nut of width w meets rollers of radius R at gap g:

    cos α = (R + g/2) / (R + w/2)        R = 75 mm

| Case | w (mm) | g (mm) | α | μ required = tan α |
|---|---|---|---|---|
| small, worst | 25 | 15 | 20.6° | 0.375 |
| medium, worst | 31 | 18 | 22.7° | 0.418 |
| **large, worst** | **36** | **21** | **23.2°** | **0.429** |

**Design statement:** the nut is pulled in only if measured shell-on-steel μ ≥ 0.43 (worst case). The serrations exist to guarantee this. **The friction measurement (inclined plane, dried shell on the actual roller surface finish) is what closes this line — schedule it in characterization week.** If measured μ < 0.43 bare, the serration grip must make up the difference and that becomes an explicit claim to defend.

---

## Part 2 — Peak torque: three estimates that must be reconciled

**Estimate A — naive entry-angle bound (overestimate).**
Tangential resisting force per roller at contact = F·sin α; torque per roller = F·R·sin α. At F = 1.6 kN (upper transverse fracture force), α = 23.2°:

    T_roller = 1600 × 0.075 × sin 23.2° = 47 N·m    →    both rollers (one drive): ≈ 94 N·m

This EXCEEDS the ~69 N·m available (below). But it is an overestimate — see C.

**Estimate B — briefing figure: ~58 N·m.** Basis unclear; could not be reconstructed from the stated formula. Do not carry it forward until someone reproduces it on the whiteboard, with its assumptions written next to it.

**Estimate C — the physically correct frame (this is the actual task).**
F and α do **not** peak together. Contact force starts near zero at first touch (large α) and reaches the fracture force only at ~1 mm of shell deformation — which happens **deep in the nip where the local contact angle is small**. The instantaneous torque is

    T(θ) = 2 · F(θ) · R · sin α(θ)

and its peak is far below Estimate A. Evaluating it needs the **force-vs-deformation curve** — which the team is already measuring on the compression rig for fracture verification. **Deliverable: overlay F(δ) from the rig onto the nip geometry (δ ↔ position ↔ α), integrate, and report T_peak and the crank-angle it occurs at.** This turns an unverifiable inherited number into an owned, defensible one.

**Cross-check — energy method (sanity floor):** fracture energy ≈ ½ × 1.5 kN × 1.05 mm ≈ 0.8–1.5 J per nut. At 40–60 nuts/min this is ~1 W average — trivial against 373 W. Average power was never the question; instantaneous peak torque is.

---

## Part 3 — What the motor actually has

- Available continuous torque at the output: T = P·η / ω = 373 W × ~0.7 (worm, catalogue η — verify) ÷ (36 rpm = 3.77 rad/s) ≈ **69 N·m**
- Single-phase capacitor-start motors deliver ~2–3× rated torque at breakaway — momentary peaks above 69 N·m do not stall the machine if brief; sustained demand above it does.
- **One nut in the nip at a time (verified):** roller surface speed = 36 rpm × π × 0.15 m = 0.283 m/s = 283 mm/s. At 60 nuts/min, spacing = 283 mm of surface travel per nut — the ~40 mm engagement zone holds one nut. Torque demands do not stack.

**Provisional conclusion to test, not to assume:** 0.5 hp is plausible because the true peak (Estimate C) will land well under Estimate A, and single-nut spacing means no stacking — but the number that goes in the thesis must come from the rig's F(δ) curve, not from this page.

---

## Sign-off block

| Item | Owner | Reproduced from scratch (date) | Adviser sighted |
|---|---|---|---|
| Draw-in α, worst case per grade | | | |
| μ measurement vs 0.43 requirement | | | |
| T_peak from rig F(δ) curve | | | |
| Motor margin incl. worm η from catalogue | | | |
| Chain tension at T_peak vs #40 working load | | | |
