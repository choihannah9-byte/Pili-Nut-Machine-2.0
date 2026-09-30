# pili-cracker-models

Interactive 3D models for the TUP BSME pili nut cracker capstone.
`npm install && npm run dev`, or import the repo into StackBlitz.

## What's in here

| Model | File | Status |
|---|---|---|
| **Rev D assembly** | `src/PiliAssemblyModelRevD.jsx` | **Current.** Loads by default. |
| Nip simulator | `src/PiliNipSimulator.jsx` | Current. Single-nut crack behaviour vs. gap. |
| Rev C2 assembly | `src/PiliAssemblyModelRevC.jsx` | Superseded by Rev D. Kept for comparison. |
| Rev B assembly | `src/PiliAssemblyModelRevB.jsx` | Superseded. |

`src/App.jsx` is the model switcher. `standalone/` holds self-contained HTML
exports of the same scenes — useful for emailing to the adviser, but the JSX
files are the source of truth. Edit the JSX, not the standalone.

## Rev D at a glance

Linear gravity cascade, flow runs **+x to -x**: hopper and three-deck sorter on
the right, buffer bins and V-channel in the middle feeding the nip, screen box
and trays on the left. Coordinates are **mm, y-up, floor at y = 0**; front is
**+z** (operator side), drive is **-z**.

- **Grading** — three oscillating decks (31 / 25 / 20 mm apertures) on a rocker-mounted
  frame, discharging through z-offset openings into three buffer bins with a
  single-cutout interlock bar. `BOTTOM_DECK_PERFORATED = true`, so the bottom
  deck screens at 20 mm over a fines drawer.
- **Feeding** — collecting funnel into a covered single-lane V-channel (38 mm
  nominal). The V seats the nut's triangular section so it enters the nip
  tip-first with the ridge toward the adjustable roller.
- **Cracking** — two 150 dia x 80 mm AISI 1045 rollers at 36 rpm with shallow grip
  serrations. Minimum clearance is a **rigid screw hard stop**; die springs only
  preload the carriage against it and act as overload protection.
- **Drive** — 0.5 hp motor to a 40:1 self-locking worm reducer to the **fixed-roller
  shaft (the main shaft)**. The adjustable roller is chain-synchronised only. The
  same shaft carries the screen eccentric and the sorter take-off sprocket.
- **Separation** — catch funnel, coarse screen, sorting tray at the front, 8 mm
  screen, cross-flow air split, kernel and chip trays.
- **Scale reference** — a 1.70 m operator and a 1 m floor scale bar are drawn in
  the `scale` subsystem. They are not machine parts; toggle them off in the panel.

Measured envelope: **approx. 1126 x 546 x 1397 mm** (W x D x H).

## Known open items

- **Envelope vs. Ch. 3.** Sections 3.2/3.8 state 950 x 450 x 700 mm. A gravity
  cascade of this stack does not fit in 700 mm of height. That figure is a
  placeholder pending real CAD; the model is deliberately **not** bent to match it.
- **Separation arrangement.** The two-stage layout (coarse screen, sorting tray,
  8 mm screen, air split) came from the 8 Sept verification note and is **not yet
  in the Ch. 1-3 text**. Kept as-is pending team review.
- **Placeholders pending measurement.** Deck apertures, 38 mm lane width, ~40 deg
  chute angles, 4 mm oscillation throw, blower velocity.
- **Peak torque.** Still Whiteboard Task 0 (`docs/WHITEBOARD-TASK-0-torque.md`).
  Nothing in the drivetrain should be sized from the current figure.

## Rev D audit pass (2026-09)

The first Rev D build had four floating sub-assemblies and three clipping
conflicts. All are fixed; the assembly is now a **single connected component**
(344 parts, verified by AABB connectivity analysis).

| Was | Now |
|---|---|
| Screen-box springs sat 80 mm above their posts and speared the ring, so the box hung off its drive linkage alone | Springs seat post-cap (160) to ring-seat (240); cap and seat plates added |
| Waste drawer floated with no support | Two fixed runners spanning the spring posts; drawer widened to 240 to land on them |
| Blower, its motor and the duct floated | Blower mounting plate across the base cross rails, plus a duct support leg |
| Tray shelf floated 4 mm above the base rails; hood hung 5 mm below its rails | Shelf dropped onto the rails with bearers; hood hung on four hanger straps |
| Adjustable divider spanned only part of the hood | Full-width divider with slotted adjusting brackets |
| Deck eccentric occupied the same z as the 11T sprocket | Eccentric moved outboard on a lengthened jackshaft; drive lug carried out to clear the small-grade trough |
| Static hopper cone clipped the **oscillating** deck-frame top rail | Hopper raised 40 mm, mounting flange added on the cradle beams |
| Part inspector had a fixed `min-height` inside a flex column, so long descriptions overlapped the content below | `height: auto` plus `flex: 0 0 auto`; the box grows with its text |

**The screen box is driven, and always was.** The linkage is main-shaft eccentric,
connecting rod, rocker lever (pivoted on the frame at y = 430), link, ring lug.
It sits at z approx. -100 to -125, behind the side plates, which is why it reads
as "absent" from the default view. Use the **Screen drive** camera button.

## Panel controls

Run/stop, feed on/off, playback speed, grade select (drives the gate interlock),
roller gap (or drag the handwheel in the scene), per-location nut counts, manual
repass, exploded view, subsystem visibility, and a part inspector — click any
part. Camera buttons across the bottom of the viewport.
