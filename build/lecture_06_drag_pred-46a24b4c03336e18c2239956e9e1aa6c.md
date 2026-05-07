# Drag Prediction

## Introduction to Drag Prediction
In this chapter, we transition from initial sizing into the detailed aerodynamic characteristics of our aircraft. For any practical design—especially a 3D-printed UAV where battery capacity and motor size are tightly constrained—a reliable drag estimate is essential. 

Our primary question is: **What is the total aircraft drag coefficient ($C_D$) for a given geometry and flight condition?**

During the conceptual design phase, estimating drag accurately determines:
- Engine/Motor size required
- Total energy/battery capacity needed
- Overall feasibility and cost of the vehicle

Instead of running high-fidelity Computational Fluid Dynamics (CFD) on day one, we rely on a **subsonic drag build-up** method. This allows us to predict the aircraft $C_D$ based on empirical relationships applied to individual geometric components, making it perfect for rapid iterations in our sizing codes.

:::{figure} lecture_06_drag_prediction_images/figure_page27_2.jpeg
:name: fig-cirrus-sr22
:align: center
:width: 600px

A standard general aviation aircraft (such as the Cirrus SR22) used for drag build-up example calculations.
:::

---

## Three Types of Drag
Total drag is broadly categorized into three types:

1. **Parasite Drag ($C_{D,0}$ or $C_{D,p}$):** Drag that is always present, regardless of lift. This is highly dependent on the wetted area and aerodynamic shape.
2. **Induced Drag ($C_{D,i}$):** Drag due to lift. 
3. **Compressibility/Wave Drag ($C_{D,c}$ or $C_{D,w}$):** Drag due to supersonic effects. For our 3D-printed UAVs, which operate at low subsonic speeds, this term is generally negligible.

Thus, our total drag coefficient is typically:
$$
C_D = C_{D,0} + C_{D,i}
$$ (eq:total-drag)

---

## Parasite Drag
Parasite drag, or "zero-lift" drag, is always present and is strongly tied to boundary layer behavior. It consists of three main components:

1. **Skin Friction Drag:** Due to air "scrubbing" the surface. It is dependent on whether the boundary layer is laminar or turbulent.
2. **Pressure Drag (Form Drag):** Due to the body pushing flow out of the way, resulting in a non-ideal pressure distribution. Thicker bodies generally have higher pressure drag.
3. **Interference Drag:** Caused by flow from one component mixing and interfering with flow from another (e.g., wing-fuselage junctions).

### Subsonic Drag Build-Up
To estimate the total subsonic parasite drag, we add up the contributions of all wetted components exposed to the flow and include corrections for miscellaneous items (like landing gear or gaps).

$$
(C_{D,0}) \cdot S_{ref} = \sum_{i} \left( C_{f,i} \cdot FF_i \cdot Q_i \cdot S_{wet,i} \right) + D_{misc} / q
$$ (eq:drag-buildup)

:::{table} Drag Build-up Parameters
:name: tab-drag-buildup
:align: center

| Symbol | Description |
|--------|-------------|
| $C_{f,i}$ | Skin friction coefficient of component $i$ |
| $FF_i$ | Form factor (accounts for pressure drag) of component $i$ |
| $Q_i$ | Interference factor for component $i$ |
| $S_{wet,i}$ | Wetted area of component $i$ |
| $S_{ref}$ | Reference area (wing planform) |
:::

#### 1. Skin Friction Coefficient ($C_f$)
For conceptual design, assuming a 100% turbulent boundary layer provides a simpler, albeit slightly conservative, estimate. We use the Schlichting formula:

$$
C_f = \frac{0.455}{(\log_{10} Re)^{2.58}}
$$ (eq:skin-friction)

where the Reynolds number $Re = \frac{\rho V l}{\mu}$ is calculated using the characteristic length $l$ of the component. 

> [!TIP]
> 3D-printed surfaces typically have higher surface roughness due to layer lines. Unless extensively sanded and smoothed, assuming fully turbulent flow is both realistic and safe for our UAV designs.

#### 2. Wetted Area ($S_{wet}$)
The wetted area is the total surface exposed to the flow. 
- **Fuselage / Nacelles:** Can be approximated as cylinders with rounded or open ends.
  $$ S_{wet,f} \approx \pi D_f l_f \left( 1 - \frac{2}{\lambda_f} + \frac{\sqrt[3]{\lambda_f^2}}{2} \right) $$
- **Wings & Tails:** Approximately twice the planform area plus a small correction for thickness.
  $$ S_{wet,w} \approx 2.02 \times S_{planform} $$

#### 3. Form Factor ($FF$)
The form factor scales the skin friction drag to account for pressure drag based on the component's thickness or fineness ratio ($\lambda = l/D$).

For wings and tails (from Shevell):
$$
FF_w = 1 + Z \left(\frac{t}{c}\right) + 100 \left(\frac{t}{c}\right)^4
$$ (eq:ff-wing)
where $Z$ is a sweep correction factor (usually close to 1.0 for straight-wing UAVs).

For the fuselage (from Raymer):
$$
FF_f = 1 + \frac{60}{\lambda_f^3} + \frac{\lambda_f}{400}
$$ (eq:ff-fuselage)

#### 4. Interference Factor ($Q$)
Interference is notoriously hard to predict without CFD or wind tunnel testing. We use empirical guidelines:
- **Clean configurations** (e.g., well-faired low wing or mid-wing): $Q \approx 1.0$
- **Unfaired intersections** (e.g., low wing with no fillets): $Q \approx 1.2$
- **Nacelles mounted directly on surfaces:** $Q \approx 1.5$

For a 3D-printed UAV, you can often integrate smooth fillets directly into your CAD model, allowing you to assume $Q$ values close to 1.0 for your main wing-fuselage joint.

---

## Equivalent Flat Plate Area
Sometimes, drag is reported as an "equivalent flat plate area" or "drag area" ($f_e$). This is simply the parasite drag coefficient multiplied by the reference area:

$$
f_e = C_{D,0} \cdot S_{ref}
$$ (eq:flat-plate-area)

This is very useful for comparing the "cleanliness" of different aircraft sizes or for handling "unusual" components like landing gears or struts.

:::{table} Typical Component Flat Plate Areas (from Raymer)
:name: tab-fe-components
:align: center

| Component | $D/q$ ($f_e$) |
|-----------|---------------|
| Regular wheel and tire | 0.25 |
| Streamlined wheel and tire | 0.18 |
| Streamlined strut | 0.05 |
:::

To add these into your drag build-up, you simply convert them back to a $C_D$ contribution:
$$ \Delta C_{D,0} = \frac{f_e}{S_{ref}} $$

---

## Miscellaneous Drag
Even after a careful drag build-up, practical aircraft have "dirty" features that add drag. 
- **Leakage and Protuberances:** Gaps in control surfaces, cooling vents, antennas. For small propeller aircraft (like our UAVs), this typically adds 5% to 10% to the total $C_{D,0}$.
- **Fuselage Upsweep:** If the rear fuselage sweeps up aggressively (angle $> 15^\circ$), separation can occur, adding significant pressure drag.

## Suggested Reading
- **Raymer:** Chapter 12 (Aerodynamics)
- **Shevell:** Fundamentals of Flight
