
---

# Colpitts Oscillator (BJT – 2N2222) | LTspice Simulation

##  This project implements and analyses a **BJT-based Colpitts oscillator** using LTspice.

A Colpitts oscillator is an LC sinusoidal oscillator widely used in **RF and high-frequency applications**. It uses:

* An inductor (L1)
* A capacitive divider (C1–C2)
* A BJT amplifier (2N2222)
* Positive feedback for sustained oscillation

This simulation verifies oscillation startup, measures frequency, compares theory vs simulation, and evaluates signal quality using Fourier/THD analysis.


##  Circuit Parameters

| Component | Value  |
| --------- | ------ |
| V1        | 6 V    |
| Q1        | 2N2222 |
| R1        | 10 kΩ  |
| R2        | 1 kΩ   |
| L1        | 500 µH |
| C1        | 100 nF |
| C2        | 100 nF |

---

##  Simulation Directives

```
.tran 0 0.5m
.four 31.28k V(out)
```

---


## LC Tank Resonant Frequency

For a Colpitts oscillator:

[
f_{theory} = \frac{1}{2\pi\sqrt{L C_{eq}}}
]

Where:

[
C_{eq} = \frac{C1 \cdot C2}{C1 + C2}
]

---

### With Given Values:

[
C_{eq} = \frac{100nF \cdot 100nF}{100nF + 100nF}
]

[
C_{eq} = 50nF
]

[
f_{theory} = \frac{1}{2\pi\sqrt{500\mu H \cdot 50nF}}
]

[
f_{theory} ≈ 31.83 kHz
]

Expected oscillation ≈ **32 kHz**


---

##  Task 1 – Verify Oscillation

Run transient simulation.

Plot:

```
V(out)
```

Required screenshots:

* Startup region (growth from noise)
* Steady-state oscillation

You should observe:

* Exponential amplitude growth
* Stable sinusoidal steady-state

---

##  Task 2 – Measure Frequency (Time Domain)

Use cursors to measure one full period:

[
f_{sim} = \frac{1}{T}
]

Example:

If
T = 31.9 µs

[
f_{sim} ≈ 31.35 kHz
]

---

## Task 3 – Theory vs Simulation

Calculate % error:

[
%error = \frac{|f_{sim} - f_{theory}|}{f_{theory}} \times 100
]

Example:

| Parameter | Value     |
| --------- | --------- |
| f_theory  | 31.83 kHz |
| f_sim     | 31.35 kHz |
| % error   | 1.51 %    |

Small error is expected due to:

* Transistor parasitics
* Non-ideal inductor
* Internal capacitances (Cbe, Cbc)
* Bias network loading

---

##  Task 4 – Fourier / THD Analysis

Update:

```
.four <your_measured_frequency> V(out)
```

Example:

```
.four 31.35k V(out)
```

Open:

```
View → SPICE Error Log (Ctrl + L)
```

Record:

* DC component
* Fundamental amplitude
* Total Harmonic Distortion (THD)

Example Output:

| Parameter    | Value  |
| ------------ | ------ |
| DC Component | 2.91 V |
| Fundamental  | 1.82 V |
| THD          | 3.4 %  |

Low THD = cleaner sine wave.

---

#  Task 5 – Frequency Tuning Experiment

---

## Case A – L1 = 250 µH

Prediction:

Since frequency is:

[
f \propto \frac{1}{\sqrt{L}}
]

Reducing L → Frequency increases

Expected ≈ √2 increase (~45 kHz)

---

## Case B – C1 = C2 = 47 nF

New:

[
C_{eq} = \frac{47 \cdot 47}{47 + 47}
]

[
C_{eq} = 23.5nF
]

Prediction:

Reducing capacitance → Frequency increases significantly

---

##  Results Table

| Case     | L1 (µH) | C1 (nF) | C2 (nF) | Ceq (nF) | f_theory (kHz) | f_sim (kHz) | % Error |
| -------- | ------- | ------- | ------- | -------- | -------------- | ----------- | ------- |
| Original | 500     | 100     | 100     | 50       | 31.83          | 31.35       | 1.51    |
| A        | 250     | 100     | 100     | 50       | 45.00          | —           | —       |
| B        | 500     | 47      | 47      | 23.5     | 46.37          | —           | —       |

(Replace with your measured values)

---

# Concept Questions

### 1️ Role of C1–C2 Divider

The capacitive divider provides controlled positive feedback to the transistor. It determines the feedback fraction and helps satisfy the Barkhausen gain condition.

---

### 2️ Why Does Oscillation Start Without Input?

The oscillator starts due to internal noise in the transistor and circuit. If loop gain > 1 at the resonant frequency, noise gets amplified until steady-state oscillation is reached.

---

### 3️ Why Can f_sim Differ from f_theory?

Differences occur due to:

* Transistor internal capacitances (Cbe, Cbc)
* Parasitic inductance
* Bias network loading
* Non-ideal component tolerances
* Nonlinear operation

---


---
