# Aircraft Performance

## Introduction to Performance Assessment
Once the aircraft geometry is defined and a propulsion system is selected, we must perform a detailed performance assessment. This phase acts as a sanity check on the initial predictions made in our sizing code. 

Instead of relying on simplified master equations, we now use our calculated **drag polar** and the **thrust/power available** from our specific motor/propeller choice to verify that the aircraft actually meets the mission requirements (Takeoff Distance, Rate of Climb, Cruise Speed, etc.).

For a 3D-printed UAV, we often have higher drag and lower thrust margins than full-scale aircraft, making numerical performance simulations critical.

---

## Takeoff Performance
Takeoff is an accelerating, unsteady maneuver. To determine the takeoff distance accurately, we must integrate the equations of motion numerically (e.g., using `ode45` in MATLAB or `scipy.integrate` in Python).

The fundamental equation of motion in the longitudinal direction is:
$$
\sum F_x = T - D - F_F = m \cdot a
$$ (eq:takeoff-eom)

### 1. Thrust ($T$)
Thrust during the takeoff roll is not constant; it decreases as forward velocity increases. You should use a multivariable curve fit based on your propeller data:
$$
T(V, rpm) = a \cdot rpm + b \cdot V + c \cdot rpm \cdot V + d
$$

### 2. Drag ($D$)
Drag must account for **ground effect**. The proximity of the ground reduces induced drag.
$$
D = \frac{1}{2} \rho V^2 S \left( C_{D,0} + K_g \frac{C_L^2}{\pi e AR} \right)
$$
where $K_g$ is the ground effect interference factor.

### 3. Friction Force ($F_F$)
The rolling friction depends on the weight on the wheels, which decreases as aerodynamic lift builds up.
$$
F_F = \mu [W - L] = \mu \left[ m \cdot g - \frac{1}{2} \rho V^2 S C_{L,g} \right]
$$
where $\mu$ is the coefficient of rolling friction (e.g., higher for grass than for a paved runway) and $C_{L,g}$ is the lift coefficient while rolling on the ground.

### Takeoff Tradeoffs
When running the simulation, you must define the takeoff criteria:
- **Fixed Angle of Attack (AoA):** The aircraft rolls at a constant $C_{L,g}$ until it lifts off naturally when $L = W$ (often at $V_{LO} \approx 1.2 V_{stall}$).
- **Rotational Takeoff:** The aircraft rolls at a low $C_{L,g}$ to minimize drag, then rapidly increases AoA (rotates) at a specific speed ($V_R \approx 1.1 V_{stall}$) to lift off. This requires elevator authority.

---

## Climb Performance
Once airborne, the aircraft must climb. The equations are driven by the excess thrust available.

The climb angle ($\gamma$) is determined by:
$$
\sin(\gamma) = \frac{T - D}{W}
$$

The **Rate of Climb (R.O.C.)** is the vertical velocity component:
$$
R.O.C. = V \sin(\gamma) = \frac{(T - D) \cdot V}{W} = \frac{Excess Power}{W}
$$ (eq:rate-of-climb)

To predict time to climb or altitude profiles, you evaluate $T(V, rpm)$ and $D(V, h)$ iteratively as air density changes with altitude.

---

## Cruise Performance
In level, unaccelerated flight, Lift equals Weight ($L = W$) and Thrust equals Drag ($T = D$).

We plot both **Thrust Required** and **Thrust Available** as functions of velocity:

1. **Thrust Required ($T_R$):**
   $$ T_R = D = \frac{1}{2} \rho V^2 S \left( C_{D,0} + \frac{C_L^2}{\pi e AR} \right) $$
   *(Remember that $C_L = W / (\frac{1}{2}\rho V^2 S)$).*

2. **Thrust Available ($T_A$):** From your multivariable propulsion fit.

Where the $T_A$ curve intersects the $T_R$ curve on the right-hand side represents the **Maximum Level Speed ($V_{max}$)**. The distance between the curves represents the **Excess Thrust**. 

Alternatively, multiplying these curves by Velocity ($V$) yields the **Power Required** and **Power Available** curves. For electric aircraft, evaluating the power required at your target cruise speed directly dictates your steady-state current draw and, consequently, your maximum range/endurance.

---

## Suggested Reading
- **Raymer:** Chapter 17 (Performance and Flight Mechanics)
- **Gudmundsson:** Chapters 18-22 (General Aviation Aircraft Design)
