# Initial Vehicle Weight Estimation

## Our Approach
In this lecture, we focus on the initial weight estimation of electric-powered aircraft. The primary question is: **How much energy is needed to complete a design mission?**

To estimate this energy, our approach is as follows:
1. Consider how much energy is used in each mission phase.
2. Estimate the battery weight required to store that much energy.
3. Use historical data to determine the empty weight of the aircraft required to carry that battery plus any payload.

The typical mission profile involves the following phases:
1. Warmup and takeoff
2. Climb
3. Cruise (Level flight)
4. Turning flight (if applicable/maneuver)
5. Descent
6. Land and taxi

## Weight Breakdown
The total aircraft weight ($W$) is broken down into three main components:

$$ W = W_e + W_B + W_P $$

Where:
- $W_e$ = Empty weight (aircraft structure, landing gear, motor, etc.; does not include battery or payload)
- $W_B$ = Battery weight
- $W_P$ = Payload weight

## Empty Weight Prediction
Empty weight ($W_e$) consists of anything that cannot be removed from the aircraft without a tool. Early in the design process, when very little detail about the aircraft is known, we must use predictors or **Weight Estimating Relationships (WER)** based on historical data of similar classes of aircraft.

This historical data is usually represented as the empty weight fraction ($W_e/W$) plotted against the total weight ($W$), which typically yields a curve fit that we can use for estimation.

For a battery-powered, fixed-wing remotely controlled airplane, specific historical relations for $W_e/W = f(W)$ can be established.

## Power Flow
To understand energy consumption, we must first understand the flow of power from the battery to the aircraft:

1. **Battery Output Power ($P_B$)**: The raw power delivered by the battery.
2. **Motor Output Power ($P_m$)**: The mechanical power produced by the motor.
   $$ P_m = \eta_m \cdot P_B $$
   Where $\eta_m$ is the motor efficiency ($\sim 0.7 - 0.9$).
3. **Propeller Output Power ($P_p$ or $P_r$)**: The effective thrust power delivered to the aircraft.
   $$ P_r = P_p = \eta_p \cdot P_m $$
   Where $\eta_p$ is the propeller efficiency ($\sim 0.5 - 0.9$).

Therefore, the total power required from the battery is related to the required thrust power by:
$$ P_r = \eta_p \cdot \eta_m \cdot P_B \quad \Rightarrow \quad P_B = \frac{P_r}{\eta_p \cdot \eta_m} $$

## Energy and Mission Phases
Energy ($E$) is Power ($P$) multiplied by time ($t$):
$$ E_{battery} = P_B \cdot t = \frac{P_r \cdot t}{\eta_p \eta_m} $$

We divide the mission into various flight phases and determine the energy required for each segment:
$$ E_{total} = E_{to} + E_{wu} + E_{cl} + E_{lf} + E_{tf} $$
(Take-off, Warmup, Climb, Level Flight, Turning Flight)

The total energy required by the battery ($E_B$) determines the battery weight ($W_B$) through the **energy density** of the battery ($e_B$, e.g., Joules/kg).
$$ W_B = \frac{E_{total}}{e_B} $$

Since the individual energy components are functions of the total aircraft weight (which is yet to be determined), we normalize by the unknown aircraft weight $W$. The problem boils down to finding the **battery weight fractions** ($W_{B,i}/W$) for each mission phase:

$$ \frac{W_B}{W} = \frac{W_{B,to}}{W} + \frac{W_{B,wu}}{W} + \frac{W_{B,cl}}{W} + \frac{W_{B,lf}}{W} + \frac{W_{B,tf}}{W} $$

---

### Energy Consumption in Level Flight
In level flight, Lift equals Weight ($L = W$) and Thrust equals Drag ($T = D$).
The thrust power required is:
$$ P_r = T \cdot V = D \cdot V = \frac{W}{L/D} \cdot V $$

The energy required for a level flight time $t_{lf}$ is $E_{lf} = P_r \cdot t_{lf}$. Factoring in the efficiencies and energy density, the battery weight fraction for level flight is:

$$ \frac{W_{B,lf}}{W} = \frac{V \cdot t_{lf}}{\eta_p \eta_m (L/D) e_B} $$

### Energy Consumption in Turning Flight
In a turning flight with bank angle $\phi$ and turning radius $R$, the load factor $n = 1/\cos\phi$.
The lift increases, and consequently, drag increases by a factor of $n$.

$$ \frac{W_{B,tf}}{W} = \frac{V \cdot t_{tf} \cdot n}{\eta_p \eta_m (L/D) e_B} $$

### Energy Consumption in Climbing Flight
In a climb to altitude $h$ at climb angle $\gamma$, the sum of forces yields:
$$ L = W \cos\gamma $$
$$ T = D + W \sin\gamma $$
Using $D = L / (L/D) = W \cos\gamma / (L/D)$, the power required is:
$$ P_r = T \cdot V_{cl} = V_{cl} \cdot W \left( \frac{\cos\gamma}{L/D} + \sin\gamma \right) $$

For a time to climb $t_{cl}$, the battery weight fraction is:

$$ \frac{W_{B,cl}}{W} = \frac{V_{cl} \cdot t_{cl}}{\eta_p \eta_m e_B} \left( \frac{\cos\gamma}{L/D} + \sin\gamma \right) $$

### Energy Consumption in Warmup and Take-off
During take-off for a time $t_{to}$, the battery output power is $P_B = \frac{P_m}{\eta_m}$. 
Normalizing by the airplane weight to get the inverse of the power loading ($P_m/W$), the battery weight fraction for take-off is:

$$ \frac{W_{B,to}}{W} = \frac{t_{to}}{\eta_m \left( \frac{P_m}{W} \right)^{-1} e_B} $$

For warmup, a fraction (e.g., $N\%$) of the take-off energy is typically assumed:
$$ \frac{W_{B,wu}}{W} = N \cdot \frac{W_{B,to}}{W} $$

---

## Solution Procedure Summary
1. For a given Payload ($W_P$), calculate the total battery weight fraction ($W_B/W$) based on the mission analysis:
   $$ \frac{W_B}{W} = \sum \frac{W_{B,i}}{W} $$
   Which gives us: $W_B = \left( \frac{W_B}{W} \right) W$.

2. We know the total weight is $W = W_e + W_B + W_P$, which can be rearranged as:
   $$ W - W_e = W_B + W_P $$

3. Plot $(W_B + W_P)$ and $(W - W_e)$ on the same plot against total weight $W$ (using the historical empty weight curve for $W_e$). The intersection of these two curves yields the **Initial Estimate of Weight**.

## Suggested Reading
- **Gundlach:** Ch. 3
- **Raymer:** Ch. 3 and Ch. 20.11
