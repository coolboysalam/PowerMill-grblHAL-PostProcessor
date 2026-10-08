# Compatibility and Implementation Notes

## Target environment

This post processor is being developed for Autodesk PowerMill 2026 / Autodesk Manufacturing Post Processor Utility 2026 and grblHAL-based 3-axis CNC machines.

Initial validation hardware:

- Voron Cascade CNC
- BTT Scylla V1
- STM32H723
- grblHAL
- Metric units
- 3 linear axes
- VFD-controlled spindle

## Current command support

| Function | G/M-code | Status |
|---|---:|---|
| Rapid positioning | G0 | Tested |
| Linear interpolation | G1 | Tested |
| CW arc | G2 | Tested |
| CCW arc | G3 | Tested |
| XY plane | G17 | Configured |
| XZ plane | G18 | Configured |
| YZ plane | G19 | Configured |
| Metric units | G21 | Tested |
| Absolute distance mode | G90 | Tested |
| Incremental IJK arc centers | G91.1 | Tested |
| Feed per minute | G94 | Tested |
| Work coordinate system | G54 | Tested |
| Cutter compensation cancel | G40 | Tested |
| Tool length compensation cancel | G49 | Tested |
| Canned-cycle cancel | G80 | Tested |
| Spindle CW | M3 | Tested |
| Spindle stop | M5 | Tested |
| Manual tool change | M6 | Tested |
| Program end | M30 | Tested |
| Standard drilling | G81 | Configured / validation ongoing |
| Chip-break drilling | G73 | Work in progress |
| Deep drilling | G83 | Work in progress |
| Tapping | G84 | Not enabled |
| Rigid tapping | G84 | Not enabled |

## Arc handling

The post uses IJK arc-center output with incremental arc-center coordinates (`G91.1`).

Configured planes:

- XY → `G17`, I/J
- XZ → `G18`, I/K
- YZ → `G19`, J/K

Helical interpolation is enabled.

## Deliberately excluded / removed behavior

The post avoids controller-specific Fanuc behavior that is inappropriate for grblHAL, including Fanuc high-speed `G05` logic.

Hard-coded machine-coordinate retracts such as `G53 Z0` are intentionally not emitted by the generic post because safe machine-coordinate positions are machine-specific.

## Drilling-cycle status

`G81` is the conservative baseline cycle.

`G73` and `G83` are being validated to ensure PowerMill maps peck depth correctly to the grblHAL `Q` word.

Tapping is currently disabled until spindle synchronization and controller behavior are validated on the target machine.

## Safety note

A post processor cannot guarantee machine safety. Machine setup, homing state, work offsets, spindle/VFD configuration, safe retract positions and limit configuration remain the responsibility of the operator.
