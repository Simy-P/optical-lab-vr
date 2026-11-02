# optical-lab-vr
VR Optics Lab: a WebXR optical bench for the Meta Quest (also playable on desktop).

Stages: laser safety, mirrors, lenses, alignment, **experiments**, and a free build.

## 4 · Experiments: adaptive optics
- 37-actuator deformable mirror, 50:50 beamsplitter, 15×15 Shack–Hartmann sensor (320 µm lenslets), phase plate.
- Wavefronts are tracked on a pupil grid with every element's ray-transfer (ABCD) matrix, so conjugation is real:
  a DM that isn't imaged onto the objective pupil corrects the centre of the field but not the edges, and a
  sensor far from the DM's conjugate sees a Fresnel-blurred version of it.
- The sensor uses the guide-star light returning from the sample, back through the DM; calibration pokes each
  actuator to build the interaction matrix, and the loop runs a regularised least-squares reconstructor.
- Aberrations come from the phase plate (astigmatism, coma, trefoil, spherical, random), tilted lenses, and the
  sample (index-mismatch spherical aberration plus a random screen, growing with depth in the spheroid).
- The residual wavefront sets the image through real PSFs (FFT of the pupil, computed in a Web Worker): confocal =
  excitation × pinhole-filtered detection, a 15×15-pixel kernel at 3×3 field points blended across the image, plus a
  17-plane through-focus stack (beads are drawn with the PSF at their own defocus; sectioning follows the axial response).
