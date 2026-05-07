# Propulsion System Sizing

## Introduction
Once the initial sizing is complete and the required power loading ($W/P$) is determined from the constraint diagram, the next step in the design of our 3D-printed UAV is selecting an appropriate motor, propeller, ESC, and battery combination.

In this chapter, we explore how to bridge the gap between our abstract constraint analysis and real-world hardware. We will learn how to size the electric propulsion system based on power and thrust requirements.

---

## Propeller Theory and Geometry
A propeller is essentially a rotating twisted wing. Because the rotational velocity of the blade increases with distance from the hub, the blade pitch angle ($\beta$) is varied along the length to maintain a consistent angle of attack ($\alpha$).

For most RC aircraft propellers, the pitch is defined as the forward distance the propeller would theoretically move in one revolution if there were no slippage:

$$
Pitch = 2\pi r \tan(\beta)
$$

### Non-Dimensional Parameters
Propeller performance is typically evaluated using non-dimensional coefficients. These are crucial when reading propeller performance data (such as those provided by APC Propellers):

1. **Advance Ratio ($J$):** Represents the ratio of forward speed to tip speed.
   $$ J = \frac{V}{n D} $$
2. **Thrust Coefficient ($C_T$):** 
   $$ C_T = \frac{T}{\rho n^2 D^4} $$
3. **Power Coefficient ($C_P$):**
   $$ C_P = \frac{P}{\rho n^3 D^5} $$
4. **Propeller Efficiency ($\eta_p$):** The ratio of useful power output to mechanical power input.
   $$ \eta_p = \frac{T \cdot V}{P_{in}} = \frac{C_T \cdot J}{C_P} $$

*(Note: $n$ is revolutions per second (rev/s), $D$ is the propeller diameter, and $\rho$ is air density).*

---

## Electric Power Flow
For internal combustion engines, performance is measured in brake horsepower. For electric propulsion, we must account for the efficiency losses as electrical power from the battery is converted into thrust.

$$
P_{electrical} \xrightarrow{\eta_{ESC}} P_{ESC,out} \xrightarrow{\eta_{motor}} P_{mechanical} \xrightarrow{\eta_{prop}} P_{thrust}
$$

When you determine the **Power Required** from your constraint diagram, you are determining the *mechanical* power required by the motor output shaft (assuming you factored $\eta_p$ into the constraint equations). To find the required *electrical* power ($P_{elec}$):

$$
P_{elec} = \frac{P_{mech, req}}{\eta_{motor} \cdot \eta_{ESC}}
$$

> [!TIP]
> **Recommended Initial Efficiencies:**
> - $\eta_{p, cruise} \approx 0.65$
> - $\eta_{p, takeoff} \approx 0.50$
> - $\eta_{motor} \approx 0.80$
> - $\eta_{ESC} \approx 0.95$

---

## Static Thrust and Takeoff
Your propulsion system must provide enough static thrust ($T_0$) to accelerate the aircraft during the takeoff roll. A common approximation is to evaluate the average forces at $0.7 \times V_{TO}$:

$$
T_0 \approx \frac{W V_{TO}^2}{2 g S_{TO}} + D_{TO} + \mu (W - L_{TO})
$$ (eq:static-thrust)

When selecting a motor/propeller combo, refer to static thrust charts provided by the motor manufacturer (e.g., Cobra Motors) or utilize online calculators like **eCalc** to ensure your setup meets this $T_0$ requirement.

---

## Selection Process
The iterative process for sizing your propulsion system is:
1. **Determine Power Required:** Use the design point from your constraint diagram. Let's say $P_{mech} = 850$ W.
2. **Calculate Electrical Power:** Using $\eta_{motor} = 0.8$ and $\eta_{ESC} = 0.95$, $P_{elec} = 850 / (0.8 \times 0.95) \approx 1118$ W.
3. **Select System Voltage:** Determine battery cells (e.g., 4S LiPo = 14.8 V nominal, or 6S LiPo = 22.2 V nominal). If 6S is used: $I_{max} = 1118 \text{ W} / 22.2 \text{ V} \approx 50$ Amps.
4. **Choose Motor and ESC:** Select a motor capable of handling $>1118$ W and $>50$ A continuously. Select an ESC rated for at least $60$ A (giving a safety margin).
5. **Select Propeller:** Consult motor manufacturer test data to find a propeller that provides the required thrust at the calculated current draw without overheating the motor.

> [!WARNING]
> **Integration Considerations:**
> - **Thrust Line:** Ensure your motor thrust line passes near the center of gravity (CG). If mounted high (like on a pylon), adding thrust will create a nose-down pitching moment.
> - **Fuselage Blockage:** A bulky, 3D-printed square fuselage directly behind the propeller will significantly reduce the effective thrust. Streamline the nose section!
