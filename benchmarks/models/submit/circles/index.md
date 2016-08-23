---
title: Models
layout: default
---

# Circles Model Overview

The circles benchmark model is a benchmark model originating from FLAME and FLAME GPU. It consists of a number of points which exert a repulsive and potentially attractive force over a limited range $$2r$$. Over a number of iterations the model will exhibit a force resolution which will ultimately result in a stable state. The model has origins in a number of biological systems and is analogous to that of cellular interactions of simple swarm systems.

The model has been used for extensive benchmarking of the FLAME and FLAME GPU frameworks and is excellent for testing message acceleration structures for spatially distributed models.

# Model Description

The position $$x$$ of a circle agent $$i$$ at a discrete time step $$t + 1$$ is given by;

$$\overrightarrow{x_{i(t+1)}} = \overrightarrow{x_{i(t)}} + \overrightarrow{F_{i}}$$

where $$F_{i}$$ denotes the force exerted on agent $$i$$ calculated as;

$$\overrightarrow{F_{i}} = \sum\limits_{i \neq j} \overrightarrow{F_{ij}^{rep}}[\lVert\overrightarrow{x_{i}x_{j}}\rVert < r] + \overrightarrow{F_{ij}^{att}}[r <= \lVert\overrightarrow{x_{i}x_{j}}\rVert < 2r]$$

The parameter $$r$$ is the homogeneous radius of the circle agent. The square Iverson bracket notation determines a condition for both the repulsive force $$F_{ij}^{rep}$$ and attractive force $$F_{ij}^{att}$$ between the agent $$i$$ and a neighbouring agent $$j$$. When the condition evaluates to true it returns a value of $$1$$ otherwise it is $$0$$. The value $$d_{ij}$$ is the distance between agent positions $$x_{i}$$ and $$x_{j}$$ given by;


$$ d_{ij} = \sqrt{ (x_{j} - x_{i})^2 } $$

The repulsive and attractive forces as defined as follows;

$$ \overrightarrow{F_{ij}^{rep}} = k_{rep}(\lVert\overrightarrow{x_{i}x_{j}}\rVert)\frac{\overrightarrow{x_{i}x_{j}}}{\lVert\overrightarrow{x_{i}x_{j}}\rVert} $$

$$ \overrightarrow{F_{ij}^{att}} = k_{att}(2r-\lVert\overrightarrow{x_{j}x_{i}}\rVert)\frac{\overrightarrow{x_{j}x_{i}}}{\lVert\overrightarrow{x_{j}x_{i}}\rVert} $$

The parameters $$k_{rep}$$ and $$k_{att}$$ are the repulsive and attractive damping terms respectively.

After the location has been calculated, it must be clamped within the environmental bounds $$0<=x<=W-1$$, as specified by the parametered $$W$$ (see below).

# Initial Conditions

The initial conditions of the circles model are a randomly positioned set of circle agents. The random distribution should be linear and the following parameters should be used to benchmark the model.

$$W$$ The width and height of the environment in which agents are placed.
$$\rho$$ The density of agents within the environment.
$$E_{dim}$$ The dimensionality of the environment (in most cases this will be $$ 2 $$ or $$ 3 $$).

$$ A_{pop} $$ The constant agent population size is then calculated according to the formula;

$$ A_{pop} = \left\lfloor{W^{E_{dim}} \rho}\right\rfloor$$ 

# Validation

Precise validation can be carried out by seeding two independent implementations with the same initial agent locations. With appropriate model paramters it is possible to export agent locations after a single iteration to confirm they remain in agreement to several decimal places.

Due to the severe force fall-off when agents cross the boundary of $$r$$ units seperation, minor floating point differences can quickly cause models to diverge, which then snowballs affecting more agents.

# Model Parameters


| Parameter | Description |
| $$ k_{rep} $$ | The repulsive damping term. Increasing this value will encourage agents to separate.|
| $$ k_{att} $$ | The attractive damping term. Increasing this term will encourage agents to attract. |
| $$ r $$ | The interaction radius of the circle agents. Increasing this value will increase the communication between agents (assuming uniform density) |
| $$ \rho $$ | The density of agents within the environment. Increasing this value will increase the communication within the model. |
| $$ W $$ | The width and height of the environment in which agents are placed. Increasing the environment size is equivalent to increasing the problem size $$ N $$ (i.e. the number of agents) given a fixed $$\rho$$. |
{:.decoratedtable}


The following suggested parameter configurations and benchmarks are suggested

| Benchmark Name | Description | Parameter Values |
| Problem scale | This benchmark will test the simulators ability to handle greater problem size. | $$k_{rep}=1\times10^{-3}$$, $$k_{att}=1\times10^{-3}$$, $$\rho$$ and $$r$$ user defined but constant. Varying $$W$$ will increase the number of agents within the environment, and hence the problem scale.  |
| Neighbourhood scale/Communication scale | This benchmark will test the simulators ability to handle increasing communication between agents given a fixed problem size and fixed number of processors, by increasing the size of each agents neighbourhood. | $$k_{rep}=1\times10^{-3}$$, $$k_{att}=1\times10^{-3}$$, $$\rho=0.01$$, $$r$$ varying creating increased communication, $$W$$ user defined but constant. |
| Entropy/Agent Activity | This benchmark will test the simulators ability to handle increasing motion of agents given a fixed problem size and number of processors. Most implementations will have stable performance throughout this benchmark. | $$r=5.0$$, $$\rho$$ and $$W$$ can be user defined but constant. Varying $$k_{rep}$$ and $$k_{att}$$ such that the difference between the two parameters increases, will increase agent speeds. |
| Nodes Scaling Benchmark | Benchmark to test the increasing number of processors on a fixed model size. This benchmark tests the scalability of a particular simulator and is not suitable for evaluation between simulators.| $$k_{rep}=1.0$$, $$k_{att}=0.0$$, $$r=2.0$$, $$\rho$$ and $$W$$ can be user defined but must remain constant. |
{:.decoratedtable}


# Reference Implementation

3D reference implementations in: FLAME GPU, MASON and Repast Simphony are available [here](https://github.com/Robadob/circles-benchmark), alongside a spreadsheet of results.

A 2D reference implementation is provided as part of the [FLAME GPU SDK](https://github.com/FLAMEGPU/FLAMEGPU/tree/master/examples/CirclesBruteForce_float/src/model).

