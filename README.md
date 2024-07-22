# Overview
This is the code implementation of the random renormalization group presented in the paper entitled as "Fast renormalizing the structures and dynamics of ultra-large systems via random renormalization group". 

The abstract of this paper is shown below:

Criticality and symmetry, studied by the renormalization groups, lie at the heart of modern physics theories of matters and complex systems. However, surveying these properties with massive experimental data is bottlenecked by the intolerable costs of computing renormalization groups on real systems. Here, we develop a time- and memory-efficient framework, termed as the random renormalization group, for renormalizing ultra-large systems (e.g., with millions of units) within minutes. This framework is based on random projections, hashing techniques, and kernel representations, which support the renormalization governed by linear and non-linear correlations. For system structures, it exploits the correlations among local topology in kernel spaces to unfold the connectivity of units, identify intrinsic system scales, and verify the existences of symmetries under scale transformation. For system dynamics, it renormalizes units into correlated clusters to analyze scaling behaviours, validate scaling relations, and investigate potential criticality. Benefiting from hashing-function-based designs, our framework significantly reduces computational complexity compared with classic renormalization groups, realizing a single-step acceleration of two orders of magnitude. Meanwhile, the efficient representation of different kinds of correlations in kernel spaces realized by random projections ensures the capacity of our framework to capture diverse unit relations. As shown by our experiments, the random renormalization group helps identify non-equilibrium phase transitions, criticality, and symmetry in diverse large-scale genetic, neural, material, social, and cosmological systems.

Two Jupyter notebook files are released as the instances of applying the random renormalization group on dynamics and structure renormalization. The full descriptions of all functions in this files can be seen in the attached PDF file, which is the supplementary material of the paper.

# Instructions
The notebook files can be run directly over simulated data.  To run the codes with real data, one only needs to change the input of the function Renormalization_Flow. We refer to “Fast_renormalizing_the_structures_and_dynamics_of_ultra_large_systems_via_random_renormalization_group_SM_.pdf” for detailed descriptions and usages of other functions.

# System requirements
## Hardware requirements
Our codes only require a modest size computer with enough RAM to support in-memory operations. All the computations are implemented in a CPU environment. To date, our codes have been implemented in a 256GB environment with two Intel Xeon Gold 5218 processors and a 32GB environment with a Intel Core i7-8750H CPU for testing.

## OS requirements
Our codes have been tested on the following system:
+ windows 10

## Python dependencies
Our codes mainly depends on following packages:
```python
numpy
scipy
faiss
networkx
datasketch
statsmodels
```

# Installation guide:
```python
git clone https://github.com/Asuka-Research-Group/Random-renormalization-group
```

# Basic instances:
```python
## Structure renormalization
X_Initial=nx.random_tree(10000) # Generate a random tree with 10000 units

RG_Flow,Tracked_ID_list=Renormalization_Flow(X_Initial,100,50,"Linear_Kernel","Structure") # Run a RRG for 100 iterations, where the dimension of hased binary vectors is 50

RG_Flow,Tracked_ID_list=Renormalization_Flow(X_Initial,50,10,"Gaussian_Kernel","Structure") # Run a RRG for 50 iterations, where the dimension of hased binary vectors is 10

RG_Flow,Tracked_ID_list=Renormalization_Flow(X_Initial,200,100,"Cauchy_Kernel","Structure") # Run a RRG for 200 iterations, where the dimension of hased binary vectors is 100

## Dynamics renormalization
X_Initial = np.random.randn(10000, 50000) # Generate a system with 10000 units, where each unit exhibits random dynamics for 50000 time steps

RG_Flow,Tracked_ID_list=Renormalization_Flow(X_Initial,100,50,"Linear_Kernel","Dynamics") # Run a RRG for 100 iterations, where the dimension of hased binary vectors is 50

RG_Flow,Tracked_ID_list=Renormalization_Flow(X_Initial,50,10,"Gaussian_Kernel","Dynamics") # Run a RRG for 50 iterations, where the dimension of hased binary vectors is 10

RG_Flow,Tracked_ID_list=Renormalization_Flow(X_Initial,200,100,"Cauchy_Kernel","Dynamics") # Run a RRG for 200 iterations, where the dimension of hased binary vectors is 100
```

# Structure renormalization analysis pipeline:
```python

X_Initial=nx.random_tree(10000) # Generate a random tree with 10000 units

RG_Flow,Tracked_ID_list=Renormalization_Flow(X_Initial,100,50,"Linear_Kernel","Structure") # Run a RRG for 100 iterations, where the dimension of hased binary vectors is 50

Mean_K_S_Static=KS_Analysis(RG_Flow) # Verify the potential existence of scale-invariance
```

# Dynamics renormalization analysis pipeline:
```python

X_Initial = np.random.randn(10000, 50000) # Generate a system with 10000 units, where each unit exhibits random dynamics for 50000 time steps

RG_Flow,Tracked_ID_list=Renormalization_Flow(X_Initial,100,50,"Linear_Kernel","Dynamics") # Run a RRG for 100 iterations, where the dimension of hased binary vectors is 50

Cut_Off_Ratio=0.1
Normalized_activity=Normalized_Dynamics(RG_Flow,Tracked_ID_list,Cut_Off_Ratio) # Obtain the normalized dynamics probability distribution

MeanClusterSize, MeanVar, Coeff, Alpha, R2, MSE, Esti_Alpha_Scaling = Alpha_Scaling(RG_Flow,Tracked_ID_list) # Scaling analysis of variance

MeanClusterSize, FreeEV, Coeff, Beta, R2, MSE, Esti_Beta_Scaling = Beta_Scaling(RG_Flow,Tracked_ID_list) # Scaling analysis of effective free energy

Average_Rank_K, Average_Evals, Coeff, Mu, R2, MSE, Esti_Mu_Scaling = Mu_Scaling(RG_Flow,Tracked_ID_list) # Scaling analysis of eigenvalue spectrum

ScaledT, MeanACFs, MeanClusterSize, Tau, Coeff, Theta, R2, MSE, Esti_Theta_Scaling = Theta_Scaling(RG_Flow,Tracked_ID_list) # Dynamic scaling
```

# License
This project is covered under the **MIT License**.
