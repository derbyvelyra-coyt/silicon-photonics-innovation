<div align="center">

# Silicon Photonics & Optical Computing

**A Technical Reference on Waveguiding, Electro-Optic Modulation, and Photonic Integration in Modern Semiconductor Architectures**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-active-brightgreen.svg)]()
[![Contributions welcome](https://img.shields.io/badge/contributions-welcome-blue.svg)](#contributing)
[![Made with Markdown](https://img.shields.io/badge/docs-markdown-informational.svg)]()

</div>

---

## Table of Contents

- [Overview](#overview)
- [Core Physical Principles](#core-physical-principles)
  - [1. High Index Contrast & Waveguiding](#1-high-index-contrast--waveguiding)
  - [2. Carrier Dispersion Effect (Electro-Optic Modulation)](#2-carrier-dispersion-effect-electro-optic-modulation)
- [On-Chip Components](#on-chip-components)
- [Applications & Quantum Interconnects](#applications--quantum-interconnects)
- [Mathematical Frameworks & References](#mathematical-frameworks--references)
- [Repository Structure](#repository-structure)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

**Silicon Photonics (SiP)** leverages silicon as an optical transmission medium, encoding and routing data as photons rather than electrons. By integrating optical interfaces directly onto silicon integrated circuits, SiP addresses the bandwidth density, latency, and thermal-dissipation limitations inherent to copper-based electrical interconnects in high-performance computing (HPC) and quantum information systems.

This repository serves as a living technical reference — documenting the physical principles, component-level building blocks, and system-level applications that define the current state of the art in photonic integration.

---

## Core Physical Principles

### 1. High Index Contrast & Waveguiding

Silicon ($\text{Si}$, refractive index $n \approx 3.45$ at $1550\,\text{nm}$) surrounded by silicon dioxide cladding ($\text{SiO}_2$, $n \approx 1.45$) produces a high refractive-index contrast, enabling strong total internal reflection (TIR) and tight optical confinement.

| Property | Specification |
|---|---|
| Waveguide cross-section | typically $220\,\text{nm} \times 500\,\text{nm}$ |
| Minimum bend radius | $\sim 5\,\mu\text{m}$, with negligible radiation loss |
| Operating windows | **O-band** ($1260$–$1360\,\text{nm}$), **C-band** ($1530$–$1565\,\text{nm}$) |
| Silicon bandgap | $E_g \approx 1.12\,\text{eV}$ (transparent at telecom wavelengths) |

### 2. Carrier Dispersion Effect (Electro-Optic Modulation)

Pure silicon exhibits no linear electro-optic (Pockels) effect due to its centrosymmetric crystal structure. High-speed modulation is instead achieved through the **plasma dispersion effect**, whereby free-carrier concentration modulates the real refractive index:

$$
\Delta n = -\frac{e^2 \lambda^2}{8 \pi^2 c^2 \varepsilon_0 n} \left( \frac{\Delta N_e}{m_{ce}^*} + \frac{\Delta N_h}{m_{ch}^*} \right)
$$

Modulating electron ($\Delta N_e$) and hole ($\Delta N_h$) concentrations alters both the real refractive index ($\Delta n$) and the absorption coefficient ($\Delta \alpha$), forming the physical basis for phase and amplitude modulation — typically implemented via PN-junction carrier depletion.

---

## On-Chip Components

| Component | Primary Function | Typical Implementation |
|---|---|---|
| Grating / Edge Couplers | Off-chip ↔ on-chip optical coupling | Subwavelength gratings (SWG), inverse tapers |
| Mach-Zehnder Modulator (MZM) | Electrical-to-optical conversion | Balanced/unbalanced interferometer, PN depletion |
| Micro-Ring Resonators (MRR) | Wavelength-selective routing (WDM) | High-Q resonant filters |
| Photodetectors | Optical-to-electrical conversion | Epitaxially grown germanium (Ge) on silicon |

---

## Applications & Quantum Interconnects

- **Co-Packaged Optics (CPO):** Integrating optical transceivers directly onto the same substrate as processors and GPUs, bypassing parasitic losses associated with copper traces.
- **Photonic Integrated Circuits (PICs):** Multi-channel Wavelength Division Multiplexing (WDM) enabling terabit-scale data transfer at sub-picojoule energy per bit ($< 1\,\text{pJ/bit}$).
- **Integrated Quantum Photonics:** On-chip manipulation of single-photon qubits via phase shifters and directional couplers, paired with integrated superconducting nanowire single-photon detectors (SNSPDs).

---

## Mathematical Frameworks & References

**Maxwell's equations in dielectric waveguides:**

$$
\nabla \times (\nabla \times \mathbf{E}) - k_0^2 n^2(\mathbf{r})\, \mathbf{E} = 0
$$

**Free-carrier absorption (Soref & Bennett model):** empirical relations describing refractive-index and absorption-coefficient shifts as a function of carrier concentration at $\lambda = 1550\,\text{nm}$.

---

## Repository Structure

```
.
├── docs/           # Extended technical notes and derivations
├── simulations/    # FDTD / photonic simulation scripts (Lumerical, Meep, etc.)
├── figures/        # Diagrams and reference plots
└── README.md
```

---

## Contributing

Contributions are welcome. If you'd like to propose corrections, extend the theoretical background, or share simulation scripts (Lumerical, Meep, PyFDTD, etc.), please open a Pull Request or start a Discussion.

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-topic`)
3. Commit your changes
4. Open a Pull Request describing the addition

---

## License

Distributed under the **MIT License**. See [`LICENSE`](LICENSE) for details.

<div align="center">

*Maintained as an open technical documentation log.*

</div>
