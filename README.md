# Model Rocket - Thrust Vector Control

An experimental model-rocket project combining embedded flight software, attitude estimation, servo-driven thrust vector control, CAD and MATLAB/Simulink modelling.

This is **Ben Lies's personal fork** of the [team project](https://github.com/C442/Rocket). It preserves the shared development work and provides an entry point into the engineering behind the rocket.

[![Watch the project video](Sketches/thumbnail.jpg)](https://www.youtube.com/watch?v=yQALvxHjtCE)

[Watch the project video](https://www.youtube.com/watch?v=yQALvxHjtCE) � [Flight software](FINAL_CODE/TVC-Flight-Code) � [Simulation](MatLab%20Sim) � [CAD](TVC/Design)

## Engineering highlights

- **Embedded C++:** flight-state management, peripheral integration and buffered SD-card logging on Teensy 4.1.
- **Attitude estimation:** BNO055 accelerometer/gyroscope readings with a Madgwick filter.
- **Control systems:** PID experiments and state-feedback control, thrust-curve interpolation and calibrated gimbal-to-servo mappings.
- **Modelling and analysis:** MATLAB/Simulink models, LQR gain calculation, actuator identification and Python/Jupyter data analysis.
- **Mechanical integration:** two-axis gimbal designs and a servo-driven parachute deployment mechanism.

## Start here

| Area | Entry point | What it contains |
| --- | --- | --- |
| Integrated firmware | [`TVC-Flight-Code`](FINAL_CODE/TVC-Flight-Code) | Flight loop, state machine, controller, sensors and logging |
| Main control implementation | [`Rocket.cpp`](FINAL_CODE/TVC-Flight-Code/Rocket.cpp) | Sensor fusion, state feedback, thrust interpolation and servo commands |
| Flight sequencing | [`StateMachine.cpp`](FINAL_CODE/TVC-Flight-Code/StateMachine.cpp) | Launch-pad idle, ascent, descent and landed states |
| Simulation | [`MatLab Sim`](MatLab%20Sim) | Simulink models and MATLAB scripts |
| Gimbal geometry | [`TVC/Design`](TVC/Design) | Printable mechanical parts |
| Experimental work | [`TVC`](TVC) | PID, state-feedback, calibration and sensor experiments |

## Hardware and software

The integrated firmware targets **Teensy 4.1** and uses a **BNO055 IMU**, a **BMP3XX-family barometer**, two TVC servos, a deployment servo and the built-in SD-card interface.

Dependencies include Arduino/Teensy support, Adafruit BNO055, Adafruit BMP3XX, MadgwickAHRS, Servo, SD and Wire. The source calls `setInitialRollPitch()` on the Madgwick filter; a compatible implementation is required, and the exact library revision is not recorded.

See the [firmware guide](FINAL_CODE/TVC-Flight-Code/README.md) for architecture, source entry points and build limitations.

## Visual overview

### Rocket and electronics

<img src="Sketches/rocket.png" alt="Rocket design overview" width="300"/>
<img src="Sketches/Board_Computer.png" alt="Flight computer board design" width="400"/>

### Thrust vector control

<img src="Sketches/TVC_Image.jpg" alt="Two-axis thrust vector control assembly" width="500"/>

### Parachute deployment prototype

<img src="Sketches/Chute_Deploy_Demo.gif" alt="Servo-driven parachute deployment demonstration" width="400"/>

## Status and scope

This is a development archive with integrated firmware, bench experiments, simulations and mechanical prototypes. The code requests a 100 Hz flight loop; that setting is not evidence of a measured sustained execution rate. Apogee and landing transitions in the integrated state machine use fixed time thresholds.

The repository does not establish successful closed-loop flight performance or a reproducible build. Simulation results and prototype demonstrations should be assessed separately from flight validation.

## Attribution

This fork originates from [C442/Rocket](https://github.com/C442/Rocket); the project is shared work. The original README credits use of ChatGPT for text editing and code generation.

The simulation folder includes a [MathWorks File Exchange reference](https://www.mathworks.com/matlabcentral/fileexchange/80716-modeling-a-thrust-vector-controlled-rocket-in-simulink) and its accompanying [licence](MatLab%20Sim/license.txt). Some mechanical inspiration comes from the [K-9 TVC gimbal](https://www.printables.com/model/9920-k-9-rocket-thrust-vector-control-gimbal-v8/related?lang=de). Retain the original attributions and licences when reusing those materials.

[Original project overview and references](https://github.com/BigblenHD/Rocket/blob/d0241f04cd03e6945dc0eed0d03ca0bd48970ab1/README.md) � [Ben's portfolio](https://benlies.com)
