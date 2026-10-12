# Changelog

All notable changes to this project will be documented in this file.

## 2026-10-12 — G73 drilling fix

### Fixed

- Output positive G73 Q peck depth using `abs(%p(Drilling Peck Depth)%)`.
- Set Q output to Always so each cycle setup includes Q after G80.
- Suppress the G73 P dwell word, resolving error:36 on the tested grblHAL controller.
- Replace the post with the operator-designated final file, uploaded as Voron_Cascade_grblHAL(3).pmoptz.

### Validation

- Complete drilling program passed grblHAL Check Mode without errors.
- Operator confirmed successful drilling on Voron Cascade.
- G83 remains under validation.

### فارسی

- اصلاح مقدار منفی Q با تابع abs و خروجی همیشگی آن در شروع هر سیکل G73، از جمله پس از G80.
- حذف پارامتر P از G73 برای رفع خطای 36 در کنترلر تست‌شده.
- بررسی کامل بدون خطا در Check Mode و تأیید اجرای موفق سوراخ‌کاری توسط اپراتور روی Voron Cascade.
- G83 همچنان در حال اعتبارسنجی است.

## [1.0.0] - 2026-10-08

### Added

- First stable public release.
- Autodesk PowerMill 2026 grblHAL post processor project.
- Published the current stable post as `postprocessor/Voron_Cascade_grblHAL.pmoptz`.
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

### Not included in the stable support scope yet

- G73 chip-break drilling validation.
- G83 deep-drilling validation.
- Q-word peck-depth mapping.
- Probing workflows.
- Tapping / rigid tapping validation.

### Notes

- Fanuc-specific G05 high-speed logic has been removed.
- Hard-coded G53 Z0 retract behavior has been removed from the generic post.
- The repository example is intentionally an excerpt and is not intended for direct machine execution.
