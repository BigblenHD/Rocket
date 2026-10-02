# Integrated flight software

Start with [TVC-Flight-Code.ino](TVC-Flight-Code.ino). The sketch delegates flight sequencing to a state machine and hardware/control behaviour to the `Rocket` class.

## Source map

| File | Responsibility |
| --- | --- |
| `TVC-Flight-Code.ino` | Arduino entry point; requests one state-machine iteration every 10 ms |
| `StateMachine.h/.cpp` | Flight states and transition checks |
| `Rocket.h/.cpp` | Hardware constants, sensor acquisition, Madgwick filtering, state-feedback control and servo outputs |
| `SDCard.h/.cpp` | Buffered CSV logging and event files with incrementing names |
| `HealthMonitor.h/.cpp` | Sensor health bookkeeping and event reporting |
| `LED.h/.cpp`, `Buzzer.h/.cpp` | Status indication |

## Behaviour in the source

- The idle state reads acceleration and checks a threshold for liftoff.
- During ascent, IMU measurements feed the attitude filter and state-feedback controller.
- A stored thrust curve converts torque demand into gimbal angle; fitted mappings convert gimbal demand to servo commands.
- During ascent, the slower barometer/logging block runs every fourth iteration: nominally 25 Hz if the requested 100 Hz loop is achieved.
- Apogee and landing checks use elapsed-time thresholds defined in `StateMachine.h`, rather than measured altitude extrema or ground detection.
- The descent state continues logging; the landed state closes logs and enables an audible indication.

Axis labels and signs follow this build's IMU mounting and mechanical calibration. They should not be treated as a universal rocket coordinate convention.

## Build requirements

Use an Arduino environment with Teensy 4.1 support and the libraries referenced by the source: Adafruit BNO055, Adafruit BMP3XX, MadgwickAHRS and their dependencies, plus Servo, SD and Wire.

Keep all files in this folder together. Open `TVC-Flight-Code.ino` and select the intended board. The SD implementation uses `BUILTIN_SDCARD`, tying the current configuration to a board with that interface.

The Madgwick code calls `setInitialRollPitch()`. Verify that the selected library exposes this method; the project does not record the exact compatible revision. Dependency versions are not pinned and no automated build is supplied. This guide describes the source; it does not report a verified compilation.

## Configuration

Review `Rocket.h` for servo pins, centre positions, sensor conventions, geometry and controller gains. Review `StateMachine.h` for acceleration and timing thresholds. The filter frequency and source loop interval describe intended scheduling, not measured timing.

## Logs

The logger creates incrementing data/event filenames, such as `DATA0001.CSV` and `EVENT0001.TXT`. Data fields include time, acceleration, angular rates, attitude, temperature, pressure, altitude, servo commands and estimated thrust. Event records include transitions and health reports.
