---
title: Models
layout: default
---

# Circles Model Overview

The circles benchmark model is a benchmark model originating from FLAME and FLAME GPU. It consists of a number of points which exert a repulsive and potentially attractive force over a limited range. Over a number of iterations the model will exhibit a force resolution which will ultimately result in a stable state. The model has origins in a number of biological systems and is analogous to that of cellular interactions of simple swarm systems.

The model has been used for extensive benchmarking of the FLAME and FLAME GPU frameworks and is excellent for testing message acceleration structures for spatially distributed models.

# Model Description

The position $$x$$ of a circle agent $$i$$ at a discrete time step $$t - 1$$ is given by;

$$x_{i(t+1)} = x_{i(t)} + F_{i}$$

where $$F_{i}$$ denotes the force exerted on agent $$i$$ calculated as;

$$F_{i} = \sum\limits_{i \neq j} F_{ij}^{rep}[d_{ij} - 2r <= 0] + F_{ij}^{att}[d_{ij} - 2r > 0]$$

The parameter $$r$$ is the homogeneous radius of the circle agent. The square Iverson bracket notation determines a condition for both the repulsive force $$F_{ij}^{rep}$$ and attractive force $$F_{ij}^{att}$$ between the agent $$i$$ and a neighbouring agent $$j$$. When the condition evaluates to true it returns a value of $$1$$ otherwise it is $$0$$. The value $$d_{ij}$$ is the distance between agent positions $$x_{i}$$ and $$x_{j}$$ given by;


$$ d_{ij} = \sqrt{ (x_{j} - x_{i})^2 } $$

The repulsive and attractive forces as defined as follows;

$$ F_{ij}^{rep} = \frac{k_{rep}(d_{ij} - 2r)(x_{j} - x_{i})} {d_{ij}} $$

$$ F_{ij}^{att} = \frac{k_{att}(d_{ij} - 2r)(x_{j} - x_{i})} {d_{ij}} $$

The parameters $$k_{rep}$$ and $$k_{att}$$ are the repulsive and attractive damping terms respectively.

# Initial Conditions

The initial conditions of the circles model are a randomly positioned set of circle agents. The random distribution should be linear and the following parameters should be used to benchmark the model.

$$W$$ The width and height of the environment in which agents are placed.
$$\rho$$ The density of agents within the environment (this will dictate the fixed number of agents)

# Model Parameters


| Parameter | Description |
| $$ k_{rep} $$ | The repulsive damping term. Increasing this value will encourage agents to separate.|
| $$ k_{att} $$ | The attractive damping term. Increasing this term will encourage agents to attract. |
| $$ r $$ | The interaction radius of the circle agents. Increasing this value will increase the communication between agents (assuming constant density) |
| $$ \rho $$ | The density of agents within the environment. Increasing this value will increase the communication within the model. |
| $$ W $$ | The width and height of the environment in which agents are placed. Increasing the environment size is equivalent to increasing the problem size $$ N $$ (i.e. the number of agents) given a fixed $$\rho$$. |
{:.decoratedtable}


The following suggested parameter configurations and benchmarks are suggested

| Benchmark Name | Description | Parameter Values |
| Strong Scaling Benchmark | Benchmark to test the increasing number of processors on a fixed model size. This benchmark tests the scalability of a particular simulator and is not suitable for evaluation between simulators.| $$k_{rep}=1.0$$, $$k_{att}=0.0, $$r=2.0$$, $$\rho$$ and $$W$$ can be user defined but must remain constant. |
| Weak Scaling Benchmark | Benchmark to test the sclability of simulators given a fixed workload per processor. This benchmark tests the scalability of a particular simulator. The performance scalability characteristics can be used for evaluation between simulators. | $$k_{rep}=1.0$$, $$k_{att}=0.0, $$r=2.0$$, $$\rho$$ user defined but constant, $$W$$ varying creating increasing problem size. |
| Simulator performacne scalability | Benchmark tests the simulator scalability with a fixed number of processors and an increasing problem size. The performance scalability characteristics can be used for evaluation between simulators. | $$k_{rep}=1.0$$, $$k_{att}=0.0, $$r=2.0$$, $$\rho$$ user defined but constant, $$W$$ varying creating increasing problem size. |
| Communication scalability | This benchmark will test the simulators ability to handle increasing communication between agents given a fixed problem size and fixed number of processors | $$k_{rep}=1.0$$, $$k_{att}=0.0, $$r=2.0$$, $$\rho$$ varying creating increased communication, $$W$$ user defined but constant. |
{:.decoratedtable}


# Reference Implementation

A reference implementation is provided as part of the [FLAME GPU SDK](https://github.com/FLAMEGPU/FLAMEGPU/tree/master/examples/CirclesBruteForce_float/src/model).

To comply with the OpenAB proposal a second implementation is required. 

