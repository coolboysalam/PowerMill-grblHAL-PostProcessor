# PowerMill grblHAL Post Processor

[فارسی](docs/README_FA.md)

A custom Autodesk PowerMill post processor for **grblHAL-based 3-axis CNC machines**, initially developed and tested for the **Voron Cascade CNC** using a **BTT Scylla V1 / STM32H723** controller.

> Status: **Alpha / active development**  
> Initial version: **v0.1.0-alpha**  
> PowerMill: Autodesk PowerMill Ultimate 2026  
> Post Utility: Autodesk Manufacturing Post Processor Utility 2026  
> Controller: grblHAL  
> Units: Metric

## Current scope

The current post is focused on conventional 3-axis milling and safe, readable grblHAL output.

### Implemented and tested

- 3-axis XYZ milling
- Metric units
- Absolute positioning (`G90`)
- Incremental IJK arc centers (`G91.1`)
- XY, XZ and YZ arc-plane definitions (`G17`, `G18`, `G19`)
- Clockwise / counter-clockwise arcs (`G2`, `G3`)
- IJK arc-center output
- Helical interpolation support
- Rapid moves (`G0`)
- Linear interpolation (`G1`)
- Feed-rate output (`F`)
- Spindle speed and clockwise spindle start (`S`, `M3`)
- Spindle stop (`M5`)
- Manual tool change (`T`, `M6`)
- Work coordinate system output (`G54`)
- Cutter compensation cancel (`G40`)
- Tool length compensation cancel (`G49`)
- Canned-cycle cancel (`G80`)
- Feed-per-minute mode (`G94`)
- Program end (`M30`)
- NC comments
- Tool and toolpath information comments

### Under validation / development

- `G73` chip-break drilling
- `G83` deep drilling
- Correct `Q` peck-depth mapping from PowerMill
- Probing workflows
- Tapping / rigid tapping
- Machine-specific safe retract and tool-change positioning
- Coolant / auxiliary output strategies

## Tested output

A real PowerMill milling toolpath has been post-processed successfully with several thousand motion blocks including:

- `G0`
- `G1`
- `G2`
- `G3`
- I/J arc-center values
- Feed changes
- Tool change
- Spindle commands
- G54 work offset
- Program start / end sequences

An example output is provided in [`examples/milling-test.tap`](examples/milling-test.tap).

## Files

- `postprocessor/Voron_Cascade_grblHAL.pmoptz` — PowerMill option file
- `examples/milling-test.tap` — example generated NC program
- `docs/README_FA.md` — Persian documentation
- `docs/COMPATIBILITY.md` — compatibility and implementation notes
- `CHANGELOG.md` — project changes

## Installation

1. Download `postprocessor/Voron_Cascade_grblHAL.pmoptz`.
2. Open Autodesk Manufacturing Post Processor Utility / PowerMill.
3. Add or select the `.pmoptz` file as the Machine Option File for the NC Program.
4. Post-process a simple test toolpath first.
5. Inspect the generated G-code before running it on the machine.

## Safety

This post processor is under active development.

Always verify:

- work coordinate system and zero position
- safe Z heights
- spindle speed and direction
- feed rates
- tool number and tool change behavior
- machine limits
- arc direction and plane
- drilling-cycle behavior

Run the first test as a **dry run / air cut** with the tool safely clear of the workpiece.

## Development hardware

The initial development and testing setup uses:

- Voron Cascade CNC
- BTT Scylla V1 controller
- STM32H723 MCU
- grblHAL
- 3 linear axes
- Metric configuration
- 2.2 kW VFD-controlled spindle

The project aims to keep the post as generic to grblHAL as practical while documenting machine-specific behavior separately.

## Contributions

Bug reports, test results from other grblHAL machines, compatibility notes and pull requests are welcome.

## License

Released under the [MIT License](LICENSE).
