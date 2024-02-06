# Creality Ender 5 Pro

Klipper Config for 
- BTT SKR 1.4 Turbo (cpu = LPC1769)
- BL Touch
- Stepper Drivers = TMC2209
- Sensorless Homing with StallGuard
- Noise Reduction with Stealthchop

Normally 'printer'cfg' is the file where you would keep your entire config however I have done it slightly differently.

- 'printer.cfg' only has transient items i.e. values which are still being changed/tested
- Core config (e.g. pins, motor current etc.) file stores all the values which have been finalized and will no longer change.
A simple [include core.cfg] directive keeps 'printer.cfg' concise and readable for transient values
- kiauh_macros config is the file which has a copy of most macros from kiauh repository
