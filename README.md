# Klicky-Probe-macros
Sync the Klipper_macros folder of Klicky-Probe

## Install
```
cd ~/klipper_config
git clone https://github.com/AdamYellen/Klicky-Probe-macros.git klicky-probe
```

## Configure Klipper
```
[include klicky-probe/klicky-variables.cfg]
[include klicky-probe/klicky-macros.cfg]
[include klicky-probe/klicky-bed-mesh-calibrate.cfg]
#[include klicky-probe/klicky-screws-tilt-calculate.cfg]
#[include klicky-probe/klicky-quad-gantry-level.cfg]
[include klicky-probe/klicky-z-tilt-adjust.cfg]

# Klick Probe variable override
[gcode_macro _User_Variables]
variable_max_bed_y:           250
variable_max_bed_x:           250
...
Variable_attachmove_x:        0
Variable_attachmove_y:        30
```
NOTE: Don't modify any files in klicky-probe. Set printer-specific variables in printer.cfg after the includes.

## Configure Moonraker for updates
```
[update_manager klicky_probe]
type: git_repo
path: ~/klipper_config/klicky-probe
origin: https://github.com/AdamYellen/Klicky-Probe-macros.git
primary_branch: main
managed_services: klipper
```
