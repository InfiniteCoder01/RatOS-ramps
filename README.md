## Installation
ssh into your raspberry pi (or whatever you are using to run RatOS). Default user is `pi`, default password is `raspberry` (I would suggest changing that).
Then, go to RatOS boards configs directory: `cd ~/printer_data/config/RatOS/boards/`
Clone the config: `git clone https://github.com/InfinteCoder01/RatOS-ramps ramps`
After that, you can refresh RatOS configurator page and select `RepRap RAMPS` as a board. Proceed as usual.
When you get to Mainsail screen, you will need to configure the printer.
First of all, copy `RatOS/templates/custom-printer.template.cfg` into printer.cfg.
Then, replace the board by commenting out `[include RatOS/boards/btt-octopus-11/config.cfg]` and adding
`[include RatOS/boards/ramps/config.cfg]` in the `CONTROL BOARD` section.
Fill up the rest of the config for your printer.
You'll probably need to add something like this (change for your printer) to the end of `PRINTER CONFIGURATION` section:
```config
[printer]
kinematics: cartesian
max_velocity: 300
max_accel: 3000

[stepper_x]
rotation_distance: 32
position_endstop: -30
position_max: 220
position_min: -30
homing_speed: 50

[stepper_y]
rotation_distance: 32
position_endstop: -8
position_min: -8
position_max: 220
homing_speed: 50

[stepper_z]
rotation_distance: 8
position_endstop: 0.5
position_max: 240
```

And this to `[heater_bed]` part:
```config
heater_pin: et_heater_bed_heating_pin
sensor_type: EPCOS 100K B57560G104F
sensor_pin: heater_bed_sensor_pin
min_temp: 0
max_temp: 130
```

And `[include RatOS/printers/base.cfg]` to `BASE SETUP` section

You might also want to change those settings:
- `HOMING` section, select a probe or leave everything commented out if you don't have one
- `TOOLHEAD` section, select the extruder and the hotend
- `TOOLBOARD` section if you have a toolboard
- `MACRO CONFIGURATION` section, set `variable_macro_travel_speed` to something reasonable for your printer
- `PRINTER CONFIGURATION` section, comment out probe part if you don't have a probe
