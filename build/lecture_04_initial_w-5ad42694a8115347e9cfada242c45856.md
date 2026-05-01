# Initial Vehicle Weight Estimation

## Our Approach
In this chapter, we focus on the initial weight estimation of electric-powered aircraft. The primary question is: **How much energy is needed to complete a design mission?**

To estimate this energy, our approach is as follows:
1. Consider how much energy is used in each mission phase.
2. Estimate the battery weight required to store that much energy.
3. Use historical data to determine the empty weight of the aircraft required to carry that battery plus any payload.

:::{table} Typical Mission Profile Phases
:name: tab-mission-phases
:align: center

| Phase | Description |
|-------|-------------|
| 1 | Warmup and takeoff |
| 2 | Climb |
| 3 | Cruise (Level flight) |
| 4 | Turning flight (if applicable) |
| 5 | Descent |
| 6 | Land and taxi |
:::

## Weight Breakdown
The total aircraft weight ($W$) is broken down into three main components:

$$
W = W_e + W_B + W_P
$$ (eq:weight-breakdown)

:::{table} Weight Component Definitions
:name: tab-weight-components
:align: center

| Symbol | Description |
|--------|-------------|
| $W_e$ | Empty weight (structure, landing gear, motor, etc.) |
| $W_B$ | Battery weight |
| $W_P$ | Payload weight |
:::

## Empty Weight Prediction
Empty weight ($W_e$) consists of anything that cannot be removed from the aircraft without a tool. Early in the design process, when very little detail about the aircraft is known, we must use predictors or **Weight Estimating Relationships (WER)** based on historical data of similar classes of aircraft.

This historical data is usually represented as the empty weight fraction ($W_e/W$) plotted against the total weight ($W$), which typically yields a curve fit that we can use for estimation.

For a battery-powered, fixed-wing remotely controlled airplane, specific historical relations for $W_e/W = f(W)$ can be established.

## Power Flow
To understand energy consumption, we must first understand the flow of power from the battery to the aircraft.

:::{table} Power Flow Chain
:name: tab-power-flow
:align: center

| Stage | Power | Efficiency | Range |
|-------|-------|------------|-------|
| Battery Output | $P_B$ | — | — |
| Motor Output | $P_m = \eta_m \cdot P_B$ | $\eta_m$ | 0.7–0.9 |
| Propeller Output | $P_r = \eta_p \cdot P_m$ | $\eta_p$ | 0.5–0.9 |
:::

Therefore, the total power required from the battery is related to the required thrust power by:

$$
P_r = \eta_p \cdot \eta_m \cdot P_B \quad \Rightarrow \quad P_B = \frac{P_r}{\eta_p \cdot \eta_m}
$$ (eq:power-flow)

## Energy and Mission Phases
Energy ($E$) is Power ($P$) multiplied by time ($t$):

$$
E_{battery} = P_B \cdot t = \frac{P_r \cdot t}{\eta_p \eta_m}
$$ (eq:battery-energy)

We divide the mission into various flight phases and determine the energy required for each segment:

$$
E_{total} = E_{to} + E_{wu} + E_{cl} + E_{lf} + E_{tf}
$$ (eq:total-energy)

The total energy required by the battery ($E_B$) determines the battery weight ($W_B$) through the **energy density** of the battery ($e_B$, in J/kg; e.g., Lithium Polymer $\approx 5.27 \times 10^5$ J/kg):

$$
W_B = \frac{E_{total}}{e_B}
$$ (eq:battery-weight)

Since the individual energy components are functions of the total aircraft weight (which is yet to be determined), we normalize by the unknown aircraft weight $W$. The problem boils down to finding the **battery weight fractions** ($W_{B,i}/W$) for each mission phase:

$$
\frac{W_B}{W} = \frac{W_{B,to}}{W} + \frac{W_{B,wu}}{W} + \frac{W_{B,cl}}{W} + \frac{W_{B,lf}}{W} + \frac{W_{B,tf}}{W}
$$ (eq:battery-fraction-total)

