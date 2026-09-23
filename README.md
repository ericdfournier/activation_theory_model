# Zero-Emission (ZE) Building Retrofit Dynamics: Activation Energy Model

An interactive simulation and thermodynamic framework analogizing commercial and non-residential building decarbonization to **chemical reaction kinetics** and **activation barriers**.

---

## 📌 Conceptual Framework

Traditional building retrofit analyses focus strictly on static payback periods or discounted cash flows. This model frames the transition to zero emissions through the lens of **chemical kinetics and thermodynamics**:

```
[ Pre-Retrofit State ]  ──( Activation Barrier / Cap-Ex )──►  [ Zero-Emission State ]
      Reactants                   Transition State                    Products
 (Baseline Op-Ex/Carbon)     (Implementation & Disruption)      (Permanent Op-Ex Savings)
```

1. **Reactants (Pre-Retrofit Baseline):**
   - High kinetic stability with ongoing operational emissions, conventional utility bills, and pre-retrofit operations and maintenance (Op-Ex).
2. **Activation Barrier (Capital Expenditures & Disruption):**
   - Upfront capital expenditure (Cap-Ex), permitting delays, physical construction downtime, supply-chain hurdles, and commissioning phases required to cross the energetic hurdle.
3. **Products (Zero-Emission State):**
   - An *exothermic* financial and carbon return where ongoing building operational expenditures drop permanently below the pre-retrofit baseline.
4. **Catalysts (Policy & Financial Interventions):**
   - Financial incentives (rebates, tax credits) directly reduce barrier height ($E_a$).
   - Streamlined permitting and expedited inspections reduce barrier width / implementation duration ($\tau$), directly elevating property owner momentum.

---

## ⚡ Key Features

- **Dynamic Interactive Simulation Canvas:**
  - Real-time HTML5 2D canvas plotting project timeline vs. effective cost rate ($/month).
  - Visual differentiation between baseline Op-Ex, Cap-Ex deployment peak, commissioning decay curve, and discounted operational savings.
- **Physics-Based Reaction Ball Simulation:**
  - Simulates a rolling particle along the potential energy landscape $U(r) = \text{Cost}(r)$ subject to slope driving forces ($-\nabla U$) and velocity-dependent damping.
  - **5-Year Payback Threshold Rule:** Dynamically computes whether property owner motivation provides enough momentum to surmount the activation barrier or fall back into the pre-retrofit basin.
- **Financial & Kinetic KPI Engine:**
  - Net Present Value (NPV)
  - Simple Payback Period (years)
  - Project ROI ($\text{NPV} / \text{Cap-Ex}$)
  - Effective Cap-Ex Barrier (after incentives)
  - Cumulative Present Value Savings
  - Property Owner Motivation Telemetry (`Low`, `Medium`, `High`, `Very High`)
- **Interactive Controls & Presets:**
  - Sliders for Cap-Ex, implementation duration, commissioning window, Op-Ex delta, discount rates, pre-retrofit baseline, and evaluation horizons.
  - Policy interventions: speedup/barrier reduction (%) and catalytic incentives (%).
  - Pre-configured case studies: Scenarios A, B, C, and D.

---

## 📊 Pre-Configured Scenarios

| Scenario | Title | Description | Outcome |
| :--- | :--- | :--- | :--- |
| **A** | Standard / Optimal | Rapid payback (<5 yrs), standard 6-month implementation, prompt commissioning, deep operational savings. | **Barrier Overcome** (Rolls into ZE state) |
| **B** | Excessive Cap-Ex | High initial capital barrier ($550k+), prolonged payback >> 5 yrs creating an insurmountable economic hurdle. | **Rollback** (Returns to baseline) |
| **C** | Long Downtime | Identical Cap-Ex to standard, but elongated implementation (18 mos); disruption penalties degrade owner momentum. | **Rollback** (Halts on slope) |
| **D** | Increased Op-Ex | Unfavorable economics where post-retrofit operating costs exceed baseline (endothermic reaction). | **Immediate Rollback** (No driving force) |

---

## 🚀 Getting Started

The interactive model is completely self-contained in a single file with zero external build dependencies:

```bash
# Clone the repository
git clone https://github.com/ericdfournier/activation_theory_model.git

# Navigate to the project directory
cd activation_theory_model

# Open in your preferred browser
open activation_model.html
```

Or serve locally with any static web server:

```bash
# Using Python
python3 -m http.server 8000

# Using Node.js (npx)
npx serve .
```

Then visit `http://localhost:8000/activation_model.html`.

---

## 🧮 Mathematical Model

### 1. Effective Implementation Duration
$$\tau_{\text{eff}} = \max\left( \tau_{\text{install}} \times (1 - \text{speedup}),\, 0.5 \text{ months} \right)$$

### 2. Barrier Height Scaling (Peak Rate)
The peak expenditure rate ($/mo) scales inversely with implementation duration window to preserve total integrated Cap-Ex:
$$\Delta\text{CapEx}_{\text{eff}} = \text{CapEx}_{\text{total}} \times (1 - \text{catalyst})$$
$$\text{Peak Height} \propto \frac{\Delta\text{CapEx}_{\text{eff}}}{\left( \tau_{\text{eff}} / \tau_{\text{base}} \right)^{0.75}}$$

### 3. Transition Dynamics
- **Implementation Phase:** Symmetrical Gaussian deployment rate curve centered at peak implementation.
- **Commissioning Phase:** Smooth cubic Hermite polynomial decay ($3s^2 - 2s^3$) from implementation conclusion to stabilized operations.
- **Operational Phase:** Discounted annual savings projected across the evaluation horizon:
$$\Delta\text{OpEx}(t) = \frac{\Delta\text{OpEx}_0}{(1 + r)^t}$$

### 4. Owner Motivation & Kinetic Momentum
Critical velocity ($v_c$) to clear the potential energy summit is solved via bisection search over numerical trajectory integration. Initial launch velocity ($v_0$) scales dynamically based on whether simple payback meets the target threshold ($\text{Payback} < 5\text{ yrs}$).

---

## 🛠️ Technologies Used

- **HTML5 Canvas:** Custom responsive 2D rendering with Device Pixel Ratio (HiDPI) scaling and mouse hover telemetry.
- **JavaScript (ES6+):** Numerical trajectory integration, bisection threshold solver, and real-time state management.
- **Tailwind CSS (CDN):** Responsive layout and dark-mode UI design.
- **Font Awesome:** System iconography.

---

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.
