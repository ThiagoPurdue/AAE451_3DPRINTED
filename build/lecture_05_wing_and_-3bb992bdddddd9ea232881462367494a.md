# Wing and Tail Design

## Wing Design -- Main Definitions

Lift comes with a price: **drag** and a **nose-down pitching moment**. Wing design decisions should therefore reflect the performance requirements, including stall speed, maximum speed, take-off run, range, and endurance.

:::{table} Wing Design Parameters to Determine
:name: tab-wing-params
:align: center

| Parameter | Symbol | Description |
|-----------|--------|-------------|
| Reference area | $S_{ref}$ | Wing planform area |
| Aspect ratio | $AR = b^2/S$ | Span-to-chord ratio |
| Taper ratio | $\lambda = c_{tip}/c_{root}$ | Tip-to-root chord ratio |
| Sweep | $\Lambda$ | Leading or quarter-chord sweep angle |
| Dihedral | $\Gamma$ | Upward angle of wing panels |
| Twist (washout) | $\epsilon_t$ | Spanwise twist angle |
| Airfoil(s) | — | Cross-section profile |
| Incidence | $i_w$ | Wing setting angle relative to fuselage |
| Flap & aileron | — | High-lift and lateral control devices |
| MAC | $\bar{c}$ | Mean Aerodynamic Chord |
:::

## Wing Arrangement

### Number of Wings
- **Monoplane (single wing):** the practical and modern solution, enabled by advanced materials.
- **Biplane:** used when span is limited; shorter span delivers higher roll control, but at higher weight.

### Wing Location

:::{table} High Wing vs. Low Wing Trade-offs
:name: tab-wing-location
:align: center

| High Wing | Low Wing |
|-----------|----------|
| Increases $C_{L_{max}}$ (ground effect) | Better take-off performance |
| Aircraft is laterally more stable | Less frontal area |
| Produces slightly more lift | Less induced drag |
| Usually lower stall speed | More lateral control |
| Drag produces nose-down pitching moment | Less stable ($C_{l_\beta} > 0$) |
| Less downwash on the tail | More downwash effect on the tail |
| Less lateral control | Less ground effect for take-off/landing |
:::

## Airfoil Selection

The airfoil is the fundamental building block of the wing. Selection criteria must balance competing objectives.

:::{table} Airfoil Selection Criteria
:name: tab-airfoil-criteria
:align: center

| Objective | Design Driver |
|-----------|---------------|
| Maximum lift ($C_{l_{max}}$) | Take-off and landing performance, stall speed |
| Minimum drag ($C_{d_{min}}$) | Range, endurance, max speed |
| Low pitching moment ($C_{m_{ac}}$) | Reduced trim drag, smaller tail |
| Gentle stall characteristics | Safety and recoverability |
:::

:::{figure} lecture_05_images/figure_page7_1.png
:name: fig-airfoil-comparison
:width: 100%
:align: center

Representative aerodynamic coefficients of selected airfoils at low Reynolds number ($Re \approx 200{,}000$), comparing lift-curve slope, maximum $C_L$, stall angle, maximum $L/D$, and minimum drag.
:::

### Wing Incidence

The wing incidence angle $i_w$ should be set such that the fuselage generates **minimum drag during cruise**, i.e., the fuselage angle of attack is approximately $0deg$ during the cruise condition.

## Considerations about Aspect Ratio

The aspect ratio $AR$ has a fundamental impact on the aerodynamic performance of the wing.

The **3D wing lift-curve slope** is related to the 2D airfoil lift-curve slope $C_{l_\alpha}$ by:

$$
C_{L_\alpha} = \frac{C_{l_\alpha}}{1 + \frac{C_{l_\alpha}}{\pi \cdot AR}}
$$ (eq:3d-lift-slope)

The **induced drag factor** is:

$$
K = \frac{1}{\pi \cdot e \cdot AR}
$$ (eq:induced-drag-factor)

And the **maximum lift-to-drag ratio** is:

$$
\left(\frac{L}{D}\right)_{max} = \frac{1}{2\sqrt{K \cdot C_{D_0}}}
$$ (eq:ld-max)

Where $C_{D_0}$ is the zero-lift drag coefficient, and $e$ is the Oswald efficiency factor.

:::{table} Effects of Aspect Ratio
:name: tab-ar-effects
:align: center

