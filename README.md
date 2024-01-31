# 3D-Printing

Klipper Config for Creality Ender 5 Pro
Specifications:
- BTT SKR 1.4 Turbo (cpu = LPC1769)
- BL Touch
- Stepper Drivers = TMC2209
- Sensorless Homing with StallGuard
- Noise Reduction with Stealthchop

  [virtual_sdcard]
path: ~/Ender5/printer_data/gcodes

[display_status]

[fan]
pin: P2.3
max_power: 0.8			# Part Cooling Fan at 80%

[heater_fan HotEnd_cooling_fan]
pin: P2.4
heater: extruder
heater_temp: 50.0			# turns off as temp drops down to below 50c

[mcu]
serial: /dev/serial/by-id/usb-Klipper_lpc1769_07A0000DA69869AF3C41415EC42000F5-if00
restart_method: command

[exclude_object]

## Copied from print-creality_ender5pro-2020.cfg
[printer]
kinematics: cartesian
max_velocity: 300
max_accel: 3000
max_z_velocity: 5
max_z_accel: 100

[stepper_x]
step_pin: P2.2
dir_pin: !P2.6
enable_pin: !P2.1
microsteps: 16
rotation_distance: 40
endstop_pin: tmc2209_stepper_x:virtual_endstop
homing_retract_dist: 0
position_endstop: 230
position_max: 230
homing_speed: 50

[tmc2209 stepper_x]
uart_pin: P1.10
run_current: 0.800			# Marlin has 580; changed to 600, 700, 800
diag_pin: ^P1.29			# StallGuard Detect Pin (end-stop detection)
driver_SGTHRS: 100			# StallGuard Threshold (sesitivity)
#interpolate: false			# TMC2209 will not utilize internal micro-stepping of 256 (default = True)
stealthchop_threshold: 999999

[stepper_y]
step_pin: P0.19
dir_pin: !P0.20
enable_pin: !P2.8
microsteps: 16
rotation_distance: 40
endstop_pin: tmc2209_stepper_y:virtual_endstop
homing_retract_dist: 0
position_endstop: 230
position_max: 230
homing_speed: 50

[tmc2209 stepper_y]
uart_pin: P1.9
run_current: 0.800			# Marlin has 650; changed to 700, 800
diag_pin: ^P1.28			# StallGuard Detect Pin (end-stop detection)
driver_SGTHRS: 100			# StallGaurd Threshold (sensitivity)
#interpolate: false			# TMC2209 will not utilize internal micro-stepping of 256 (default = True)
stealthchop_threshold: 999999

[stepper_z]
step_pin: P0.22
dir_pin: !P2.11
enable_pin: !P0.21
microsteps: 16
rotation_distance: 4		# copied from print-creality_ender5pro-2020.cfg
endstop_pin: probe:z_virtual_endstop
position_max: 300
position_min: -5

[tmc2209 stepper_z]
uart_pin: P1.8
run_current: 0.580			# Marlin has 580; changed to
#interpolate: false			# TMC2209 will not utilize internal micro-stepping of 256 (default = True)
stealthchop_threshold: 999999

[extruder]
step_pin: P2.13
dir_pin: !P0.11
enable_pin: !P2.12
microsteps: 16
rotation_distance: 32.342	# copied from print-creality_ender5pro-2020.cfg
nozzle_diameter: 0.400
filament_diameter: 1.750
heater_pin: P2.7
sensor_type: EPCOS 100K B57560G104F
sensor_pin: P0.24
min_temp: 0
max_temp: 300

[tmc2209 extruder]
uart_pin: P1.4
run_current: 0.800			# Marlin has 600; changed to 800
#interpolate: false			# TMC2209 will not utilize internal micro-stepping of 256 (default = True)
#stealthchop_threshold: 999999

[heater_bed]
heater_pin: P2.5
sensor_type: EPCOS 100K B57560G104F
sensor_pin: P0.25
min_temp: 0
max_temp: 135

# https://www.klipper3d.org/BLTouch.html
[bltouch]
sensor_pin: ^P0.10			# White wire (on Probe)
control_pin: P2.0			# Yellow Wire (on Servos)
x_offset: -43				# values transferred from Marlin (NOZZLE_TO_PROBE_OFFSET)
y_offset: -4				# values transferred from Marlin (NOZZLE_TO_PROBE_OFFSET)
stow_on_each_sample: false
samples: 3
#z_offset: 1.155

[safe_z_home]
home_xy_position: 150, 115 # coordinates to the center of your print bed for nozzle
speed: 50
z_hop: 10    
z_hop_speed: 5

# https://www.klipper3d.org/Bed_Mesh.html
[bed_mesh]
speed: 120
horizontal_move_z: 5
mesh_min: 20, 15
mesh_max: 185, 200
mesh_pps: 2, 2
probe_count: 7, 7
algorithm: bicubic
bicubic_tension: 0.2
