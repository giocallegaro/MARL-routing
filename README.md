# **Multi Agent Reinforcement Learning Algorithm for Routing**

Discrete Event Simulation environment and Multi Agent Reinforcement Learning algorithm for routing opitmization in industrial applications.
The purpose of the project is to provide an optimized solution for routing, general and customizable to any use case respecting the following conditions:
- unidirectional flow;
- all products undergoing the same operations.

## Repository Structure

<pre>
├── ExperimentX/                   # Repository of the Experiments described in the thesis
    ├── Layout                     # Layout configuration files
    ├── SimulationCode             # Jupyter Notebook containing the DES and the MARL algorithm
├── requirements.txt               # List of dependencies
├── main.py                        # Main entry point
└── README.md                      # This documentation </pre>

## RL Algorithm Logic

The Reinforcement Learning algorithm effectiveness is strictly related to the accuracy of the state definitions.
The logic adopted in this project is the following: 
<img width="270" height="480" alt="FlowDiagram1" src="https://github.com/user-attachments/assets/7e93ca91-6330-4a07-b5ee-fe5855c6a618" />

## Jupyter Notebook Structure

<pre>
├── Import and Constants 
    ├── Import                     # Import of necessary libraries
    └── Constants                  # Definition of layout-dependent constants
├── Simulation Functions
    ├── Pallets                    # Generation of pallets
    ├── Environment                # Definition of the SimPy environment
    ├── Production Functions       # Definition of multiple configurable machine and agent functions
    ├── Get State Function         # Function capturing the state of the system
    ├── Configs                    # Configuration of the machines and the layout
    └── Source                     # Definition of the SimPy source functions
├── Random Policy                  # Simulation with RandomPolicy
├── Heuristic Policy Th            # Simulation with HeuristicPolicyTh
├── Heuristic Policy Flow          # Simulation with HeuristicPolicyFlow
├── RL Agent
    ├── Q-Table print Function     # Prints the Q-Table
    ├── Agent function             # Definition of the agent class (configurable)
    ├── Reduced State Function     # Reduces the complexity of the state
    ├── Configs                    # Configures the agents, machines and layout
    ├── Training                   # Automated training simulation
    └── Test                       # Simulation with RL-based policy </pre>

## Features

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

Machines need to be added to simpy environment, after that further configurations are needed to define the machines and the agents present in the system.
To do so, a dictionary for each machine is needed, where the parameters of the functions reported at 'Production Functions' have to be specified.
Depending on the kind of machine, a corresponding function among the available ones has to be chosen.

After accurately configuring the system, it is possible to run the simulations for the comparison policies. 
To run the RL policy, a new set of configuration dictionaries is needed, both for the agent and the machines, thus allowing for a higher level of customizability of the agents.
The training and the test phases duration can be different.

When running the simulations, a txt file is automatically generated for each replication, reporting the log of some events.
