# Electronic-Stethoscope-Moderate-Pre-Amplifier-Filtering-Stages
Designing of an electronic stethoscope without microcontrollers using basic principles of biomedical instrumentation.
# Low-Noise Analog Electronic Stethoscope Architecture

An advanced analog front-end system for biomedical instrumentation designed for clinical auscultation prototyping. Unlike conventional acoustic stethoscopes that merely transmit sound passively, this electronic alternative actively captures, amplifies, and filters body sounds (such as heart and lung murmurs) to overcome high ambient noise environments.

---

## 📋 Table of Contents
- [Project Overview]
- [Key Features]
- [Technical Specifications]
- [Circuit Design & Architecture]
- [MATLAB Frequency Response Analysis]
- [Proteus Simulation & Verification]
- [Performance & Results Data]
- [Project Structure]
- [Authors & Acknowledgments]

---

## 🔍 Project Overview

The **Low-Noise Analog Electronic Stethoscope** project addresses the inherent limitations of standard acoustic stethoscopes—specifically poor signal-to-noise ratios in noisy clinical or field environments. By integrating a high-gain analog front-end with precision active filtering, this system isolates microvolt-level acoustic vibrations from biological tissue and amplifies them into clear, actionable audio streams.

### Key Features
* **Acoustic Signal Conversion:** Employs an electret microphone transducer to capture mechanical chest wall vibrations.
* **High-Gain Amplification Stage:** Utilizes an operational amplifier configuration to deliver significant voltage gain.
* **Active Filtering:** Integrated low-pass and high-pass filters isolate clinical frequency bands while suppressing environmental and clothing friction noise.
* **Real-time Volume Control:** Adjustable output via an integrated potentiometer.

---

## ⚙️ Technical Specifications

| Parameter | Specification / Value | Notes |
| :--- | :--- | :--- |
| **Core Active Component** | IC741 Operational Amplifier | Configured in an inverting topology for stability |
| **Power Supply** | 12{V} DC Supply | Ensures proper operation and full signal swing |
| **Midband Voltage Gain (A_v)** | 1,000 (60 dB) | Standard operating gain |
| **Maximum System Gain** | 11,000 (80.8 dB) | Via gain divider mechanics |
| **Target Clinical Ranges** | Heart: 20 Hz - 150 Hz<br>Lung: 100 {Hz} - 1,000 {Hz} | Focused auscultation bands |
| **Low-Pass Filter** | Feedback capacitor C_2 = 120 nF & R_3 | Suppresses high-frequency noise & circuit hiss |
| **High-Pass / DC Blocking** | Coupling capacitors C_1 and C_5 | Filters baseline drift and movement artifacts |
| **Bias Compensation** | R_2 \approx 1.2 kΩ/1.2 MΩ | Matched to parallel combo of $R_1$ and $R_3$ |

---

## 🔌 Circuit Design & Architecture

1. **Sensing Stage:** The electret microphone transducer converts minute mechanical chest wall vibrations into microvolt-level electrical signals.
2. **Amplification & Noise Suppression Stage:** An inverting op-amp setup powered by the IC741 boosts signals up to a thousandfold while rolling off high-frequency interference using a feedback capacitor network (C_2 = 120 nF).
3. **Control Stage:** A variable potentiometer (RV_1) allows real-time output volume adjustment.
4. **Coupling & Output Stage:** DC decoupling capacitors protect downstream audio components from DC saturation and baseline shifts.

---

## 💻 MATLAB Code / Analysis

The repository includes a `/matlab` directory with scripts for calculating frequency response, filter Bode plots, and gain margins based on component values (R_1, R_3, C_2).

```matlab
% Frequency response and gain calculation script
| Component / Pin | Value / Rating | Function / Description |
| --- | --- | --- |
| **IC1** | LM 741 Op-Amp | Central Signal Amplifier |
| **R1 / R3** | 1.2 kΩ/1.2 MΩ | Gain Determination (Input/Feedback) |
| **C1 / C5** | 100 uF/47uF | Input/Output Signal Coupling |
| **C2** | 120 nF| Feedback Noise Suppression |
| **RV1** | 10 kΩ Pot | Variable Output Gain (Volume) |
Gain_magnitude = R3 / R1;
Gain_dB = 20 * log10(Gain_magnitude);
fprintf('Calculated Midband Gain: %.2f dB\n', Gain_dB);
```

---

## 🔬 Proteus Simulation & Verification

* **Setup Description:** Modeled in Proteus using virtual signal generators to inject weak millivolt-level physiological signals into the electret microphone node. Oscilloscope probes were placed across the output stage to monitor signal integrity and waveform distortion under a 12{V} rail.
* **Simulation Goals:** Verified that the 1,000 times amplification factor did not clip the op-amp output and that high-frequency noise was successfully attenuated by the feedback capacitor network.

---

## 📊 Performance & Results Data

* **Signal Clarity:** Successfully lifted microvolt-level acoustic signals into clear, audible waveforms without introducing severe phase distortion.
* **Noise Mitigation:** Effectively eliminated environmental and friction artifacts (such as stethoscope rubbing against clothing) using active filtering.
* **Stability:** Maintained a stable output baseline by blocking DC offset shifts caused by patient respiration and movement.

## Project Structure

```text
low-noise-electronic-stethoscope/
│
├── docs/
│   ├── images/
│   │   ├── circuit_schematic.png      # IC741 Inverting Amplifier with feedback filtering
│   │   ├── proteus_simulation.png     # Proteus schematic layout with oscilloscope window
│   │   ├── hardware_prototype.png     # Veroboard/Breadboard implementation (±12V DC)
│   │   └── oscilloscope_waveform.png  # Input vs. Processed Output waveform comparison
│   └── schematic_diagrams/
│
├── matlab/
│   └── frequency_response.m           # Gain and Bode plot calculations
│
├── proteus/
│   └── stethoscope_sim.pdsprj         # Proteus simulation workspace
│
└── README.md

👥 Authors & Acknowledgments

* **Project Team:** Dua Satar, Fatima Noor, Sana Naeem, Aliha Yaseen
* **Coursework Context:** Developed as part of collaborative biomedical instrumentation coursework focusing on cost-effective clinical prototyping using standard components (IC741).
