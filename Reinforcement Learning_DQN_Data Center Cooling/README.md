# Data Center Cooling DQN Project

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)    [![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)


## Project Objective

Optimize the control of the cooling system inside a data center to ultimately reduce energy usage and CO2 emissions associated with Data Centers without impacting performance.

## Formulating the MDP

__Model Simplification__
- View the data center as one entity with one server
- Assume we are able to get information about the network and workload to inform decisions for cooling

__Goal__
- Minimize the energy usage of the cooling system
- Hypothesis is that RL Agent can use additional information to make better, more proactive decisions

__Constraints__
- Must keep the temperatures between a minimum and maximum temperature range

__Question__
- Based on information that we have about the server given time interval, what should the cooling system do to satisfy that condition within the constraints? Heat? Cool? By how much?

__Possible States__

__Available Actions__
- Goal is to keep the server temperature optimal: 18°C ≤ Optimal Temperature ≤ 24°C
- When the temperature is above the range: Turn cooling on
- When the temperature is below the range: Turn heating on
- When the temperature is withing the range: Do nothing

__System Model__
- Each episode is a pre-defined period of time (e.g. one day)
- At each time T within the period of time the server temperature will be calculated based on a function of: 
	- The ambient temperature 
	- The data rate going through the server* 
	- The number of users logged on to the server*
		- 𝑇_𝑠𝑒𝑟𝑣𝑒𝑟=𝑓(𝑇_(𝑎𝑚𝑏 )+ 𝛽_1 𝑅_𝑑𝑎𝑡𝑎+ 𝛽_2 𝑁_𝑢𝑠𝑒𝑟𝑠)
		- *(Random value within a pre-defined range)

__Rewards__
- Our goal is to save energy, so it will be rewarded on how much energy it saved compared to the non-AI cooling system
		𝑅 =𝑓(𝐸_𝑁𝑜 𝐴𝐼− 𝐸_𝐴𝐼)
- There is a linear relationship between a change and temperature and the cooling energy usage. Thus, this further simplifies to:
		𝑅 = ΔT_𝑁𝑜 𝐴𝐼 − Δ T_𝐴𝐼
Where T is the temperature setpoint by the AI and non-AI at any given point in time. 

__Game Over__
- As the agent explores, it may get to an upper and lower bound of the temperature constraints. When this happens, the episode will end, and move to the next one to avoid introducing states that are outside of our bounds.

## Solving the MDP Using DQN Learning Algorithm

## Hyperparameter Tuning

## A Top Performing Model Tested For a Full Year
- 87% Energy Savings during Hyperparameter Tuning vs. 89% Energy Savings over the course of the full year
- AI learns to operate in a wider temperature range

## Testing Robustness 
- To test the robustness of the model and how well it deals with changes to the environment, we trained it on one set of β coefficients, and then modified each one to test the effects
