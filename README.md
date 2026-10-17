# Photonic bond-health sensing in SiC power modules: raw simulation data

Raw simulation outputs used in the article *Differential Calibration Drift Limits Photonic Bond-Health Sensing in SiC Power Modules: A Detectability Law and Ratiometric Two-Heater Self-Calibration*. All files are plain CSV with a header row and are unedited solver exports.

## Contents

| Folder | Model | Files |
|---|---|---|
| `converter_profiles/` | Electrothermal model of one switch of a 1200 V, 450 A SiC half-bridge (800 V, 20 kHz, 40 °C ambient) | `sim_<profile>.csv` |
| `waveguide_optics/` | Mode solutions of the 220 nm silicon strip waveguide vs. width, temperature and strain | `b1*.csv`, `b2v2_sweep.csv` |
| `package_thermomechanics/` | Static quarter model of chip, bond and baseplate under a 100 K rise | `a1*.csv` |
| `package_transients/` | Transient package model driven by the converter case temperature | `a3_<profile>_<bond>.csv` |
| `heater/` | Axisymmetric micro-heater frequency response and heater-induced strain | `heater_*.csv` |

### Converter profiles (`sim_<profile>.csv`)

Columns: `t_s` time (s), `I_A` phase current (A), `Phs_W` loss of the switching device (W), `Ptot_W` total half-bridge loss (W), `Tj_C`, `Tcase_C`, `Ths_C` junction, case and heat-sink temperature (°C). Sampling 0.05 s, after 1800 s of preconditioning.

| Profile | Current (A) |
|---|---|
| A | constant 120 |
| B / C | step 40 → 200 / 200 → 40 at 600 s |
| D, E10, E40, E160 | square wave 40/200, period 60, 10, 40, 160 s |
| F1 | ramp 40 → 200 over 600 s |
| F2 | step 40 → 200 with 60 s overshoot to 260 |
| G | start-stop, 0/200, 20 min on, 20 min off |

### Waveguide optics

- `b1b2_sweep.csv`, `b2v2_sweep.csv`: `w_um` core width (µm), `case` (`T` temperature, `lam` wavelength, `unix`/`uniz`/`biax` strain, `base` unstrained), `TC` (°C), `lam_um` (µm), `ex`, `ez` applied lateral and longitudinal strain, `neff`, `TEfrac` TE fraction, `Gcore` core confinement. `b1b2` is the isotropic model. `b2v2` is the anisotropic model with deformed core and adds `pset` (photoelastic set 1 or 2).
- `b1_mesh_convergence.csv`: mesh study (`neff` at 25 and 75 °C, d*n*/d*T*).

### Package thermomechanics (`a1*.csv`)

Columns: `label` sweep name, `tc_um` chip thickness, `tb_um` bond thickness, `Eb_GPa` bond modulus, `adel_um` edge delamination, `dt_um` trench depth, `Ri_um` island radius, `hfine_um` mesh size at rings, `nelem` elements, `eA_tt`, `eA_rr`, `eB_tt`, `eB_rr` hoop and radial strain at rings A and B, `dT` temperature rise (K).

### Package transients (`a3_*.csv`)

Columns: `t_s` (s), `Tbase_C`, `TA_C`, `TB_C` baseplate and ring temperatures (°C), `eA_tt`, `eA_rr`, `eB_tt`, `eB_rr` ring strains. Bond states: `healthy`, `Eb1` (bond modulus 1 GPa), `delam150` (150 µm edge delamination).

### Heater (`heater_*.csv`)

- `heater_<ring>_<state>.csv`: `f_Hz` frequency, `T_re`, `T_im` complex ring temperature per milliwatt (K mW⁻¹), `nelem` elements. `h05` is the coarser mesh check; `fig_30k` is the case plotted at 30 kHz.
- `*_strain.csv`: `Tdc_K` DC temperature rise, `e_tt_mech`, `e_rr_mech` heater-induced mechanical strain at the ring.

## Notes

- One row in `a1a2_sweep.csv` and one in `a1_mesh_convergence2.csv` are failed solver runs. They hold a multi-line error message in place of values and are skipped in the analysis.
- Material constants and model parameters are listed in Table 3 of the article.

## License

[CC BY 4.0](LICENSE). Please cite the article when using these data.
