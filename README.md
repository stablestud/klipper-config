# Klipper Config
Home of personal configuration files of my 3D printer

## Prusa Slicer Settings
This section will contain required settings to be set in Prusa Slicer so it works with the 3D printer

### Printers

#### General

##### Size and coordinates
* Size
** x: 295
** y: 295
* Origin
** x: 0
** y: -10
* Texture and Model: https://www.thingiverse.com/thing:5167737

##### Firmware
* G-code flavor: `Klipper`
* G-code thumbnails: `32x32/PNG, 400x300/PNG`

#### Custom G-code

##### Start G-code
```
SET_PRINT_STATS_INFO TOTAL_LAYER=[total_layer_count]
_GCODE_START BED_TEMP=[first_layer_bed_temperature] EXTRUDER_TEMP={first_layer_temperature[initial_tool]} CHAMBER_TEMP=[chamber_temperature]
```

##### Start G-code options
* Emit temperature commands automatically: `[ ]` (unselect)

##### End G-code
```
; total layers count = [total_layer_count]
_GCODE_END
```

##### Before layer change G-code
```
TIMELAPSE_TAKE_FRAME
```

##### After layer change G-code
```
SET_PRINT_STATS_INFO CURRENT_LAYER={layer_num + 1}
```

#### Extruder 1

##### Size
* High flow nozzle: `[x]` (select)

##### Layer height limits
* Min: `0`

##### Retraction
* Retraction length: `0.5`

### Print Settings

#### Output options

##### Output file
* Label object: `Firmware-specific`
* Output filename format: `[input_filename_base]_[print_time]_{temperature[0]}C_{nozzle_diameter[0]}mm_{filament_type[0]}_{digits(layer_height,1,2)}mm.gcode`
