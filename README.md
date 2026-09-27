# Quantum Scattering

A compact numerical study of one-dimensional quantum scattering. The project follows a Gaussian wave packet from free propagation to barrier scattering, compares time-dependent simulations with stationary transmission, and explores resonances using a box basis and complex scaling.

The repository includes the simulation code, reproducible scripts, selected figures, animations, and a technical report. The public version has been prepared without personal identifiers.

## What is explored

- Free propagation and spreading of a Gaussian wave packet
- A smooth finite-width approximation to the Dirac delta function
- Stationary transmission through a symmetric double barrier
- Time-dependent reflection, partial transmission, and resonant tunnelling
- Localized and resonance-like states in a finite box basis
- Complex scaling, resonance poles, and Breit-Wigner line shapes

## Stationary scattering

The double barrier produces two clear transmission resonances. Away from the peaks, the barriers largely reflect an incoming state; close to a resonance, the probability density builds up in the central well and transmission approaches unity.

![Transmission probability through the double barrier](results/part3_stationary_scattering/transmission_profile.png)

The numerical transmission coefficient is obtained by matching the stationary wave function across a discretized potential. The continuum reference curves and selected resonant wave functions are included in [`results/part3_stationary_scattering`](results/part3_stationary_scattering).

## Wave-packet dynamics

The time-dependent calculation makes the same structure visible in real space. These three snapshots show representative blocked, partially transmitted, and transmitted packets.

| Mostly reflected | Partially transmitted | Mostly transmitted |
|---|---|---|
| ![Blocked wave packet](results/part4_wavepacket_scattering/blocked.png) | ![Partially blocked wave packet](results/part4_wavepacket_scattering/partially_blocked.png) | ![Passing wave packet](results/part4_wavepacket_scattering/pass.png) |

The animations show the packet approaching the barriers, temporarily occupying the well, and separating into reflected and transmitted components.

| Reflection | Partial transmission | Transmission |
|---|---|---|
| ![Blocked packet animation](results/part4_wavepacket_scattering/blocked.gif) | ![Partially blocked packet animation](results/part4_wavepacket_scattering/partially_blocked.gif) | ![Passing packet animation](results/part4_wavepacket_scattering/pass.gif) |

Narrow packets centred on the two stationary resonances isolate the quasi-bound dynamics more clearly.

| First resonance | Second resonance |
|---|---|
| ![Wave packet at the first resonance](results/part4_wavepacket_scattering/first_resonance_zoom.gif) | ![Wave packet at the second resonance](results/part4_wavepacket_scattering/second_resonance_zoom.gif) |

## Free propagation and basis calculations

Before introducing a potential, the free-particle calculation checks translation of the packet centre and dispersive broadening.

![Free Gaussian wave-packet propagation](results/part1_free_gaussian/free_propagation.gif)

A finite box basis is then used to identify states concentrated near the interaction region. This provides a useful bridge between bound-state intuition and metastable scattering resonances.

![Selected localized states](results/part5_box_basis/three_localized_states.png)

## Complex scaling

Complex rotation separates resonance poles from the rotated continuum. Stable complex eigenvalues provide the resonance energy and width, which can be compared with the stationary transmission peaks through a Breit-Wigner approximation.

| Complex spectrum | Resonance line shape |
|---|---|
| ![Complex-scaled eigenvalue spectrum](results/part6_complex_scaling/complex_eigenvalues_all.png) | ![Breit-Wigner and finite-difference transmission](results/part6_complex_scaling/breit_wigner_profiles_zoom.png) |

## Repository structure

```text
quantum-scattering/
├── src/quantum_scattering/   # Numerical methods and figure generation
├── scripts/                  # Entry points for each stage of the study
├── results/                  # Selected PNG, GIF, and CSV outputs
├── report/                   # Technical report without personal identifiers
├── pyproject.toml
└── README.md
```

## Running the project

Python 3.10 or later is recommended.

```bash
python -m pip install -e .
quantum-scattering all --profile quick --output-dir output
```

The `quick` profile reduces grid sizes and animation frames for a short test run. Use `--profile reference` for the settings used to produce the included figures. Add `--skip-gifs` when only static outputs are needed.

Individual stages can also be run directly:

```bash
python scripts/part3.py --output-dir output
python scripts/part4.py --profile quick --skip-gifs --output-dir output
python scripts/part6.py --profile quick --output-dir output
```

## Technical notes

The stationary solver uses finite-difference propagation and boundary matching. Time evolution uses a split-operator Fourier method, while the box-basis and complex-scaling sections diagonalize matrix representations of the Hamiltonian. The report records the derivations, numerical choices, and interpretation of the results.

See [`report/quantum_scattering_report.docx`](report/quantum_scattering_report.docx) for the full discussion. Background material and a related formulation of resonance extraction are available from [arXiv:2204.03651](https://arxiv.org/abs/2204.03651).
