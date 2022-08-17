# Klicky-Probe-macros
This project exists to automatically sync the `Klipper_macros` folder of the [Klicky-Probe](https://github.com/jlas1/Klicky-Probe) project to a git repository so that it can be auto-updated by Moonraker.

Synchronization is achieved through a GitHub [action](https://github.com/AdamYellen/Klicky-Probe-macros/blob/main/.github/workflows/sync-push.yml) that runs on a schedule. It compares the current hash of the upstream project with a file (`.last_sync_id`) and will proceed only if it has changed. This is done to avoid more expensive operations. Currently the script doesn't try to detect changes on the macro files, so any change to the upstream repo will trigger a new release. The script uses a date-based versioning scheme because the upstream project doesn't have versioned releases. This script must run on a schedule because GitHub actions don't support push/merge event triggers on other repos.

The instructions below illustrate how the user can install this repo on their printer in a way that avoids local changes and so Moonraker can automatically update the macros when they change.

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

# Klicky Probe variable override
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