| Low AR | High AR |
|--------|---------|
| Increases stall angle $\alpha_{stall}$ | Higher $L/D$ |
| Reduces $C_{L_\alpha}$ | Higher $C_{L_\alpha}$ |
| Lower structural weight | Higher structural weight |
| Better roll rate | Longer span, higher bending loads |
:::

> **Design rule:** The horizontal tail should have an AR lower than the wing to ensure the tail stalls after the wing (no twist required on the tail).

## Considerations about Taper Ratio

The taper ratio $\lambda = c_{tip}/c_{root}$ influences the spanwise lift distribution, structural weight, and manufacturing complexity.

$$
\bar{c} = \frac{2}{3} c_{root} \frac{1 + \lambda + \lambda^2}{1 + \lambda}
$$ (eq:mac)

:::{table} Effects of Taper Ratio
:name: tab-taper-effects
:align: center

| Effect | Description |
|--------|-------------|
| $\lambda \approx 0.4--0.5$ | Approximates elliptical lift distribution |
| $\lambda < 0.4$ | Reduces weight, but tip stall risk increases |
| $\lambda = 1.0$ | Rectangular wing — easy to manufacture |
| Decreases $I_{xx}$ | Improves lateral control (roll rate) |
:::

## Considerations about Twist (Washout)

Wing twist (washout) reduces the angle of attack at the tip relative to the root. This serves two purposes:
1. **Prevents tip stall before root stall**, which is critical for maintaining aileron effectiveness and safe stall recovery.
2. **Helps approximate an elliptical spanwise lift distribution**, reducing induced drag.

A typical washout angle for general aviation is $\epsilon_t \approx 2deg--5deg$.

---

## Tail Design

The horizontal and vertical tails provide pitch and yaw stability and control. The key parameters to determine are listed below.

:::{table} Tail Design Parameters
:name: tab-tail-params
:align: center

| Horizontal Tail | Vertical Tail |
|-----------------|---------------|
| $S_t$ — planform area | $S_v$ — planform area |
| $b_t$ — span | $b_v$ — height |
| $l_t$ — tail arm | $l_v$ — tail arm |
| $\Lambda_t$ — sweep | $\Lambda_v$ — sweep |
| Airfoil | Airfoil |
| $AR_t$ | $AR_v$ |
| $\lambda_t$ — taper ratio | $\lambda_v$ — taper ratio |
| $i_t$ — incidence | — |
:::

:::{figure} lecture_05_images/figure_page26_1.jpeg
:name: fig-control-surfaces
:width: 80%
:align: center

Aircraft control surfaces: ailerons, flaps, elevator, rudder, fin, and stabilizer (Source: Gudmundsson).
:::

## Pitching Moment and Longitudinal Stability

The total pitching moment about the center of gravity ($M_{cg}$) is the sum of contributions from the wing, fuselage, propulsion, and tail:

$$
C_{M_{cg}} = C_{M_{ac,w}} + C_{M_{fus}} + C_{M_{prop}} + C_{M_{tail}}
$$ (eq:moment-components)

Expanding:

$$
M_{cg} = M_{ac,w} + (x_{cg} - x_{ac}) L_w + M_{ac,t} - l_t L_t + M_F + M_P
$$ (eq:moment-balance)

The **pitching moment coefficient** about the c.g. is:

$$
C_{M_{cg}} = C_{M_{ac,w}} + \left(C_{L_W} + C_{L_t}\frac{S_t}{S_w}\right)\frac{(\bar{x}_{cg} - \bar{x}_{ac,w})}{\bar{c}} - C_{L_t} V_H + C_{M_{ac,t}} V_H \frac{\bar{c}_t}{l_t}
$$ (eq:cm-cg)

Where the **horizontal tail volume coefficient** is defined as:

$$
\boxed{V_H = \frac{S_t \cdot l_t}{S_w \cdot \bar{c}}}
$$ (eq:vh)

:::{figure} lecture_05_images/figure_page15_1.png
:name: fig-pitching-moment-contributions
:width: 80%
:align: center

Pitching moment contributions from the tail (empenage), fuselage, and wing. For static stability, the total aircraft curve must have a negative slope ($\partial C_m / \partial \alpha < 0$).
:::

## Neutral Point

The **neutral point** ($x_n$) is the c.g. location at which the aircraft has **neutral static stability** ($C_{M_\alpha} = 0$). It is defined by:

$$
\bar{x}_n = \bar{x}_{ac} + \frac{C_{L_{\alpha_t}}}{C_{L_\alpha}} \left(1 - \frac{\partial \varepsilon}{\partial \alpha}\right) V_H
$$ (eq:neutral-point)

