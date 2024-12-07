# USB Debug Mode

Instead of using serial pads we may be able to access a debug terminal using ADB (Android Debug Terminal).

Modify device tree parameter

`dr_mode = "host";`

to

`dr_mode = "peripheral";`

or maybe 

`dr_mode = "otg";`
