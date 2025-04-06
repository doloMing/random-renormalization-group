# Overview
This is the code implementation of the random renormalization group presented in the paper entitled as "Random renormalization group for fast renormalizing ultra-large complex systems". 

The abstract of this paper is shown below:

Criticality and symmetry, fundamental concepts in modern physics theories of matter, are typically studied using the renormalization group (RG) method. However, computational costs limit the application of RG to large-scale datasets. Here we present the random renormalization group (RRG), an efficient framework that analyzes dynamics and structures in ultra-large systems (millions of units) within minutes. The RRG combines random projections, hashing techniques, and kernel representations to capture both linear and nonlinear correlations. For structural analysis, it identifies connectivity patterns, intrinsic scales, and symmetries through local topology correlations in kernel spaces. For dynamical analysis, it groups units into correlated clusters to study scaling behaviors and critical phenomena. Our experiments demonstrate the computational efficiency of the RRG, which achieves at least two orders of magnitude speedup while successfully identifying non-equilibrium phase transitions, criticality, and symmetries across diverse complex systems.

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
git clone https://github.com/doloMing/Random-renormalization-group
```

```python
pip install random-renormalization-group
```

# Basic instances:
```python
## Structure renormalization
X_Initial=nx.random_tree(10000) # Generate a random tree with 10000 units

RG_Flow,Tracked_ID_list=Renormalization_Flow(X_Initial,100,50,"Linear_Kernel","Structure") # Run a RRG for 100 iterations, where the dimension of hased binary vectors is 50

RG_Flow,Tracked_ID_list=Renormalization_Flow(X_Initial,50,10,"Gaussian_Kernel","Structure") # Run a RRG for 50 iterations, where the dimension of hased binary vectors is 10

RG_Flow,Tracked_ID_list=Renormalization_Flow(X_Initial,200,100,"Cauchy_Kernel","Structure") # Run a RRG for 200 iterations, where the dimension of hased binary vectors is 100

# Generate a random tree with 10000 units, and assign the weights by a power-law distribution
tree = nx.random_tree(10000)
nx.set_edge_attributes(tree, 1, 'number')
size = tree.number_of_edges() 
alpha = 2.0
weights = np.random.pareto(alpha, size) + 1
for i, (u, v) in enumerate(tree.edges()):
    tree[u][v]['weight'] = weights[i]

RG_Flow,Tracked_ID_list=Renormalization_Flow(tree,200,100,"Cauchy_Kernel","Structure",Weighted=True) # Run a RRG for 200 iterations, where the dimension of hased binary vectors is 100 and weight information is considered

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
