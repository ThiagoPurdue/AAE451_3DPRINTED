# Structural Design

## Structures in Conceptual Design
During the conceptual design phase, we typically have little structural detail; however, the initial structural layout fundamentally dictates the aircraft's empty weight ($W_e$). The choices we make regarding load paths, component placement, and materials drive both the aerodynamic mold line (OML) and the manufacturing complexity. 

For our 3D-printed UAVs, standardizing structural architectures—like using carbon fiber tube spars with 3D-printed aerodynamic shells (the "skeleton-and-skin" approach)—allows us to build lightweight, highly predictable airframes.

:::{figure} lecture_09_structural_design_images/figure_page7_1.png
:name: fig-exploded-cad
:align: center
:width: 600px

Exploded view of a typical UAV CAD model showing structural and payload components.
:::

---

## The Wing Box
The wing box is the primary structural spine of the aircraft, resisting aerodynamic lift, drag, and twisting moments. 

:::{figure} lecture_09_structural_design_images/figure_page3_1.png
:name: fig-wingbox-components
:align: center
:width: 500px

Typical components of a wing box: spars, ribs, and skins.
:::

:::{table} Wing Box Components
:name: tab-wingbox
:align: left

| Component | Function |
|-----------|----------|
| **Spars** | The primary longitudinal load-carrying members. They carry shear forces and bending moments from aerodynamic lift and transfer them to the fuselage. |
| **Ribs** | Perpendicular to the spars, ribs maintain the airfoil shape, distribute aerodynamic pressure from the skins to the spars, and prevent local buckling. |
| **Skins** | The outermost layer providing the aerodynamic surface. Attached to ribs and spars, they also carry torsional loads. |
| **Stiffeners** | Longitudinal members (stringers) that reinforce the skin against compressive buckling. |
:::

### Wing Structural Loads
When designing the main spar, the shear force at the wing root is a critical design driver. It is fundamentally related to the load factor ($n$):

$$
V_{root} = \frac{W \cdot n}{2}
$$

*(Assuming a symmetric load where the lift equals $W \cdot n$ and is distributed evenly across both semi-spans).*

To calculate bending moments and shear forces accurately, you must understand how lift is distributed along the span. A common simplification is the **Shrenk approximation**, which averages a purely elliptical distribution with the actual wing planform shape.

---

## Margin of Safety (M.S.)
All structural components must be analyzed to ensure they do not fail under limit loads. We evaluate this using the **Margin of Safety (M.S.)**, which must always be strictly greater than zero ($M.S. > 0.0$).

### 1. Yield / Ultimate Stress
For tension, compression, and shear stresses, the M.S. is calculated against the material's allowable strength:
$$
M.S. = \frac{\text{Material Strength}}{\text{Maximum Expected Stress}} - 1.0
$$

### 2. Buckling
Long, slender members (like our carbon fiber tail booms or thin 3D-printed skins) are susceptible to buckling under compression.
$$
M.S._{buckling} = \frac{\text{Critical Buckling Load}}{\text{Maximum Compressive Load}} - 1.0
$$

### 3. Deflection
Structures must not only be strong but also stiff. Excessive wing deflection can alter aerodynamics or cause control surface binding. A common rule of thumb for UAV wings is to limit maximum wingtip deflection to less than 5% of the semi-span.

---

## Fuselage and Component Layout (CG)
The fuselage is the structural "bridge" connecting the wing, tail, landing gear, and payload. Its structural design is highly dependent on the layout of heavy internal components (Motor, Battery, Payload). 

You must maintain a detailed **Center of Gravity (CG) Table**, comparing the predicted weight and location of components in your CAD model to the actual built weights. If heavy components are moved to achieve a stable CG, the resulting moments of inertia will change, which affects dynamic stability and structural inertia loads.

### Fuselage Load Paths in Flight
During flight, the fuselage acts as a beam undergoing bending and shear.
- **Upward forces:** Wing lift at the wing root.
- **Downward forces:** Distributed weights of the motor, battery, payload, and the aerodynamic downforce from the horizontal tail.

:::{figure} lecture_09_structural_design_images/figure_page18_1.png
:name: fig-fuselage-loads
:align: center
:width: 600px

Fuselage load paths showing shear force and bending moment distributions.
:::

### Fuselage Loads During Landing
Landing is often the most critical load case for the fuselage. A hard landing can easily impart a 10g load ($n=10$) into the airframe through the landing gear mounts.

If $F_{total} = W \cdot n_{landing}$, this force must be distributed between the nose and main gear based on their distances to the CG:
$$
F_{main} = F_{total} \times \left( \frac{d_{nose\_to\_CG}}{L_{wheelbase}} \right)
$$
$$
F_{nose} = F_{total} \times \left( \frac{d_{main\_to\_CG}}{L_{wheelbase}} \right)
$$

These concentrated point loads induce massive bending moments through the fuselage, often requiring reinforced longerons and bulkheads directly above the gear struts.

---

## Landing Gear Placement
The geometric positioning of the landing gear is critical for ground handling.
- **Tip-back Angle:** The main gear must be placed far enough aft of the CG so the aircraft doesn't tip backward when resting or during a tail-strike on takeoff rotation (typically requiring a $\geq 15^\circ$ tip-back angle).
- **Tip-forward (Nose-over) Angle:** The nose gear must be placed far enough forward to prevent the aircraft from flipping on its nose during heavy braking or operating on rough grass.

---

## Critical Load Comparison
When analyzing the structure, consider the **V-n diagram**. You must evaluate multiple flight conditions:
- **Symmetric loads:** High-G pull-ups where lift is identical on both wings.
- **Asymmetric loads:** Rolling maneuvers where lift is significantly higher on one wing than the other. Often, the critical load condition for wing attachment fittings is an asymmetric, low-speed maneuver at a constant load factor.

> [!IMPORTANT]
> **Key Takeaway:** Understanding the load path is essential. For every critical component, you must create a table listing the Maximum Stress, the Failure Mode (Yield, Buckling), and the resulting Margin of Safety.
