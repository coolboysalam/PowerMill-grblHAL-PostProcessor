# PowerMill grblHAL Post Processor v1.0.0

First stable release of the Autodesk PowerMill post processor for grblHAL-based 3-axis CNC machines.

## Highlights

- 3-axis XYZ milling support
- Metric output (`G21`)
- Absolute positioning (`G90`)
- Incremental IJK arc centers (`G91.1`)
- XY / XZ / YZ arc planes (`G17`, `G18`, `G19`)
- Linear and circular interpolation (`G0`, `G1`, `G2`, `G3`)
- Helical interpolation support
- Feed-rate output
- Spindle speed, start and stop output
- Manual tool-change output (`T` / `M6`)
- G54 work coordinate system output
- Safe modal cancellation for cutter compensation, tool-length compensation and canned cycles
- Program end with `M30`
- English and Persian documentation
- Representative PowerMill-generated NC example

## Main post file

`postprocessor/Voron_Cascade_grblHAL.pmoptz`

Initial development and validation hardware:

- Voron Cascade CNC
- BTT Scylla V1
- STM32H723
- grblHAL
- 3 linear axes
- 2.2 kW VFD-controlled spindle

## Not included in the stable support set yet

The following features are intentionally not claimed as stable in v1.0.0:

- G73 chip-break drilling
- G83 deep drilling
- PowerMill peck-depth to `Q` mapping
- Probing workflows
- Tapping / rigid tapping
- Machine-specific safe retract positions

## Safety

Always inspect generated G-code before running it on a machine. Verify work offsets, safe Z heights, spindle commands, feed rates, tool-change behavior and machine limits. Perform the first test as a dry run / air cut.

## License

MIT License
