# پست پروسسور grblHAL برای Autodesk PowerMill

[English](../README.md)

این پروژه یک Post Processor سفارشی برای **Autodesk PowerMill** است که برای دستگاه‌های CNC سه‌محوره مبتنی بر **grblHAL** توسعه داده شده است. نسخه اولیه روی **Voron Cascade CNC** با کنترلر **BTT Scylla V1 / STM32H723** ساخته و تست شده است.

> وضعیت: **نسخه پایدار / اصلی**  
> نسخه فعلی: **v1.0.0**  
> PowerMill: Autodesk PowerMill Ultimate 2026  
> Post Utility: Autodesk Manufacturing Post Processor Utility 2026  
> کنترلر: grblHAL  
> واحد: Metric

فایل اصلی نسخه فعلی پروژه:

[`postprocessor/Voron_Cascade_grblHAL.pmoptz`](../postprocessor/Voron_Cascade_grblHAL.pmoptz)

## محدوده نسخه 1.0.0

نسخه 1.0.0 اولین نسخه پایدار برای ماشین‌کاری معمول سه‌محوره با grblHAL است. قابلیت‌هایی که در بخش «در حال اعتبارسنجی / برنامه‌ریزی‌شده» آمده‌اند هنوز جزو پشتیبانی پایدار این نسخه محسوب نمی‌شوند.

### قابلیت‌های پیاده‌سازی و تست‌شده

- ماشین‌کاری سه‌محوره XYZ
- واحد متریک
- مختصات مطلق با `G90`
- مرکز قوس Incremental با `G91.1`
- صفحات قوس XY / XZ / YZ با `G17` / `G18` / `G19`
- قوس ساعتگرد و پادساعتگرد با `G2` و `G3`
- خروجی مرکز قوس به‌صورت IJK
- پشتیبانی از Helical Interpolation
- حرکت سریع `G0`
- حرکت خطی `G1`
- خروجی Feed با `F`
- سرعت و استارت ساعتگرد اسپیندل با `S` و `M3`
- توقف اسپیندل با `M5`
- تعویض دستی ابزار با `T` و `M6`
- Work Offset با `G54`
- لغو Cutter Compensation با `G40`
- لغو Tool Length Compensation با `G49`
- لغو Canned Cycle با `G80`
- Feed Per Minute با `G94`
- پایان برنامه با `M30`
- NC Comments
- Comment اطلاعات Tool و Toolpath

### در حال اعتبارسنجی / برنامه‌ریزی‌شده

- سوراخ‌کاری Chip Break با `G73`
- Deep Drilling با `G83`
- انتقال صحیح Peck Depth به پارامتر `Q`
- Probing
- Tapping / Rigid Tapping
- Safe Retract و Tool Change Position اختصاصی ماشین
- استراتژی Coolant و خروجی‌های Auxiliary

## تست انجام‌شده

یک Toolpath واقعی PowerMill با چند هزار بلوک حرکتی Post شده و شامل موارد زیر بوده است:

- `G0`
- `G1`
- `G2`
- `G3`
- مقادیر I/J برای Arc
- تغییر Feed
- Tool Change
- فرمان‌های Spindle
- Work Offset با `G54`
- Program Start / End

یک نمونه کوتاه از خروجی واقعی تولیدشده در این فایل قرار دارد:

[`examples/milling-test-excerpt.tap`](../examples/milling-test-excerpt.tap)

> این فایل فقط برای بررسی و مستندسازی است و **برای اجرای مستقیم روی دستگاه در نظر گرفته نشده است**.

## فایل‌ها

- `postprocessor/Voron_Cascade_grblHAL.pmoptz` — فایل اصلی و پایدار Post Processor
- `examples/milling-test-excerpt.tap` — بخشی از خروجی NC واقعی برای بررسی
- `docs/README_FA.md` — مستندات فارسی
- `docs/COMPATIBILITY.md` — وضعیت سازگاری و نکات فنی
- `CHANGELOG.md` — تاریخچه تغییرات

## نصب

1. فایل `postprocessor/Voron_Cascade_grblHAL.pmoptz` را دانلود کنید.
2. Autodesk Manufacturing Post Processor Utility یا PowerMill را باز کنید.
3. فایل `.pmoptz` را به‌عنوان Machine Option File برای NC Program انتخاب کنید.
4. ابتدا یک Toolpath ساده تستی Post کنید.
5. قبل از اجرا روی دستگاه، G-code تولیدشده را بررسی کنید.

## نکات ایمنی

نسخه 1.0.0 نسخه پایدار برای محدوده مستندشده ماشین‌کاری سه‌محوره است. قابلیت‌هایی که در بخش **در حال اعتبارسنجی / برنامه‌ریزی‌شده** قرار دارند تا زمان اعلام رسمی، آزمایشی در نظر گرفته می‌شوند.

قبل از هر اجرا موارد زیر را کنترل کنید:

- Work Coordinate System و Zero قطعه
- ارتفاع‌های امن Z
- دور و جهت اسپیندل
- Feed Rate
- شماره ابزار و رفتار Tool Change
- محدوده حرکتی دستگاه
- جهت و Plane قوس‌ها
- رفتار سیکل‌های سوراخ‌کاری

اولین تست را به‌صورت **Dry Run / Air Cut** و با فاصله ایمن ابزار از قطعه انجام دهید.

## سخت‌افزار اولیه توسعه

- Voron Cascade CNC
- BTT Scylla V1
- STM32H723
- grblHAL
- سه محور خطی
- تنظیمات Metric
- اسپیندل 2.2 kW با VFD

هدف این پروژه این است که Post تا حد امکان Generic برای grblHAL باقی بماند و رفتارهای اختصاصی هر ماشین جداگانه مستند شوند.

## مشارکت

گزارش باگ، نتایج تست روی دستگاه‌های دیگر grblHAL، نکات سازگاری و Pull Request برای بهبود پروژه استقبال می‌شوند.

## مجوز

این پروژه تحت [MIT License](../LICENSE) منتشر شده است.
