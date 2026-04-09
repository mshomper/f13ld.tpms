# tpms-builder

**A browser-based tool for designing, visualizing, and analyzing custom Triply Periodic Minimal Surfaces (TPMS).**

No installation. No dependencies. Open it and go.

<img width="891" height="974" alt="tpms_builder_v0 5" src="https://github.com/user-attachments/assets/3f103580-150d-4797-8e62-88e2e14817fb" />

🔗 **[Launch the tool](https://mshomper.github.io/tpms-builder)**

---

## What it does

TPMS Builder lets you interactively construct implicit TPMS surfaces from trigonometric terms, visualize them in real-time 3D, and run a homogenization analysis to estimate their effective elastic properties.

The surface equation takes the general form:

```
F(x, y, z) = Σ cᵢ · f₁(x,y,z) · f₂(x,y,z) · ... = 0
```

where each factor is a sine or cosine function with independently adjustable spatial frequencies.

---

## Features

### 3D Viewer
- Real-time WebGL ray-marching renderer
- Iridescent surface shading (color encodes surface normal direction)
- Drag to rotate, scroll to zoom, trackball-style interaction
- XYZ orientation gizmo

### Surface Controls
- **Solid mode** — renders the solid region where F(x,y,z) > offset
- **Thin-wall mode** — renders a shell of specified thickness: |F - offset| < t
- **Cell scale** — adjust the number of unit cells in the viewport (0.5× to 3×)
- **Offset** — shift the isosurface to tune volume fraction
- **Wall thickness** — controls shell wall thickness in thin-wall mode

### Equation Editor
- Add and remove terms freely
- Each term has a scalar coefficient and one or more trig factors
- Each factor supports: `sin(x)`, `cos(x)`, `sin(y)`, `cos(y)`, `sin(z)`, `cos(z)`
- Per-factor spatial frequency control in x, y, z independently
- Toggle individual terms on/off without deleting them
- Live equation display updates as you edit

### Built-in Presets
| Name | Equation |
|------|----------|
| Gyroid | sin(x)cos(y) + sin(y)cos(z) + sin(z)cos(x) = 0 |
| Schwarz P | cos(x) + cos(y) + cos(z) = 0 |
| Schwarz D | sin(x)sin(y) − sin(x)cos(z) + cos(x)sin(z) − cos(y)cos(z) = 0 |
| Neovius | 3(cos(x)+cos(y)+cos(z)) + 4cos(x)cos(y)cos(z) = 0 |
| I-WP | 2(cos(x)cos(y)+cos(y)cos(z)+cos(z)cos(x)) − (cos(2x)+cos(2y)+cos(2z)) = 0 |

### Homogenization Analysis
Estimates effective elastic properties using a voxel-based MIL (Mean Intercept Length) fabric tensor method (Harrigan & Mann, 1984).

**Inputs:**
- Grid resolution: 32³, 48³, or 64³
- Solid-phase Young's modulus E_s (GPa)
- Solid-phase Poisson's ratio ν
- Power-law exponent n

**Outputs:**
- Volume fraction ρ
- Directional moduli E_x, E_y, E_z (GPa)
- Shear modulus G_xy (GPa)
- Effective Poisson's ratio ν_eff
- Anisotropy index E_max / E_min
- Bar chart of directional stiffness
- Stiffness ellipsoid projections (xy, xz, yz planes)

The constitutive model used is:

```
Eᵢ = Eₛ · ρⁿ · 3Hᵢ / ΣHⱼ
```

where Hᵢ are the MIL fabric tensor eigenvalues.

---

## Usage

Open [https://mshomper.github.io/tpms-builder](https://mshomper.github.io/tpms-builder) in any modern browser with WebGL support (Chrome, Firefox, Edge, Safari).

No login, no install, no data sent anywhere — everything runs locally in your browser.

---

## Technical details

- Pure HTML/CSS/JavaScript — single file, zero dependencies
- 3D renderer: WebGL 1.0 ray-marching with dynamic GLSL shader compilation
- Homogenization: runs in the browser via JavaScript on a voxelized domain
- Shader is recompiled live as you edit the equation

---

## Roadmap

- [ ] STL mesh export
- [ ] Graded / functionally-graded TPMS (spatially varying offset)
- [ ] Multi-surface boolean operations
- [ ] CSV export of homogenization results
- [ ] Additional presets (FRD, Split-P, Lidinoid)

---

## References

Harrigan, T.P. & Mann, R.W. (1984). Characterization of microstructural anisotropy in orthotropic materials using a second rank tensor. *Journal of Materials Science*, 19, 761–767.

Schoen, A.H. (1970). *Infinite periodic minimal surfaces without self-intersections*. NASA Technical Note TN D-5541.

---

## License

MIT — see [LICENSE](LICENSE)
