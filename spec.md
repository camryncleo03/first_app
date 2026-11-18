# Beam Designer

## Purpose
A beam design tool for engineers and students. The user sets up a beam,
places loads on it, and picks a steel or lumber section. The app shows the
shear, moment, and deflection diagrams and checks whether the beam is
strong and stiff enough, updating instantly as anything changes.

## Users
A civil engineering student checking a homework beam, or an engineer
sizing a floor beam or deck joist.

## Inputs
- Support type
  - Control: radio or segmented control.
  - Options: Simply Supported (default) or Cantilever (fixed at the left end).
- Span
  - Units: ft.
  - Range: 4 to 40 ft.
  - Default: 20 ft.
  - Controls: a slider and a number box that stay in sync.
  - Slider step: 1 ft.
  - Number-box step: 0.25 ft.
- Loads
  - At least one load must remain in the beam.
  - Loads are listed in a panel, with an edit control and a remove control for each load.
  - Point loads:
    - Magnitude units: kips, downward positive.
    - Magnitude range: 0.1 to 100 kips.
    - Magnitude default: 1 kip.
    - Magnitude step: 0.1 kip.
    - Position units: ft.
    - Position range: -span to 2span.
    - Position default: midspan for simply supported beams or the free end for cantilevers.
    - Position step: 0.25 ft.
    - Controls: a number box and a draggable point-load arrow in the drawing.
    - Point-load arrows snap to 0.25 ft.
    - A point load outside the beam's 0-to-span interval is ignored and does not draw an arrow or contribute to calculations.
  - Uniform loads:
    - Magnitude units: kips/ft, downward positive.
    - Magnitude range: 0.01 to 10 kips/ft.
    - Magnitude default: 1 kip/ft.
    - Magnitude step: 0.01 kip/ft.
    - Start and end units: ft.
    - Start and end range: -span to 2span.
    - Start default: 0 ft.
    - End default: span.
    - Position step: 0.25 ft.
    - Controls: separate number boxes for the start and end positions.
    - Start must not be greater than end. If a load extends outside the beam, only the
      portion from 0 to span is included in calculations.
  - Controls: "Add point load" and "Add uniform load" buttons.
- Material and section
  - Material options: Steel and Douglas Fir-Larch No. 2.
  - Material default: Steel.
  - Material control: dropdown.
  - Section options: the sections in the table for the selected material.
  - Section default: W12x26.
  - Section control: dropdown, populated with sections for the selected material.
  - When the material changes, choose the first section in that material's table.

  Material and section data:

  Steel W-shapes (E = 29,000 ksi, allowable bending stress Fb = 30 ksi):

  | Section | Ix (in^4) | Sx (in^3) | Weight (lb/ft) |
  |---------|-----------|-----------|----------------|
  | W8x10   | 30.8      | 7.81      | 10 |
  | W10x12  | 53.8      | 10.9      | 12 |
  | W12x26  | 204       | 33.4      | 26 |
  | W14x22  | 199       | 29.0      | 22 |
  | W16x26  | 301       | 38.4      | 26 |
  | W18x35  | 510       | 57.6      | 35 |
  | W21x44  | 843       | 81.6      | 44 |
  | W24x55  | 1350      | 114       | 55 |

  Douglas Fir-Larch No. 2 lumber (E = 1,600 ksi, Fb = 0.900 ksi):

  | Section | Ix (in^4) | Sx (in^3) |
  |---------|-----------|-----------|
  | 2x8     | 47.63     | 13.14     |
  | 2x10    | 98.93     | 21.39     |
  | 2x12    | 177.98    | 31.64     |

- Deflection limit
  - Options: L/240 or L/360.
  - Default: L/360.
  - Control: radio or segmented control.
- Waste factor
  - Units: percent.
  - Range: 0 to 15%.
  - Default: 5%.
  - Step: 1%.
  - Control: slider with a synchronized percentage readout; no number box.
  - Apply the waste factor to the recommended section's weight for display:
    adjusted weight = section weight x (1 + waste factor / 100).
  - Steel section weights from the section table are available for this calculation.
  - Lumber has no weight in the section table, so do not show an adjusted lumber weight.
- Self-weight is ignored.

## Calculations
- Reactions from statics.
- Shear V(x) and moment M(x) along the beam, at 1 ft spacing or finer,
  plus exactly at every load point and load start/end.
- Deflection y(x) by integrating M/EI twice with the boundary conditions
  for the support type (y = 0 at both supports; or y = 0 and slope = 0 at
  the fixed end).
- Bending stress fb = |M max| x 12 / Sx (ksi). Bending check passes if
  fb <= Fb.
- Deflection check passes if |y max| <= L/240 or L/360 (L in inches).
- Lightest passing section: of the sections in the chosen material, the
  lightest steel section that passes both checks (if two weigh the same,
  the one with the larger Ix), or the first lumber size in the table
  that passes.
- Units: kips, ft, and kip-ft on screen; inches for deflection.

## Outputs
- A beam drawing with the supports, load arrows (point loads as single
  arrows, uniform loads as a row of small arrows), and the reactions.
- Three diagrams stacked under the beam and lined up with it on the same
  x scale: shear (kips), moment (kip-ft), and deflected shape (in). Each
  diagram is filled and shows its maximum value labeled at its location.
- Moving the mouse over any diagram shows a vertical line across all three
  with the values of V, M, and y at that x.
- Two check cards: Bending and Deflection. Each shows the actual value, the
  allowable value, a bar for the ratio (green under 70%, amber 70-100%,
  red over 100%), and PASS or FAIL.
- A line suggesting the lightest passing section, with a button to use it.
- Everything updates immediately whenever any input changes.

## Look and feel
- Opens with an example already loaded (20 ft simply supported W12x26
  with a 1 kip/ft uniform load over the full span), so it is useful the
  moment it opens.
- Clean and professional, like a commercial engineering web app: light
  background, white cards with soft shadows, one accent color, a modern
  system font, generous spacing. No clutter.
- Inputs in a panel on the left; drawing, diagrams, and checks on the
  right. On a phone, the panels stack.
- Every input has a short label with units. Hovering over a check card
  explains the formula used.

## Validation
1. Simply supported, 20 ft, W12x26, uniform 1 kip/ft over the full span:
   reactions 10 k and 10 k; max shear 10 k; max moment 50.0 kip-ft at
   10 ft; fb = 17.96 ksi; max deflection 0.609 in at 10 ft; L/360 =
   0.667 in; both checks pass.
2. Simply supported, 20 ft, W12x26, point load 10 k at 5 ft: reactions
   7.5 k (left) and 2.5 k (right); max moment 37.5 kip-ft at 5 ft;
   fb = 13.47 ksi; max deflection 0.340 in at 8.82 ft.
3. Cantilever, 10 ft, W12x26, point load 5 k at the free end: reaction
   5 k and fixed-end moment 50 kip-ft; max deflection 0.487 in at the free
   end (PL^3/3EI); L/360 = 0.333 in, so deflection fails.
4. Simply supported 12 ft 2x10 joist, uniform 0.05 kip/ft: max moment
   0.90 kip-ft; fb = 0.505 ksi; max deflection 0.147 in; both pass.

## Out of scope
- Self-weight, shear stress, lateral-torsional buckling, load
  combinations, and continuous beams.
- Saving designs.
