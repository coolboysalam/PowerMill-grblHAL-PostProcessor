# Changelog

All notable changes to this project will be documented in this file.

## [0.1.0-alpha] - 2026-10-08

### Added

- Initial public project structure.
- Autodesk PowerMill 2026 grblHAL post processor project.
- Published the current reference post as `postprocessor/Voron_Cascade_grblHAL.pmoptz`.
- 3-axis XYZ milling output.
- Metric units and absolute positioning.
- Incremental IJK arc-center handling.
- XY / XZ / YZ arc plane configuration.
- G0 / G1 / G2 / G3 motion output.
- Helical interpolation support.
- Feed-rate and spindle output.
- Manual tool change support.
- G54 work offset output.
- Program start and end safety states.
- English and Persian documentation.
- Representative milling NC output excerpt for review.
- `.gitattributes` rule marking `.pmoptz` files as binary.

### In progress

- G73 chip-break drilling validation.
- G83 deep-drilling validation.
- Q-word peck-depth mapping.
- Probing workflows.
- Tapping / rigid tapping validation.

### Notes

- Fanuc-specific G05 high-speed logic has been removed.
- Hard-coded G53 Z0 retract behavior has been removed from the generic post.
- The repository example is intentionally an excerpt and is not intended for direct machine execution.
