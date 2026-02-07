# Klipper Config
Home of personal configuration files of my 3D printer

## Printer

### Machine limits
* Velocity XY: `370`
* Acceleration XY: `6000`
* Velocity Z: `40`
* Acceleration Z: `600`

These limits were determined using the `AUTO_SPEED` macros from [klipper_auto_speed](https://github.com/Anonoei/klipper_auto_speed)

### Printable bed size and coordinates
* Size
  * x: 295
  * y: 295
* Origin
  * x: 0
  * y: -10
* Texture and Model: https://www.thingiverse.com/thing:5167737

### Installed Components

* Titan Aero (TH3D Studio's Tough Ultimate Hotend Package)
* EZABL Pro 18mm
* 5015 Blower Part Cooling Fan (HoneyBadger, 9200RPM, 4-Wire, 24V, max 95C, 7.1CFM, 57.4mmH20)
* 750W Heated Bed (310x310mm, 220V)
* 70W V6 Hotend Heating Cartridge (max 500C, 24V)
* 200W iHeater Chamber Heater (220V)
* PT1000 Hotend Sensor (max 450Cm, 3-Wire)
* TMC2209 Stepper Drivers
* BTT Octopus Pro v1.1 H723
* Raspberry Pi 3B+
* 2x Relay (max 10A, 5VDC control, 250VAC/30VDC relay)
* NF-A4X20 Heatbreak Fan (Noctua, 5000RPM, 4-Wire, 12V)

## Slicer Configuration
This section will contain required settings to be set in Prusa Slicer so it works with the 3D printer

### Firmware
* G-code flavor: `Klipper`
* G-code thumbnails: `32x32/PNG, 400x300/PNG`

### Start G-code
Make sure the slicer does not emit temperatures setting G-Codes itself
```
SET_PRINT_STATS_INFO TOTAL_LAYER=[total_layer_count]
PRINT_START BED_TEMP=[first_layer_bed_temperature] EXTRUDER_TEMP={first_layer_temperature[initial_tool]} CHAMBER_TEMP=[chamber_temperature] MESH_MIN={first_layer_print_min[0]},{first_layer_print_min[1]} MESH_MAX={first_layer_print_max[0]},{first_layer_print_max[1]} NOZZLE_DIAMETER={nozzle_diameter[0]}
```

### End G-code
```
; total layers count = [total_layer_count]
PRINT_END
```

### Before layer change G-code
```
TIMELAPSE_TAKE_FRAME
```

### After layer change G-code
```
SET_PRINT_STATS_INFO CURRENT_LAYER={layer_num + 1}
```

### Output options
* Label objects: `Firmware-specific`/`Enable`
* Exclue objects: `Enable`
* Output filename format:
```
[input_filename_base]_[print_time]_{temperature[0]}C_{nozzle_diameter[0]}mm_{filament_type[0]}_{digits(layer_height,1,2)}mm.gcode
```

## Calibration

Good calibration guide can be found [here](https://ellis3dp.com/Print-Tuning-Guide/)    
Axis rotation_distance calibration can be done with the `AXIS_CALIBRATE` macro
