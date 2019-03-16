This is a RangeFinder sensor array for ArduPilot with up to 9 VL53L0X/VL53L1X sensors.

# Usage
0. [Only as long as the pull request is not merged into master] Build your ArduPilot with the code from the PR [#10739](https://github.com/ArduPilot/ardupilot/pull/10739)
1. Connect the sensor array via I2C to the board running ArduPilot.
2. Adjust the parameters in ArduPilot as follows (the `x` in parameter names stands for _all_ sensors 1-9):

Parameter        | Value
-----------------|------
`RNGFNDx_TYPE`   | 23*
`RNGFND1_ADDR`   | 41
`RNGFND1_PIN`    | -1
`RNGFND1_ORIENT` | 25
`RNGFND2_ADDR`   | 33
`RNGFND2_PIN`    | 7
`RNGFND2_ORIENT` | 0
`RNGFND3_ADDR`   | 34
`RNGFND3_PIN`    | 0
`RNGFND3_ORIENT` | 1
`RNGFND4_ADDR`   | 35
`RNGFND4_PIN`    | 1
`RNGFND4_ORIENT` | 2
`RNGFND5_ADDR`   | 36
`RNGFND5_PIN`    | 2
`RNGFND5_ORIENT` | 3
`RNGFND6_ADDR`   | 37
`RNGFND6_PIN`    | 3
`RNGFND6_ORIENT` | 4
`RNGFND7_ADDR`   | 38
`RNGFND7_PIN`    | 4
`RNGFND7_ORIENT` | 5
`RNGFND8_ADDR`   | 39
`RNGFND8_PIN`    | 5
`RNGFND8_ORIENT` | 6
`RNGFND9_ADDR`   | 40
`RNGFND9_PIN`    | 6
`RNGFND9_ORIENT` | 7

*Subject to change until the PR [#10739](https://github.com/ArduPilot/ardupilot/pull/10739) is merged into master.

3. Restart ArduPilot

# Explanation of parameters
- Setting `RNGFNDx_TYPE` to 23 enables address auto-configuration for this sensor array at ArduPilot startup. If you already configured the sensors manually before starting ArduPilot, you can also select `RNGFNDx_TYPE` 16, so that the sensors are treated as separate entities rather than a part of an array.
- Because of the auto-configuration you can actually set `RNGFNDx_ADDR` to whatever address you want. Exceptions are:
   - `42`. This address is used to temporarily move sensors to during the auto-configuration.
   - `32`. This address is used by the IO expander on the sensor array. The IO expander is responsible for turning individual sensors on and off.
- There is one sensor that is always on, and cannot be disabled by the IO expander. If auto-configuration (`_TYPE 23`) is enabled for that sensor, it must have `_ORIENT` set to 24 or 25 (up or down respectively) and `_PIN` set to -1.
- The `_PIN` parameters are used together with `_ORIENT` to configure what sensors are pointing in which direction, where `_PIN` determines the pin of the IO expander that the sensor is connected to, and `_ORIENT` determines how ArduPilot interprets this direction. The above table corresponds to the correct arrangement if the main sensor is facing down, the sensor that the arrow points to (drawn on the board) shows forward, and all other sensors go straight out in their respecrive directions. If you physically arrange the sensors differently, these 2 parameters would have to be adjusted accordingly.
- The independent configuration of `_PIN` and `_ORIENT` also means that you can have multiple sensors (say sensors on pins 1, 2, 3, 4) pointing in the same direction (for example all four forward, i.e. 0) should you want to go with such a configuration.
- If `_PIN` is not configured (i.e. left at the default -1), the auto-configuration will assume the default arrangement (middle sensor pointing down, the one with arrow forward) and use `_ORIENT` to determine the correct pins (the ones you see in the table above).

# Preparing for installation.
Video

https://youtu.be/QsDIQ4lPHv0

https://youtu.be/lDLPVkdIu3o

https://youtu.be/dYpx_mXiDM4

https://youtu.be/QuRKrF_noZo
