# PX4 Autopilot Firmware for FSR@TUDa

Base Version: **v1.17.0**

This fork adds airframes and board configurations required for operating the UAS fleet of FSR@TUDa.

## Additional Board Configuration

### `boards/px4/fmu-v5x`

- [fsr.px4board](boards/px4/fmu-v5x/fsr.px4board)

  Default board config for FSR.
  
### `boards/cubepilot/cubeorangeplus`

- [crsf.px4board](boards/cubepilot/cubeorangeplus/crsf.px4board)

  Crsf board config.

### `boards/cubepilot/cubeorangeplus`

- [crsf.px4board](boards/cubepilot/cubeorangeplus/crsf.px4board)

  Crsf board config.

## Additional Airframes

### `ROMFS/px4fmu_common/init.d/airframes`

- [4002_tuda_fsr_edufly](ROMFS/px4fmu_common/init.d/airframes/4002_tuda_fsr_edufly)
- [4003_tuda_fsr_scidom](ROMFS/px4fmu_common/init.d/airframes/4003_tuda_fsr_scidom)
- [13001_tuda_fsr_scidragon](ROMFS/px4fmu_common/init.d/airframes/13001_tuda_fsr_scidragon)

### `ROMFS/px4fmu_common/init.d-posix/airframes` (Simulation)

## Code Changes

**`rtl_direct_mission_land.cpp`**
Temporarily disables the transition-to-fixed-wing block to prevent a state
transition attempt with uninitialized mission data.

**`rtl.cpp` — `setRtlTypeAndDestination()`**
Adds a vehicle state check before the RTL type is assigned. If the airframe
is a VTOL and the current vehicle state is rotary-wing (MC), the RTL type is
overridden from `RTL_DIRECT_MISSION_LAND` to `RTL_DIRECT`, sending the vehicle
directly to home position. This only applies, if  `RTL_TYPE!=0`
