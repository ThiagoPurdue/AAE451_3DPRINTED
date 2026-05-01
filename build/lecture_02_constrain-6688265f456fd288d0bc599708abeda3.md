# Initial Vehicle Sizing by Constraint Analysis

## Purpose of the Constraint Diagram
The correct sizing of an airplane depends on numerous important variables. A clearly stated mission plays a paramount role in this respect and allows the sizing to be accomplished using mathematical tools. Constraint analysis is used to assess the relative significance of selected aircraft performance parameters on the design with respect to a set of requirements.

Specifically, it allows one to understand which combinations of wing loading ($W/S$) and power loading ($P/W$) permit the aircraft to simultaneously meet dissimilar performance requirements, such as rate of climb, take-off distance, and others.

## Overview of Constraint Analysis

Given mission requirements, we perform a constraint analysis using a constraint diagram. From this, we select design parameter values such as:
- Stall Speed ($V_s$)
- Cruise Speed ($V_{cr}$)
- Climb rate or climb angle
- Take-off run
- Maneuver loads

**Design Space:** The design space is that region within which all the constraints are met. For each quantitative requirement of the mission, we find the relationship between the wing loading and the power loading that exactly satisfies that requirement.

The general form of the Constraint Equation is:
$$ \left( \frac{P}{W} \right)_{Sea-Level} = f\left( \frac{W}{S} \right) $$

For each requirement, we find the region where the vehicle violates that requirement and indicate the forbidden region with a hash mark. The feasible region (where we want to design our aircraft) is the intersection of all allowed regions. We typically prefer smaller engines (lower $P/W$ for cost/weight) and smaller wings (higher $W/S$), so the optimal point often lies at a corner of the feasible space.

## 1st Constraint: Sizing to Stall Speed

To satisfy the stall speed requirement, the aircraft must be able to generate enough lift to balance its weight at stall velocity $V_s$.

$$ L = W = \frac{1}{2} \rho V_s^2 S_{ref} C_{L_{max}} $$

Rearranging for Wing Loading ($W/S$):

$$ \frac{W}{S} = \frac{1}{2} \rho V_s^2 C_{L_{max}} $$

Where:
- $W$ = weight
- $S$ = wing area ($S_{ref}$)
- $\rho$ = air density
- $V_s$ = stall velocity
- $C_{L_{max}}$ = maximum lift coefficient

This is a vertical line on the constraint diagram. Any wing loading greater than this value will violate the stall speed requirement.

## 2nd Constraint: Sizing to Cruise Speed

Assuming the aircraft is in level flight during cruise, the power required ($P_{req}$) must be less than or equal to the power available from the engine ($P_{avail} \cdot \eta_p$).

$$ P_{req} = D \cdot V_{cr} = \frac{1}{2} \rho V_{cr}^3 S C_D $$

Where:
- $\eta_p$ is the propeller efficiency
- $C_D$ is the drag coefficient

Cruise speeds for propeller-driven airplanes are typically calculated at 75 to 80 percent maximum power. Often, induced drag is small compared to profile drag, giving:
$$ C_D = C_{D_0} + 0.1 C_{D_0} = 1.1 C_{D_0} $$

If cruise is at sea-level, the constraint equation is:

$$ \frac{P}{W} \ge \frac{1.1 \rho V_{cr}^3 C_{D_0}}{2 \eta_p \left( \frac{W}{S} \right)} $$

This equation creates a curve on the constraint diagram where power loading must be greater than or equal to the required power loading for a given wing loading.

![Constraint Diagram: Cruise](lecture_02_images/figure_page14_1.jpeg)

## 3rd Constraint: Sizing to Climb Requirement

For an aircraft in a climb:
- Thrust direction: $T \cos(\alpha + \epsilon_T) - D = W \sin(\gamma)$
- Lift direction: $L + T \sin(\alpha + \epsilon_T) = W \cos(\gamma)$

Assuming $\alpha + \epsilon_T$ is small and $T \sin(\alpha + \epsilon_T)/W$ is small, we have:
$$ L \approx W $$
$$ D = \frac{W}{L/D} $$

Climbing at $L/D = 0.866 (L/D)_{max}$, the thrust required is:
$$ T = \frac{W}{0.866 (L/D)_{max}} + W \sin(\gamma) $$

Accounting for propeller efficiency $\eta_p = \frac{T \cdot V_{climb}}{P}$:

$$ \frac{P}{W} \ge \frac{V_{climb}}{\eta_p} \left( \frac{1}{0.866 (L/D)_{max}} + \sin(\gamma) \right) $$

![Constraint Diagram: Climb](lecture_02_images/figure_page18_1.jpeg)

## 4th Constraint: Sizing to Maneuver Requirement

Consider an airplane in a level constant velocity turn. The load factor is $n = 1 / \cos(\phi)$, where $\phi$ is the bank angle.

The required thrust to maintain load factor $n$ while banking at constant airspeed and altitude is:
$$ T = q S C_{D_0} + \frac{n^2 W^2}{q S \pi e AR} $$

Dividing by weight and multiplying by velocity to get power:
$$ \frac{P}{W} \ge \frac{V}{\eta_p} \left( \frac{q C_{D_0}}{W/S} + \frac{n^2 (W/S)}{q \pi e AR} \right) $$

Where:
- $q = \frac{1}{2} \rho V^2$
- $n$ = load factor
- $AR$ = aspect ratio
- $e$ = Oswald efficiency factor

![Constraint Diagram: Maneuver](lecture_02_images/figure_page22_1.jpeg)

## 5th Constraint: Take-Off

During the take-off run ($S_{to}$), the aircraft accelerates from $V = 0$ to $V = V_{to}$ (typically $1.1 V_s$ to $1.3 V_s$). The general form for the take-off constraint will depend on runway friction ($\mu$) and aerodynamic forces during the ground roll.

Based on Sadraey's derivation (Chapter 4), the power loading constraint is:

$$ \frac{W}{P} \le \frac{\eta_P}{V_{to}} \left[ \frac{1 - \exp\left( \frac{0.6 g \rho C_{D_g} S_{to}}{W/S} \right)}{\mu - \left( \mu + \frac{C_{D_g}}{C_{L_g}} \right) \exp\left( \frac{0.6 g \rho C_{D_g} S_{to}}{W/S} \right)} \right] $$

Where:
- $S_{to}$ = maximum take-off distance
- $C_{D_g}, C_{L_g}$ = drag and lift coefficients during the ground roll
- $\mu$ = runway friction coefficient
- $g$ = gravitational acceleration


*(Detailed derivation can be found in Sadraey's text book, Chapter 4).*

## The Master Constraint Diagram

By plotting all the above constraints ($P/W$ vs. $W/S$), we identify the **Design Space**. The preferred design point is usually the one that minimizes the engine size (lowest $P/W$) and minimizes wing size (highest $W/S$) while staying within the feasible region.

> **Note:** See the Jupyter Notebook `DBF_Constraint_Diagram.ipynb` for the Python implementation and visualization of these constraints.

## Reading & References
- **Gundlach:** Ch. 3, 9.4
- **Roskam (Vol. I):** Ch. 3
- **Gudmundsson:** Ch. 3
- **Sadraey:** Ch. 4
