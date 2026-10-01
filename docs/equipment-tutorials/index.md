# Equipment Tutorials

Operating procedures for the shared instruments. These pages supplement
hands-on training from the instrument's owner; they don't replace it.

| Instrument | Owner | Tutorial |
| ---------- | ----- | -------- |
| Thermal evaporator | see [owners](../group-organization/equipment-owners.md) | [Evaporator](evaporator.md) |
| PL setup | see [owners](../group-organization/equipment-owners.md) | [PL setup](pl-setup.md) |
| XRD | see [owners](../group-organization/equipment-owners.md) | [XRD](xrd.md) |

!!! danger "Before using any instrument"
    1. Complete the required institutional safety training.
    2. Get signed off by the instrument's owner.
    3. Book the instrument and fill in the logbook every session.

## Adding a tutorial for a new instrument

1. Copy `templates/equipment-tutorial-template.md` from the repository into
   `docs/equipment-tutorials/` and rename it (e.g. `uv-vis.md`).
2. Fill it in.
3. Add it to the `nav:` section of `mkdocs.yml` under *Equipment tutorials*.
4. Add the instrument to the [equipment owners](../group-organization/equipment-owners.md)
   table.

See [How to edit](../how-to-edit.md) for the editing workflow.
