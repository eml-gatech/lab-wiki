# XRD

!!! abstract "Page info"
    - **Model:** _manufacturer / model_
    - **Source:** _e.g. Cu Kα, λ = 1.5406 Å_
    - **Location:** _Room ###_
    - **Owner:** see [equipment owners](../group-organization/equipment-owners.md)
    - **Last verified:** _YYYY-MM-DD by Name_

!!! warning "Draft"
    Replace every _italic placeholder_ with the values for this instrument.

## Radiation safety

!!! danger "X-ray hazard"
    Never defeat or bypass the door interlocks. _Dosimeter / badge
    requirements and institutional training required before use._

## Background

Peak positions follow Bragg's law:

$$
n\lambda = 2d\sin\theta
$$

where $d$ is the lattice-plane spacing and $2\theta$ is the angle between the
incident and diffracted beams.

## Startup

1. _Generator / cooling water startup sequence_
2. Ramp the tube to operating power: _kV / mA_, using the software ramp, not
   a single step.
3. Launch the control software: _program name_.

## Sample preparation

- Powders: _zero-background holder; how to pack and level_
- Thin films: _mounting method; height alignment procedure_
- Air-sensitive samples: _dome/airtight holder, Kapton window, or glovebox
  loading procedure_

## Measurement

=== "θ–2θ (Bragg–Brentano)"

    1. Select optics: _slits, filters, detector mode_.
    2. Align sample height: _procedure_.
    3. Set scan range, step size, and time per step: _typical values_.
    4. Run the scan and save as _format / naming convention_.

=== "Grazing incidence (GIXRD)"

    1. _Optics configuration for parallel-beam geometry_
    2. _Sample alignment: height and tilt_
    3. Set the incidence angle ω: _typical range_.
    4. _Scan settings and saving_

## Shutdown

1. Ramp the tube down to standby: _kV / mA_.
2. Remove your sample and clean the holder.
3. Copy data off the instrument PC: _where_.
4. Fill in the logbook.

## Data analysis

- Phase identification: _software / database the group uses_
- _Link to group analysis scripts, if any_

## Troubleshooting

??? failure "Door won't unlock after a scan"
    _Shutter status, software state, who to contact._

??? failure "Peaks shifted from reference positions"
    _Check sample height displacement first, then the zero-offset
    calibration against the reference standard (name the standard here)._
