# **Multi Agent Reinforcement Learning Algorithm for Routing**

Discrete Event Simulation environment and Multi Agent Reinforcement Learning algorithm for routing opitmization in industrial applications.
The purpose of the project is to provide an optimized solution for routing, general and customizable to any use case respecting the following conditions:
- unidirectional flow;
- all products undergoing the same operations.

## Repository Structure

├── des_env/ # Discrete Event Simulation environment modules
├── marl/ # Multi-Agent Reinforcement Learning agents and training logic
├── configs/ # YAML/JSON configuration files
├── utils/ # Helper functions and visualization scripts
├── results/ # Output data, logs, and trained model checkpoints
├── requirements.txt # List of dependencies
├── main.py # Main entry point
└── README.md # Project documentation

## Features.

To adapt the environment to the configuration under analysis, the following constants and variables have to be configured:

- for each machine x, a constant called MACHINE_TIME_x representing the mean value of the processing time on machine x;
- for each machine x, a variable called machine_time_x representing the processing time probability distribution on machine x;
- for each pair of connected machines (x, y), a constant called TRANSPORT_TIME_x_y representing the mean value of the transport time between machine x and machine y;
- for each pair of connected machines (x, y), a variable called transport_time_x_y representing the transport time probability distribution between machine x and machine y;
- SOURCE_TIME, a constant for the initial period of generation of pallets;
- SEED_PALLET, a constant for tracking the random generation of pallets;
- for each machine x, a constant called CAP_BUF_x representing the buffer capacity of machine x;
- SIMULATION_LENGTH, a constant representing the length of the simulation;
- NUM_PALLET, a constant representing the total number of pallets generated;

For the Reinforcement Learning agents, the following constants are required:
- PALLET_STAR, a constant corresponding to the pallet code of the aimed target pallet;
- T_STEP, a constant defining the sampling frequency;
- T_START, a constant defining the moment to start the sampling process;
- TH_P, a constant defining the positive reward for the end of the episode (the completion of the target pallet);
- STEP, a constant defining the negative reward assigned at each sample.

To define the sequence of operations to be performed by each pallet, it is possible to modify the value of the string sequence.
A pallet is a class defined by these fields:
- sequence, a string which for the current state of the algorithm is the same for all pallets;
- next_ope, a number defining what element of the string sequence contains the next operation to be performed on the pallet;
- pallet, a fixed number for each pallet, representing the pallet id;
- product, a dynamic variable representing the id of the product carried by the pallet.
