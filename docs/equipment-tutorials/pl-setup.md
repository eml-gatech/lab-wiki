# PL setup

!!! abstract "Page info"
    - **Components:** _laser(s), spectrometer, detector_
    - **Location:** _Room ###_
    - **Owner:** see [equipment owners](../group-organization/equipment-owners.md)
    - **Last verified:** _YYYY-MM-DD by Name_

!!! warning "Draft"
    Replace every _italic placeholder_ with the values for this setup.

## Laser safety

!!! danger "Laser eyewear"
    Wear the goggles rated for the laser in use (_wavelength, OD rating, where
    stored_). Check that the room interlock / warning light is on before
    opening the shutter.

- _Laser class(es) and wavelengths_
- Keep beam paths at table height; no reflective jewelry or watches.

## Startup

1. Turn on the _detector cooling_ and wait until it reaches _temperature_.
2. Turn on the laser and let it warm up for _N_ minutes for stable power.
3. Launch the acquisition software: _program name, computer_.

## Measurement

=== "Steady-state PL"

    1. Mount the sample: _holder, orientation_.
    2. Set excitation power with _ND filters / power setting_ and record it
       (measure with the power meter at the sample position).
    3. Set grating, center wavelength, slit width, and integration time:
       _typical values_.
    4. Take a dark/background spectrum with the shutter closed.
    5. Acquire the spectrum and save raw data: _file naming convention_.

=== "Time-resolved PL"

    1. _Pulsed source settings: repetition rate, pulse energy_
    2. _Detector / TCSPC settings_
    3. Record the instrument response function (IRF): _method_.
    4. _Acquisition and saving_

!!! tip "Record the conditions"
    Always log excitation wavelength, power density, spot size, and
    atmosphere. Perovskite PL can change under continuous illumination, so
    note exposure time and use a fresh spot when comparing samples.

## Calibration

- Wavelength calibration: _lamp, how often_
- Spectral response correction: _file location, how to apply_

## Shutdown

1. Close the shutter and turn off the laser.
2. _Detector warm-up / shutdown sequence_
3. Copy data off the instrument PC: _where_.
4. Fill in the logbook.

## Troubleshooting

??? failure "No signal"
    _Check shutter, alignment, filter in the beam path, detector cooling._

??? failure "Saturated detector"
    _Reduce integration time or excitation power; widen ND filtering._
