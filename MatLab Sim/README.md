# Rocket modelling and control analysis

MATLAB/Simulink models and supporting scripts used during TVC development.

## Files

| File | Purpose |
| --- | --- |
| `RocketStateSpace.slx` | State-space rocket model |
| `advancedTVCRocketModel.slx` | Additional TVC simulation model |
| `State_Control_Matrices.m` | Defines a two-state model and calculates feedback gains using `lqr` |
| `Thrust_Data.m` | Thrust-data preparation |
| `TVC_Identification.m` | Prepares input/output data as an `iddata` object |
| `Get_Logged_Data.m` | Logged-data helper |

## Getting started

Open MATLAB in this folder and inspect the model's callbacks and workspace dependencies before running a simulation. `lqr` requires Control System Toolbox; `iddata` requires System Identification Toolbox. Simulink model requirements depend on the blocks used, and the project's MATLAB release is not recorded.

`TVC_Identification.m` expects `simdata_tvc.txt` and `simdata_realtvc.txt` in the working directory. Those files are stored under [`TVC/Real_Life_Simulation`](../TVC/Real_Life_Simulation); adjust the paths or copy the files into your working directory.

The gain-calculation script and firmware contain different controller settings. Treat them as development revisions rather than assuming the script reproduces the deployed configuration.

## Upstream reference and attribution

The original documentation cites [Modeling a Thrust Vector Controlled Rocket in Simulink](https://www.mathworks.com/matlabcentral/fileexchange/80716-modeling-a-thrust-vector-controlled-rocket-in-simulink) and the accompanying [BPS.Space video](https://www.youtube.com/watch?v=nwgd1CV__rs). The included [licence](license.txt) applies to the corresponding upstream material.

The original instructions referred to `simpleTVCRocketModel.slx`, which is not present in this fork. Use the model files listed above.

![Gimballed thrust diagram](https://upload.wikimedia.org/wikipedia/commons/7/7a/En_Gimbaled_thrust_diagram.svg)

Diagram: [Brian0918 / Titimaster, Wikimedia Commons](https://commons.wikimedia.org/wiki/File:En_Gimbaled_thrust_diagram.svg), public domain.