---

## Energy Consumption in Level Flight
In level flight, Lift equals Weight ($L = W$) and Thrust equals Drag ($T = D$).
The thrust power required is:

$$
P_r = T \cdot V = D \cdot V = \frac{W}{L/D} \cdot V
$$ (eq:level-power)

The energy required for a level flight time $t_{lf}$ is $E_{lf} = P_r \cdot t_{lf}$. Factoring in the efficiencies and energy density, the battery weight fraction for level flight is:

$$
\boxed{\frac{W_{B,lf}}{W} = \frac{V \cdot t_{lf}}{\eta_p \eta_m (L/D) \, e_B}}
$$ (eq:level-fraction)

## Energy Consumption in Turning Flight
In a turning flight with bank angle $\phi$ and turning radius $R$, the load factor $n = 1/\cos\phi$.
The lift increases, and consequently, drag increases by a factor of $n$.

$$
\boxed{\frac{W_{B,tf}}{W} = \frac{V \cdot t_{tf} \cdot n}{\eta_p \eta_m (L/D) \, e_B}}
$$ (eq:turning-fraction)

:::{table} Turning Flight Variables
:name: tab-turning-vars
:align: center

| Variable | Description |
|----------|-------------|
| $R$ | Turning radius (m) |
| $\phi$ | Bank angle (rad) |
| $n = 1/\cos\phi$ | Load factor |
| $g = 9.81$ m/s² | Gravitational acceleration |
:::

## Energy Consumption in Climbing Flight
In a climb to altitude $h$ at climb angle $\gamma$, the sum of forces yields:

$$
L = W \cos\gamma, \qquad T = D + W \sin\gamma
$$ (eq:climb-forces)

Using $D = L / (L/D) = W \cos\gamma / (L/D)$, the power required is:

$$
P_r = T \cdot V_{cl} = V_{cl} \cdot W \left( \frac{\cos\gamma}{L/D} + \sin\gamma \right)
$$ (eq:climb-power)

For a time to climb $t_{cl} = h / (V_{cl} \sin\gamma)$, the battery weight fraction is:

$$
\boxed{\frac{W_{B,cl}}{W} = \frac{V_{cl} \cdot t_{cl}}{\eta_p \eta_m \, e_B} \left( \frac{\cos\gamma}{L/D} + \sin\gamma \right)}
$$ (eq:climb-fraction)

## Energy Consumption in Warmup and Take-off
During take-off for a time $t_{to}$, the battery output power is $P_B = P_m / \eta_m$. 
Normalizing by the airplane weight to get the inverse of the power loading ($P_m/W$), the battery weight fraction for take-off is:

$$
\boxed{\frac{W_{B,to}}{W} = \frac{t_{to}}{\eta_m \left( W/P \right) \, e_B}}
$$ (eq:takeoff-fraction)

For warmup, a fraction $N$ of the take-off energy is typically assumed:

$$
\frac{W_{B,wu}}{W} = N \cdot \frac{W_{B,to}}{W}
$$ (eq:warmup-fraction)

---

## Solution Procedure Summary

:::{table} Solution Procedure Steps
:name: tab-solution-steps
:align: center

| Step | Action |
|------|--------|
| 1 | For a given payload $W_P$, calculate the total battery weight fraction $W_B/W$ from Eq. [](#eq:battery-fraction-total) |
| 2 | Compute battery weight: $W_B = (W_B/W) \times W$ |
| 3 | Rearrange the weight equation: $W - W_e = W_B + W_P$ |
| 4 | Plot $(W_B + W_P)$ and $(W - W_e)$ vs. total weight $W$ using the historical $W_e/W$ curve |
| 5 | The intersection gives the **Initial Weight Estimate** |
:::

## Suggested Reading
- **Gundlach:** Ch. 3
- **Raymer:** Ch. 3 and Ch. 20.11