Where $\partial \varepsilon / \partial \alpha$ is the downwash gradient at the tail.

:::{figure} lecture_05_images/figure_page20_1.png
:name: fig-static-margin
:width: 80%
:align: center

Static longitudinal stability: for a statically stable aircraft, the neutral point (n.p.) is aft of the center of gravity (c.g.). The static margin is the distance between them.
:::

## Static Margin

The **static margin** (SM) is a measure of longitudinal stability:

$$
\boxed{SM = \bar{x}_n - \bar{x}_{cg} = -\frac{\partial C_M}{\partial C_L}}
$$ (eq:static-margin)

- **Larger SM** → more stable, less agile
- **SM ≈ 0** → neutrally stable
- **SM < 0** → statically unstable

:::{table} Typical Static Margins for Various Aircraft
:name: tab-static-margins
:align: center

| Aircraft | Static Margin |
|----------|:------------:|
| Cessna 172 | 0.19 |
| Learjet 35 | 0.13 |
| Boeing 747 | 0.27 |
| P-51 Mustang | 0.05 |
| F-16C | 0.01 |
| X-29 | −0.33 |
:::

:::{figure} lecture_05_images/figure_page22_1.png
:name: fig-cm-cl-curve
:width: 80%
:align: center

Example pitching moment ($C_M$) vs. lift coefficient ($C_L$) curve. The slope $dC_M/dC_L$ is the negative of the static margin.
:::

## Scissor Plot ($S_t / S$)

The **scissor plot** is a design tool that plots the required tail-to-wing area ratio ($S_t / S$) as a function of the c.g. location ($\bar{x}_{cg}$). It establishes the forward and aft c.g. limits based on three criteria:

1. **Forward limit (stability):** ensures adequate static margin.
2. **Stall recovery:** ensures sufficient nose-down control authority at stall.
3. **Take-off rotation:** ensures sufficient nose-up moment to rotate during take-off.

The intersection of these constraints determines the minimum required tail size.

## Trim Condition

An aircraft is **trimmed** when it does not rotate about the c.g. in flight. Two conditions must be satisfied simultaneously:

$$
C_M = 0 \qquad \text{and} \qquad C_L = C_{L_{trim}} = \frac{2W}{\rho V_\infty^2 S_w}
$$ (eq:trim-conditions)

Two unknowns must be solved: the angle of attack $\alpha_{trim}$ and the elevator deflection $\delta_{e_{trim}}$.

$$
\alpha_{trim} = \frac{C_{M_0} C_{L_{\delta_e}} + C_{M_{\delta_e}} (C_{L_{trim}} - C_{L_0})}{C_{L_\alpha} C_{M_{\delta_e}} - C_{L_{\delta_e}} C_{M_\alpha}}
$$ (eq:alpha-trim)

$$
\delta_{e_{trim}} = -\frac{C_{M_0} C_{L_\alpha} + C_{M_\alpha} (C_{L_{trim}} - C_{L_0})}{C_{L_\alpha} C_{M_{\delta_e}} - C_{L_{\delta_e}} C_{M_\alpha}}
$$ (eq:delta-trim)

Where the elevator effectiveness derivatives are:

$$
C_{L_{\delta_e}} = \frac{S_t}{S_w} C_{L_{\delta_{e_t}}}, \qquad C_{M_{\delta_e}} = C_{L_{\delta_{e_t}}} \frac{S_t}{S_w} (\bar{x}_{cg} - \bar{x}_{ac,w}) - C_{L_{\delta_{e_t}}} V_H
$$ (eq:elevator-derivatives)

## Trim Drag

Trim drag is the additional drag resulting from the deflection of the horizontal stabilizer and elevator to maintain the trim condition. Since the tail typically produces a downward force, the wing must produce extra lift to compensate, resulting in a slight increase in induced drag:

$$
C_D = C_{D_0} + \frac{C_{L_w}^2}{\pi \cdot e_w \cdot AR_w} + \frac{C_{L_t}^2}{\pi \cdot e_t \cdot AR_t} \cdot \frac{S_t}{S_w}
$$ (eq:trim-drag)

## Suggested Reading
- **Raymer:** Ch. 6
- **Gudmundsson:** Ch. 24 and 25
- **Drela:** Basic Aircraft Design Rules
- **Nelson:** Flight Stability and Automatic Control
- **Sadraey:** Ch. 5
