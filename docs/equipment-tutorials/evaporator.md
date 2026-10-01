# Thermal evaporator

!!! abstract "Page info"
    - **Model:** _manufacturer / model_
    - **Location:** _Room ###_
    - **Owner:** see [equipment owners](../group-organization/equipment-owners.md)
    - **Last verified:** _YYYY-MM-DD by Name_

!!! warning "Draft"
    The steps below are a generic outline. The owner should replace every
    _italic placeholder_ with the values and settings for this instrument.

## Safety

- _Hazards: high voltage/current to the source, hot boats and chamber parts
  after a run, vacuum implosion risk on viewports, toxic source materials
  (list any)_
- _Required PPE_
- Never vent the chamber while sources are still hot.

## Before you start

- [ ] Instrument booked and logbook entry started
- [ ] Substrates cleaned and loaded in the holder
- [ ] Shadow mask selected: _mask ID / pattern_
- [ ] Source material and boat type confirmed: _e.g. Au in W boat_

## Loading and pump-down

1. Vent the chamber: _procedure / valve sequence_.
2. Load the source into the boat; check the boat for cracks or thinning.
3. Mount the substrate holder and mask; check that the shutter moves freely.
4. Close the chamber and start the pump-down: _procedure_.
5. Wait for base pressure: _target, e.g. < X × 10⁻⁶ mbar_ (typically
   _N_ minutes).

## Deposition

1. On the thickness monitor, select the material program and confirm
   density, Z-ratio, and tooling factor: _where these are stored_.
2. Ramp the source current slowly: _ramp profile_.
3. Once the rate is stable at _X Å/s_, zero the thickness and open the
   shutter.
4. Close the shutter at the target thickness.
5. Ramp the current down to zero.

| Material | Boat | Typical rate | Tooling factor | Notes |
| -------- | ---- | ------------ | -------------- | ----- |
| _Au_ | _W_ | _X Å/s_ | _X %_ | |
| _Ag_ | _W/Mo_ | _X Å/s_ | _X %_ | |
| _MoOₓ_ | _Mo_ | _X Å/s_ | _X %_ | |

## Unloading and shutdown

1. Let the sources cool for _N_ minutes.
2. Vent, unload samples, close the chamber, and pump back down to leave the
   system under vacuum.
3. Finish the logbook entry (base pressure, rates, thickness, any issues).

## Troubleshooting

??? failure "Rate is unstable or won't rise"
    _Possible causes: boat contact, depleted source, crystal near end of life._

??? failure "Base pressure won't come down"
    _Possible causes: O-ring debris, open valve, leak; who to contact._

## Consumables

- Thickness monitor crystals: _part number, where stored_
- Boats: _part numbers, where stored_
