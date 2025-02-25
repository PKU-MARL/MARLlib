

<div align="center">
<img src=image/logo2-1.png width=70% />
</div>

**Multi-Agent RLlib (MARLlib)** is a *MARL benchmark* based on [**Ray**](https://github.com/ray-project/ray) and one of its toolkits [**RLlib**](https://github.com/ray-project/ray/tree/master/rllib). 
It provides MARL research community a unified platform for developing and evaluating the new ideas in various multi-agent environments.
There are four core features of **MARLlib**. 

- it collects most of the existing MARL algorithms that are widely acknowledged by the community and unifies them under one framework. 
- it gives a solution that enables different multi-agent environments using the same interface to interact with the agents.
- it guarantees great efficiency in both the training and sampling process.
- it provides trained results including learning curves and pretrained models specific to each task and each algorithm's combination, with finetuned hyper-parameters to guarantee credibility. 

**Project Website**: https://sites.google.com/view/marllib/home


--------------------------------------------------------------------------------
The README is organized as follows:
- [**Overview**](#Part-I.-Overview)
- [**Environment**](#Part-II.-Environment)
- [**Algorithm**](#Part-III.-Algorithm)
- [**Getting started & Examples**](#Part-VI.-Getting-started)
- [**Bug Shooting**](#Part-VI.-Getting-started)

### Part I. Overview

We collected most of the existing multi-agent environment and multi-agent reinforcement learning algorithms and unify them under one framework based on [**Ray**](https://github.com/ray-project/ray)'s [**RLlib**](https://github.com/ray-project/ray/tree/master/rllib) to boost the MARL research. 

The common MARL baselines include **independence learning (IQL, A2C, DDPG, TRPO, PPO)**, **centralized critic learning (COMA, MADDPG, MAPPO, HATRPO)**, and **value decomposition (QMIX, VDN, FACMAC, VDA2C)** are all implemented.

The popular MARL environments like **SMAC, MaMujoco, Google Research Football** are all provided with a unified interface.

The algorithm code and environment code are fully separated. Changing the environment needs no modification on the algorithm side and vice versa.

The tutorial of RLlib can be found at https://docs.ray.io/en/releases-1.8.0/rllib/index.html.
Fast examples can be found at https://docs.ray.io/en/releases-1.8.0/rllib-examples.html. 
These will help you easily dive into RLlib.

We hope everyone interested in MARL can be benefited from MARLlib.



### Part II. Environment

#### Supported Multi-agent Environments / Tasks

Most of the popular environment in MARL research has been incorporated in this benchmark:

| Env Name | Learning Mode | Observability | Action Space | Observations |
| ----------- | ----------- | ----------- | ----------- | ----------- |
| [LBF](https://github.com/semitable/lb-foraging)  | Mixed | Both | Discrete | Discrete  |
| [RWARE](https://github.com/semitable/robotic-warehouse)  | Collaborative | Partial | Discrete | Discrete  |
| [MPE](https://github.com/openai/multiagent-particle-envs)  | Mixed | Both | Both | Continuous  |
| [SMAC](https://github.com/oxwhirl/smac)  | Cooperative | Partial | Discrete | Continuous |
| [MetaDrive](https://github.com/decisionforce/metadrive)  | Collaborative | Partial | Continuous | Continuous |
|[MAgent](https://www.pettingzoo.ml/magent) | Mixed | Partial | Discrete | Discrete |
| [Pommerman](https://github.com/MultiAgentLearning/playground)  | Mixed | Both | Discrete | Discrete |
| [MaMujoco](https://github.com/schroederdewitt/multiagent_mujoco)  | Cooperative | Partial | Continuous | Continuous |
| [GRF](https://github.com/google-research/football)  | Collaborative | Full | Discrete | Continuous |
| [Hanabi](https://github.com/deepmind/hanabi-learning-environment) | Cooperative | Partial | Discrete | Discrete |

Each environment has a readme file, standing as the instruction for this task, talking about env settings, installation, and some important notes.

### Part III. Algorithm

We provide three types of MARL algorithms as our baselines including:

**Independent Learning:** 
IQL
DDPG
PG
A2C
TRPO
PPO

**Centralized Critic:**
COMA 
MADDPG 
MAAC 
MAPPO
MATRPO
HATRPO
HAPPO

**Value Decomposition:**
VDN
QMIX
FACMAC
VDAC
VDPPO

Here is a chart describing the characteristics of each algorithm:

| Algorithm | Support Task Mode | Need Global State | Action | Learning Mode  | Type |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| IQL  | Mixed | No | Discrete | Independent Learning | Off Policy
| PG  | Mixed | No | Both | Independent Learning | On Policy
| A2C  | Mixed | No | Both | Independent Learning | On Policy
| DDPG  | Mixed | No | Continuous | Independent Learning | Off Policy
| TRPO  | Mixed | No | Both | Independent Learning | On Policy
| PPO  | Mixed | No | Both | Independent Learning | On Policy
| COMA  | Mixed | Yes | Both | Centralized Critic | On Policy
| MADDPG  | Mixed | Yes | Continuous | Centralized Critic | Off Policy
| MAA2C  | Mixed | Yes | Both | Centralized Critic | On Policy
| MATRPO  | Mixed | Yes | Both | Centralized Critic | On Policy
| MAPPO  | Mixed | Yes | Both | Centralized Critic | On Policy
| HATRPO  | Cooperative | Yes | Both | Centralized Critic | On Policy
| HAPPO  | Cooperative | Yes | Both | Centralized Critic | On Policy
| VDN | Cooperative | No | Discrete | Value Decomposition | Off Policy
| QMIX  | Cooperative | Yes | Discrete | Value Decomposition | Off Policy
| FACMAC  | Cooperative | Yes | Discrete | Value Decomposition | Off Policy
| VDAC  | Cooperative | Yes | Both | Value Decomposition | On Policy
| VDPPO | Cooperative | Yes | Both | Value Decomposition | On Policy

**Current Task & Available algorithm mapping**: Y for available, N for not suitable, P for partially available on some scenarios.
(Note: in our code, independent algorithms may not have **I** as prefix. For instance, PPO = IPPO)

| Env w Algorithm | IQL | PG | A2C | DDPG | TRPO | PPO | COMA | MADDPG | MAAC | MATRPO | MAPPO | HATRPO | HAPPO| VDN | QMIX | FACMAC| VDAC | VDPPO 
| ---- | ---- | ---- | ---- | ---- | ---- | ----- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |  ---- | ---- | ---- | ---- | ---- |
| LBF         | Y | Y | Y | N | Y | Y | Y | N | Y | Y | Y | Y | Y | P | P | P | P | P |
| RWARE       | Y | Y | Y | N | Y | Y | Y | N | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| MPE         | P | Y | Y | P | Y | Y | P | P | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| SMAC        | Y | Y | Y | N | Y | Y | Y | N | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| MetaDrive  | N | Y | Y | Y | Y | Y | N | Y | Y | Y | Y | Y | Y | N | N | N | N | N |
| MAgent      | Y | Y | Y | N | Y | Y | Y | N | Y | Y | Y | Y | Y | N | N | N | N | N |
| Pommerman   | Y | Y | Y | N | Y | Y | P | N | Y | Y | Y | Y | Y | P | P | P | P | P |
| MaMujoco    | N | Y | Y | Y | Y | Y | N | Y | Y | Y | Y | Y | Y | N | N | Y | Y | Y |
| GRF         | Y | Y | Y | N | Y | Y | Y | N | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| Hanabi      | Y | Y | Y | N | Y | Y | Y | N | Y | Y | Y | Y | Y | N | N | N | N | N |

### Part IV. Getting started

Install Ray 
```
pip install ray==1.8.0 # version sensitive
```


Add patch of MARLlib
```
cd patch
python add_patch.py
```

**Y** to replace source-packages code

**Attention**: Above is the common installation. Each environment needs extra dependency. Please read the installation instruction in envs/base_env/install.

Examples
```
python marl/main.py --algo_config=MAPPO [--finetuned] --env-config=smac with env_args.map_name=3m
```
--finetuned is optional, force using the finetuned hyperparameter 

We provide an introduction to the code directory to help you get familiar with the codebase:

* top level directory structure

<div align="center">
<img src=image/code-MARLlib.png width=120% />
</div>

This picture is in image/code-MARLlib.png

* MARL directory structure

<div align="center">
<img src=image/code-MARL.png width=70% />
</div>

This picture is in image/code-MARL.png.png

* ENVS directory structure

<div align="center">
<img src=image/code-ENVS.png width=70% />
</div>

This picture is in image/code-ENVS.png.png


### Part V. Bug Shooting

- observation/action out of space bug:
    - make sure the observation/action space defined in env init function 
        - has same data type with env returned data (e.g., float32/64)
        - env returned data range is in the space scope (e.g., box(-2,2))
    - the returned env observation contained the required key (e.g., action_mask/state)

--------------------------------------------------------------------------------
## License

The MIT License